# Values and Units 

* CSS pixels depends "**px**" on the pixel density of the viewing device , it varies from display to display.
* One display might be a sandard display and other might be a high density display in this display thus the pixel rescales providing the consitency among all display screens. 
* Percentage element "**%**" is relative to it's parents length(breadth) i.e they can adjust it's value according to it's parent's value. 
* **em** is equal to it's font size value of it's parent value.

* The default font-size for most of the browsers is 16px, 1em = 16px.
* To convert the px into em we need to do desired element pixel value by the parent element font size value(16).
eg: Title has a font-size: 26px = 26/16 = 1.625em

*Example*
```css
body{
  color: #878787; 
  margin: 0;
  font-size: 1em;
}

.main-header{
  color: #878787; 
  margin: 0;
  font-size: 3em;
}

.title{
  color: white;
  font-size : 1.625em; 
}

```
In the above example a compund effect takes place as each fount size inherits from the above thus increasing the the font-size each time. This is called the **compund effect**.

A quick work around to the effect is the **rem** element (root-element) which has no effect of inheritance thus no compund effect takes place. 

* If the font name has multiple letters it should be inclosed in the **" "**. 

* **vh** viewport height , helps in sizing puerly on the size of the view port. 
* 1 vh = 1% height of the view port. 
* You can calucuate the vh with the help of the calc() function.
```css
.wrap{
  min-width: calc(100vh-89px)
}
``` 
