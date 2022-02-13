# *Problem*
> How to Edit and Delete Unwanted Element in Webpage, So that We can Easily Make ScreenShot or Take Print of the Content as we want

---
# _Solution_
> Try _**PrintCut v0.1**,_ PrintCut, We can Easily Edit, Resize , Delete and Text or Block in WebPage

___

> # Steps for Use

> 1. Copy the Below Script
> 1. Paste in the Console of Browser (shortcut key in Chrome for Opening Console) (Ctrl + Shift + J) and Press Enter
> 1. Move the Mouse at the Above of the Element which you want to remove
> 1. Press **x** key in keyboard to **Delete** that Element 
> 1. Press **e** key in keyboard to **Edit** that Element 
> 1. Press **r** key in keyboard to **Resize** that Element 
> 1. Take Print out of the Page, which contains no Ads or unwanted Element in Print Out
---
---
# Code
```js
(() => {
  document.body.innerHTML += `<style>.resizable{border:2px dotted #4286f4; outline:none;background:rgba(0,0,0,0.2);}.resizable[contenteditable="true"]{border:2px solid red;}.resizable .resizers{box-sizing:border-box;position:absolute;top:0;left:0;width:100%;height:100%}.resizable .resizers .resizer{width:10px;height:10px;border-radius:50%;background:#fff;border:3px solid #4286f4;position:absolute}.resizable .resizers .resizer.top-left{left:-5px;top:-5px;cursor:nwse-resize}.resizable .resizers .resizer.top-right{right:-5px;top:-5px;cursor:nesw-resize}.resizable .resizers .resizer.bottom-left{left:-5px;bottom:-5px;cursor:nesw-resize}.resizable .resizers .resizer.bottom-right{right:-5px;bottom:-5px;cursor:nwse-resize}</style>`;
function makeResizableDiv(div) {const element = div;const resizers = div.querySelectorAll(".resizer");const minimum_size = 20;let original_width = 0;let original_height = 0;let original_x = 0;let original_y = 0;let original_mouse_x = 0;let original_mouse_y = 0;for (let i = 0; i < resizers.length; i++) {const currentResizer = resizers[i];currentResizer.addEventListener("mousedown", function (e) {e.preventDefault();original_width = parseFloat(getComputedStyle(element, null).getPropertyValue("width").replace("px", ""));original_height = parseFloat(getComputedStyle(element, null).getPropertyValue("height").replace("px", ""));original_x = element.getBoundingClientRect().left;original_y = element.getBoundingClientRect().top;original_mouse_x = e.pageX;original_mouse_y = e.pageY;window.addEventListener("mousemove", resize);window.addEventListener("mouseup", stopResize);});function resize(e) {if (currentResizer.classList.contains("bottom-right")) {const width = original_width + (e.pageX - original_mouse_x);const height = original_height + (e.pageY - original_mouse_y);if (width > minimum_size) {element.style.width = width + "px";}if (height > minimum_size) {element.style.height = height + "px";}}}function stopResize() {window.removeEventListener("mousemove", resize);}}}let nowEle = null;let flagNotJump = false;const removeResizer = (target) => {let re = target?.querySelector(".resizers");if (re) {re.remove();}};const addResizer = (target) => {if (!flagNotJump) {flagNotJump = true;let addThis = `<div id="x0001" class='resizers'><div id="x0001" class='resizer bottom-right'></div></div>`;target.innerHTML = addThis + target.innerHTML;makeResizableDiv(target);let _p = target.style.position;target.style.position = "relative";target._p = _p;} else {removeResizer(target);let newClass = target.className.split(" ").filter((e) => e !== "resizable").join(" ");target.className = newClass;target.style.position = target._p;flagNotJump = false;}};const editMode = (target,p)=>{target.contentEditable =p.edit};document.addEventListener("mouseover", (e) => {let target = e.target;if (target.id !== "x0001" && !flagNotJump) {
  target.className += " resizable";nowEle = target;}});document.addEventListener("mouseout", (e) => {let target = e.target;if (target.id !== "x0001" && !flagNotJump) {let newClass = target.className.split(" ").filter((e) => e !== "resizable").join(" ");target.className = newClass;editMode(nowEle, {edit:"false"});
nowEle = null;}});document.addEventListener("keyup", (e) => {if (nowEle)switch (e.key) {case "x":nowEle.remove();break;case "r":addResizer(nowEle);break;case "e":editMode(nowEle,{edit:"true"});break;}});})();

```

