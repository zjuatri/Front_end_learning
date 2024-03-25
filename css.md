## CSS flex
```css
display:flex 
```
![](flex.png)
### `flex-direction`
```css
 flex-direction:row
```
![](row.png)
```css
 flex-direction:row-reverse
```
![](row-reverse.png)
```css
 flex-direction:column
```
![](column.png)
```css
 flex-direction:column-reverse
```
![](column-reverse.png)
## `flex-basis`&`flex-grow`&`flex-shrink`
```css
.container{
    display:flex;
    width:500px;
}
.item{
    flex-basis:50px;
    /*flex-basis represents the width of the flex element
    if it is set to auto, it's the same as min-content, which equals to the length of the longest word in the text.
    you can also use width instead of flex-basis*/
    flex-grow:1;
}
.item:nth-child(1){
    flex-grow:6
}
/* 4(50+x)+50+6x=500 */
/*you can set flex-basis to 0 to make the width of the first child 6 times the others.*/
```
`flex-shrink` is the minus version of `flex-grow`  

`flex: grow shrink basis`  
```css
flex:initial;
/*flex: 0 1 auto*/
flex:auto;
/*flex: 1 1 auto*/
flex:none;
/*flex: 0 0 auto*/
flex:1 0px;
/*devide into equal parts*/
```
### `align-items`
manipulate cross axis
```css
.container{
    display:flex;
    width:500px;
    align-items:stretch
    /*'stretch is the 'default value, meaning stretching other elements'height to that of the highest element*/
}
```
```css
align-items:flex-start;
align-items:flex-end;
align-items:center;
align-items:baseline;
```
![](a_flex-start.png)
![](a_flex-end.png)
![](a_center.png)
![](a_baseline.png)
### `justify-content`
manipulate the main axis
```css
justify-content:flex-start
justify-content:flex-end
justify-content:center
justify-content:space-between
justify-content:space-around
justify-content:space-evenly
```
![](j_flex-start.png)
![](j_flex-end.png)
![](j_center.png)
![](j_space-between.png)
![](j_space-around.png)
![](j_space-evenly.png)