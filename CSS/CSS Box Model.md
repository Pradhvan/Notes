# CSS Box Model


* In the box model the elements are generally displayed in a box. So every element has a display value , depending on what type of element it is. Default is block and inline.

* The inline element take only the space that is needed for it's element.
eg: a,span or images 

* The block element forms a seprate block and takes the full width available based on it's parent element and creates a new line before and after the element. 
eg: divs,p,h or list 

## Pading  
* seprating the content from the surrounding area,creates space inside the box.
* The padding of content happens in a clockwise manner i.e top , right , bottom, left. 
```css 
padding: 100px,120px,100px,120px; 
```
* If it has only two values it will be top - bottom and left - right. 

* If three the standard clockwise rule will follow.

* If % is used instead of px the padding becomes fluid as it adjusts to the width of the parent container.

*example:*
```html 
<div class ="test"></div>
```
```css
.test {
  padding: 100% 150%
}
```
* Here the padding ajusts to the width(breadth) of the container div. 

## Border: 
* Acts as an outline to the box and are optional. 
* It generally has three property border-width , border-style, border-color. 
* A shorthand boder takes cares all of them if you don't want to mention them seprately. 

```css
boder-width: 10px,20px;
border-style: solid ;
border-color: red 
```
* The border property also follows the clowise rule. 

* Given below is the shorthand for the above css. 
* Both the shorthand and the normal property can be used simultaneously is needed. 

```css
border: 10px solid red;
```

**Margin:** 
* Space around the element that seprates it from other elements,creates space outside the box.

* Follows the clockwise rule. 
* We can use negative values which overlaps the box which side negative value is used either left,right,top or bottom. 
* Magin has a property auto which autmatically calculates the centre of the page and sets the element in the centre. 

```css
margin: 105px 0 -50px;
```
