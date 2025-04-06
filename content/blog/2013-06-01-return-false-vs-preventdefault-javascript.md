---
id: 684
title: 'return false vs preventDefault in javascript'
date: '2013-06-01T22:53:39+00:00'
author: kalpesh
layout: post
guid: 'http://ka.lpe.sh/?p=684'
permalink: /index.php/2013/06/01/return-false-vs-preventdefault-javascript/
crp_related_posts:
    - '<div id="crp_related" class="crp_related"><h3>Related Posts:</h3><ul><li><a href="http://ka.lpe.sh/2012/10/22/magento-add-products-to-placed-order-programatically/"     class="crp_title">Magento: Add products to placed order programatically</a></li><li><a href="http://ka.lpe.sh/2012/10/22/wordpress-show-total-aggregate-ratings-and-reviews-to-your-posts-pages/"     class="crp_title">WordPress: Show total/aggregate ratings and reviews to your posts/pages</a></li><li><a href="http://ka.lpe.sh/2013/02/25/magento-design-patterns/"     class="crp_title">Magento: Design Patterns</a></li><li><a href="http://ka.lpe.sh/2012/04/15/magento-difference-between-source_model-frontend_model-backend_model/"     class="crp_title">Magento: Difference between source_model, frontend_model, backend_model</a></li><li><a href="http://ka.lpe.sh/2013/06/01/jquery-prototype-conflict/"     class="crp_title">jQuery Prototype conflict, resolve it using noconflict</a></li></ul></div>'
categories:
    - jQuery
    - 'Prototype JS'
tags:
    - javascript
    - jquery
    - prototypejs
---

This post will help you to differentiate between javascript’s *return false*, *preventDefault*, *stopPropagation* and *stopImmediatePropagation*.

The first thing you learn when using javascript is to use *return false*. That’s the best thing we think to cancel browser’s default behavior, to stop further execution of an event. If you are using a simple function which returns what you want, then probably you won’t notice anything wrong in using *return false*. But when you want event to propagate, *return false* will not be helpful and will give unexpected result.

## What is event propagation?

When a single event, such as a mouse click, if is handled by two or more event handlers defined in various location of the DOM hiearachy, then the event handling starts by executing for individual elements at the lowest level. There are two models of this event propagation, *event bubbling* and *event capturing*.

<u>Event bubbling</u> is when an event has more than one event handler and event handling execution starts from **bottom to top** i.e. from individual links to it’s parent element (e.g. form or body or document) having it’s own event handler.

{{< highlight html "style=emacs" >}}

<form onclick="2ndEvent()"> [  
 This is a link!  
 ](#)  
 </form>   
{{< /highlight >}}

On clicking on the link in the above example code, first the hyperlink’s event will be handled, then form’s event will get handled, and at last body’s event will get handled. This is event bubbling, which bubble up from bottom to top.

<u>Event capturing</u> is opposite to event bubbling, where event handling execution starts from **top to bottom**.

If you have such type of architecture, where there are many event handlers for an event, you should not use *return false* or atleast use it with caution. It can get you in big trouble, as it does *preventDefault()* and *stopPropagation()* both and hence never allows further execution of an event.

## preventDefault()

It simply stops the default action of an element. Example, prevents the hyperlink from following the URL, prevents the submit button to submit the form. When you have many event handlers and you just want to prevent default event from occuring, just use *e.preventDefault()* in the top of the function definition. The reason we put *preventDefault()* in the first line of function is because, if something goes wrong in the code following the *preventDefault()*, then also it will not allow link or form to get submitted or do whatever action you want it to do. And hence the link or submit button will get submitted. It will still allow further propagation of the event.

Following example prevents the link from following the URL given in href attribute.  
{{< highlight html "style=emacs" >}}

<div> [Blah](http://ka.lpe.sh/) </div> <script type="text/javascript">
      $("div a").click(function(e){
  			e.preventDefault();
			});
     </script>  
   
{{< /highlight >}}

## stopPropagation()

{{< highlight html "style=emacs" >}}

<div onclick="doSomething()"> [Blah](#) </div>   
{{< /highlight >}}  
The above code has two event handlers for hyperlink. If you click on Blah, *doSomethingElse()* and then *doSomething()* will get fired.  
Now let’s say you want to stop the execution of div’s onclick function i.e. *doSomething()*, but you want the anchor tag’s onclick to fire when clicking on Blah, then use *stopPropagation()*.  
{{< highlight js "style=emacs" >}}$(“div a”).click(function (e) {  
 alert(‘Link is clicked! Sorry div will not get clicked..’);  
 e.stopPropagation();  
});{{< /highlight >}}

## stopImmediatePropagation()

If you have multiple event handlers for the event, and you want to stop all other event handlers and current event also from further executing, you should use *stopImmediatePropagation()*.  
{{< highlight html "style=emacs" >}}

<div> [Blah](#) </div> <script type="text/javascript">
      $("div a").click(function () {
         alert('Hello!');
      });</script>

 $("div a").click(function (e) { alert('Hi! You can see me'); e.stopImmediatePropagation(); });

 $("div a").click(function () { alert('I will never popup :('); });   
   
{{< /highlight >}}

So next time when you use *return false*, think twice do you really want return false or *e.preventDefault()* or other methods explained above will well-suited there.