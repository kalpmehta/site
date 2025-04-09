---
id: 687
title: 'Prototype Utility Methods &#8211; Commonly used prototypejs functions'
date: '2013-06-03T11:33:13+00:00'
author: kalpesh
layout: post
tags:
    - 'Prototype JS'
tags:
    - prototypejs
---

![Prototype JS Javascript framework](http://ka.lpe.sh/uploads/2013/06/prototype_logo.gif)Prototype JS comes with many utility methods which are very powerful and useful while development. Below methods are shorthands or aliases of other Prototype methods, created to save time in typing.

These are created as they are very commonly used, to make developer’s life easier.

## $() Function

– Retuns the element that has the ID passed as an argument  
*Shorthand to*: document.getElementById()  
Example:  
{{< highlight js "style=emacs" >}}  
$(“car”); //returns element having id “car”  
$(“car”).hide(); //hides div where id is “car”  
$(“car”).addClassName(“hidden”); //adds class name “hidden” to element with id “car”  
{{< /highlight >}}

## $$() Function

– Returns the elements that has CSS selectors as an argument  
*Shorthand to*: document.getElementById() + document.getElementsByTagName() + prototype’s getElementsByClassName()  
Example:  
{{< highlight js "style=emacs" >}}  
$$(‘.active’);//returns all the elements having class “active”  
$$(‘div.active p, #car a’).invoke(‘hide’); //hides all the “p” tags under div having class “active”, hides all links under element having id “car”  
$$(‘div:empty’); //all divs without any content, version 1.5.1 and above  
{{< /highlight >}}

## $F() Function

– Returns the value of a form control, like text boxes or dropdown options  
*Shorthand to*: Form.Element.getValue, Form.Element#getValue  
{{< highlight html "style=emacs" >}}  
<script type="text/javascript">
	function showName() {
		var name = $F('firstname') + ' ' + $F('lastname');
		alert('Name: ' + name);
	}
</script>

<form> <input id="firstname" type="text" value="Kalpesh"></input>  
 <input id="lastname" type="text" value="Mehta"></input>  
 <input onclick="showName();" type="button" value="Get my Name!"></input>  
</form>{{< /highlight >}}

## $R() Function

– Builds a range object, shorthand to “new ObjectRange()”  
*Shorthand to*: ObjectRange()  
Example:  
{{< highlight js "style=emacs" >}}  
var range = $R(10, 20, false);  
range.each(function(value, index){  
 alert(value);  
});  
{{< /highlight >}}

## $H() Function

– Converts objects into enumerable Hash objects which resembles associate arrays.  
*Shorthand to*: Hash  
{{< highlight js "style=emacs" >}}  
var a = {  
 firstname: ‘John’,  
 lastname: ‘Doe’  
};

var h = $H(a);  
alert( h.get(‘firstname’) ); //alert’s John  
{{< /highlight >}}

## $A() Function

– Converts the single argument passed into an Array object.  
*Shorthand to*: Array.from  
{{< highlight js "style=emacs" >}}  
var paras = $A(document.getElementsByTagName(‘p’)); //gets all the paragraph’s in array format  
paras.each(Element.hide); //looping paragraphs and hiding them each  
$(paras.last()).show(); //showing the last paragraph  
{{< /highlight >}}

## $w() Function

– Splits a string into an array with whitespace as a delimiter.  
*Shorthand to*: Ruby’s %w{foo bar} or Perl’s qw(foo bar).  
{{< highlight js "style=emacs" >}}  
var str = ‘apples bananas kiwis’;  
$w(str).each(function(fruit){  
 alert(fruit); //alerts 3 times with values apples, bananas and kiwis  
})  
{{< /highlight >}}