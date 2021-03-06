- [W3C: CSSOM View Module](http://www.w3.org/TR/cssom-view/)
- [QuirksMode: W3C DOM Compatibility - CSS Object Model View](http://www.quirksmode.org/dom/w3c_cssom.html#elementview)
- [The CSSOM View Module](http://www.quirksmode.org/blog/archives/2008/02/the_cssom_view.html)
- [getBoundingClientRect is Awesome](http://ejohn.org/blog/getboundingclientrect-is-awesome/)


There are 4 kinds of measurement (left/top/width/height):

- x.offset* : `top,left` -> offsetParent, `width/height` -> border edge (including border)
- x.client* : `top,left` -> border width, `width/height` -> content field
- x.scroll* : `top.left` -> hidden parts, `width/height` -> content field, including hidden parts
- x.style.* : style.left, style.top,style.width,style.height will affect above values

Element Interface:
```c++
partial interface Element {
  ClientRectList getClientRects();
  ClientRect getBoundingClientRect();

  // scrolling
  void scrollIntoView(optional boolean top);
           attribute long scrollTop;   // scroll on setting
           attribute long scrollLeft;  // scroll on setting
  readonly attribute long scrollWidth;
  readonly attribute long scrollHeight;

  readonly attribute long clientTop;
  readonly attribute long clientLeft;
  readonly attribute long clientWidth;
  readonly attribute long clientHeight;
};
```

HTMLElement Interface:
```c++
partial interface HTMLElement {
  readonly attribute Element? offsetParent;
  readonly attribute double offsetTop;
  readonly attribute double offsetLeft;
  readonly attribute double offsetWidth;
  readonly attribute double offsetHeight;
};
```

Only `scrollTop` and `scrollLeft` is writable, when it's assigned a new value, it scroll the content and change scroll bar position.
**To make animation**, you change `element.style.left/top/width/height/margin/padding/...` 


ElementView properties
======================

> The `clientTop`, `clientLeft`, `clientWidth`, and `clientHeight` attributes must return zero if the element does not have any associated CSS layout box or if the CSS layout box is **inline**

[clientLeft and clientTop](http://www.w3.org/TR/cssom-view/#dom-element-clienttop)
------------------------
The position of the upper left corner of the content field relative to the upper left corner of the entire element (including borders) 

[element.clientLeft](https://developer.mozilla.org/en-US/docs/Web/API/element.clientLeft?redirectlocale=en-US&redirectslug=DOM%2Felement.clientLeft)

> **`The width of the left border of an element in pixels.`** It includes the width of the vertical scrollbar if the text direction of the element is right–to–left and if there is an overflow causing a left vertical scrollbar to be rendered. clientLeft does not include the left margin or the left padding. clientLeft is read-only.

[element.clientTop](https://developer.mozilla.org/en-US/docs/Web/API/element.clientTop?redirectlocale=en-US&redirectslug=DOM%2Felement.clientTop)

> **`The width of the top border of an element in pixels.`** It does not include the top margin or padding. clientTop is read-only.

[clientWidth and clientHeight](http://www.w3.org/TR/cssom-view/#dom-element-clientwidth)
----------------------------
The width and height of the content field, `excluding border and scrollbar`, but including `padding`

> padding edges surrounded field

<hr/>

offsetLeft and offsetTop
------------------------
The left and top position of the element relative to its `offsetParent`. 

[offsetParent](https://developer.mozilla.org/en-US/docs/Web/API/element.offsetParent?redirectlocale=en-US&redirectslug=DOM%2Felement.offsetParent)
------------
The ancestor element relative to which the offsetLeft/Top are calculated. 

> `offsetParent` returns a reference to the object which is the closest (nearest in the containment hierarchy) positioned containing element. If the element is non-positioned, the nearest table cell or root element (html in standards compliant mode; body in quirks rendering mode) is the offsetParent. `offsetParent returns null when the element has style.display set to "none"`. The offsetParent is useful because offsetTop and offsetLeft are relative to its `padding edge`.

offsetWidth and offsetHeight
----------------------------
The width and height of the entire element, `including borders`

> `clientWidth/Height` - padding edge.

> `offsetWidth/Height` - border edge.

<hr/>

[scrollLeft and scrollTop](http://www.w3.org/TR/cssom-view/#dom-element-scrolltop)
------------------------
The amount of pixels the element has scrolled. **`Read/write`**. 

> hidden part dimension

scrollWidth and scrollHeight
----------------------------
The width and height of the entire content field, including those parts that are currently hidden.
If there's no hidden content it should be equal to clientX/Y. 

> whole size of elements

WindowView properties
=====================

innerWidth and innerHeight
--------------------------
The dimensions of the `viewport` (interior of the browser window) 

outerWidth and outerHeight
--------------------------
The dimensions of the `entire browser window` (including taskbars and such) 

pageXOffset and pageYOffset
---------------------------
The amount of pixels the entire pages has been scrolled 

screenX and screenY
-------------------
The position of the browser window on the screen


<hr/>

[jQuery.fn.position](http://jqapi.com/#p=position)
------------------
Get the current coordinates of the first element in the set of matched elements, relative to the `offset parent`.

[jQuery.fn.offset](http://jqapi.com/#p=offset)
----------------
Get the current coordinates of the first element, or set the coordinates of every element, in the set of matched elements, relative to the document.
