# Basic Selectors 

## Type Selector 

## ID Selector 
* Id's carry more weight than the class as they target something in particular. 
* So if an element has both class and an ID , the ID will override the class.

## Class Selector 

* Class selecors are not unique and can be reused. 
* They start with the "."
* Target only that match the class atribute.
* An element can have multiple classes. 
* **Pseudo classes** are not explitly defined and does not appear in the source code, mainly used to target elements based on the user interaction.
eg: A website might have a particular link turned to diffrent color when it's been visited by the user. 

*HTML example:*
```HTML
<div class = "primary-content t-border"></div>
<header id = "top" class = "main-border"></header>
``` 
*CSS Example:* 
```CSS
.t-border {
  border: 3px solid red;
}
```
## Decendent Selector 

* It targets a particluar element that is the decendent(inside) the other element. 
* It requires two selectors seprated by a space. 
* It works for a particluar element inside a class too. 

*HTML example:*
```HTML
<header id = top>
    <span>Hello world !<span>
<header>
```
*CSS Example:* 
```css
header span {
  color: white 
  font-size: 30px 
}
```