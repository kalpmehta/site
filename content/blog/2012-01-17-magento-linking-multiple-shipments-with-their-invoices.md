---
id: 187
title: 'Magento: Linking multiple shipments with their invoices'
date: '2012-01-17T17:17:39+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=187'
permalink: /index.php/2012/01/17/magento-linking-multiple-shipments-with-their-invoices/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2011/12/31/magento-admin-forcing-invoice-and-ship-button-together/"     class="crp_title">Magento Admin &#8211; Forcing Invoice and Ship button together</a></li><li><a href="http://ka.lpe.sh/2012/01/17/magento-adding-column-to-sales_flat_order_item-sales_flat_invoice_item-and-sales_flat_shipment_item/"     class="crp_title">Magento: Adding column to sales_flat_order_item, sales_flat_invoice_item and sales_flat_shipment_item</a></li><li><a href="http://ka.lpe.sh/2013/04/18/change-default-length-of-increment-id-for-orders-invoices-shipments-creditmemos/"     class="crp_title">Change default length of Increment ID for orders, invoices, shipments, creditmemos</a></li><li><a href="http://ka.lpe.sh/2013/04/28/magento-get-all-invoices-and-shipments-of-an-order/"     class="crp_title">Magento get all invoices and shipments of an order</a></li><li><a href="http://ka.lpe.sh/2012/01/08/magento-save-shipment-information-tracking-number-carrier-code-programatically/"     class="crp_title">Magento: Save shipment information of order programatically</a></li></ul></div>'
categories:
    - Magento
    - 'Magento admin'
tags:
    - 'linking invoice with shipment'
    - magento
    - 'multiple invoices'
    - 'multiple shipments'
---

In Magento, it’s a feature to create multiple invoices and shipments. But you can’t find the link between invoice with their respective shipment if you have more than one invoice and shipment. It’s because if you have forced invoice and shipment enabled (Invoice and Ship button combined in Manage Orders view page), it saves both invoice and shipment object together and hence can’t give the invoice id to shipment and hence fails in building the link between them.

So what we need to do here is:  
1\. Add a column to sales_flat_shipment which will store invoice increment id (say invoice_id)  
2\. Before invoice and shipment are saved, get the invoice’s latest increment id and increment it by 1 (to get next invoice increment id)  
3\. Give that invoice increment id to shipment object, so it will get saved along with other shipment columns

Here we go technically,  
  
Firstly, add a column to sales_flat_shipment table.  
{{< highlight php "style=emacs" >}}<?php $installer = $this;

$installer->
startSetup();

$installer->run(”  
ALTER TABLE sales_flat_shipment ADD COLUMN invoice_id VARCHAR(50) AFTER increment_id  
“);

$installer->endSetup();

?>{{< /highlight >}}

Then, override InvoiceController.php of sales/order: Mage/Adminhtml/controllers/Sales/Order/InvoiceController.php  
Paste this code to newly overridden file:

{{< highlight php "style=emacs" >}}<?php require_once('Mage/Adminhtml/controllers/Sales/Order/InvoiceController.php');
class Namespace_Module_Sales_Order_InvoiceController extends Mage_Adminhtml_Sales_Order_InvoiceController
{
    /**
     * @author - Kalpesh Mehta
     * @desc - Rewritten this method for linking shipment and invoice
     */

    public function saveAction()
    {
        $data = $this->
getRequest()->getPost(‘invoice’);  
 $orderId = $this->getRequest()->getParam(‘order_id’);

 if (!empty($data[‘comment_text’])) {  
 Mage::getSingleton(‘adminhtml/session’)->setCommentText($data[‘comment_text’]);  
 }

 try {  
 $invoice = $this->_initInvoice();  
 if ($invoice) {  
 if (!empty($data[‘capture_case’])) {  
 $invoice->setRequestedCaptureCase($data[‘capture_case’]);  
 }  
 if (!empty($data[‘comment_text’])) {  
 $invoice->addComment($data[‘comment_text’], isset($data[‘comment_customer_notify’]), isset($data[‘is_visible_on_front’]));  
 }

 $invoice->register();

 if (!empty($data[‘send_email’])) {  
 $invoice->setEmailSent(true);  
 }  
 $invoice->getOrder()->setCustomerNoteNotify(!empty($data[‘send_email’]));  
 $invoice->getOrder()->setIsInProcess(true);

 $transactionSave = Mage::getModel(‘core/resource_transaction’)  
 ->addObject($invoice)  
 ->addObject($invoice->getOrder());  
 $shipment = false;

 if (!empty($data[‘do_shipment’]) || (int) $invoice->getOrder()->getForcedDoShipmentWithInvoice()) {  
 $shipment = $this->_prepareShipment($invoice);  
 if ($shipment) {

 //Get last invoice increment ID  
 $invoiceLast = Mage::getModel(‘sales/order_invoice’)->getCollection()  
 ->setOrder(‘increment_id’,’DESC’)  
 ->setPageSize(1)  
 ->setCurPage(1);

 $invLastIncrId = $invoiceLast->getFirstItem()->getIncrementId();  
 $invNewIncrId = (int)$invLastIncrId + 1; //incrementing by 1  
 $shipment->setInvoiceId($invNewIncrId); //setting data for our sales_flat_shipment table column invoice_id

 $shipment->setEmailSent($invoice->getEmailSent());  
 $transactionSave->addObject($shipment);  
 }  
 }  
 $transactionSave->save();

 if (!empty($data[‘do_shipment’]) || (int) $invoice->getOrder()->getForcedDoShipmentWithInvoice()) {  
 $this->_getSession()->addSuccess($this->__(‘The invoice and shipment have been created.’));  
 } else {  
 $this->_getSession()->addSuccess($this->__(‘The invoice has been created.’));  
 }

 // send invoice/shipment emails  
 $comment = ”;  
 if (isset($data[‘comment_customer_notify’])) {  
 $comment = $data[‘comment_text’];  
 }  
 try {  
 $invoice->sendEmail(!empty($data[‘send_email’]), $comment);  
 } catch (Exception $e) {  
 Mage::logException($e);  
 $this->_getSession()->addError($this->__(‘Unable to send the invoice email.’));  
 }  
 if ($shipment) {  
 try {  
 $shipment->sendEmail(!empty($data[‘send_email’]));  
 } catch (Exception $e) {  
 Mage::logException($e);  
 $this->_getSession()->addError($this->__(‘Unable to send the shipment email.’));  
 }  
 }  
 Mage::getSingleton(‘adminhtml/session’)->getCommentText(true);  
 $this->_redirect(‘*/sales_order/view’, array(‘order_id’ => $orderId));  
 } else {  
 $this->_redirect(‘*/*/new’, array(‘order_id’ => $orderId));  
 }  
 return;  
 } catch (Mage_Core_Exception $e) {  
 $this->_getSession()->addError($e->getMessage());  
 } catch (Exception $e) {  
 $this->_getSession()->addError($this->__(‘Unable to save the invoice.’));  
 Mage::logException($e);  
 }  
 $this->_redirect(‘*/*/new’, array(‘order_id’ => $orderId));  
 }

}{{< /highlight >}}