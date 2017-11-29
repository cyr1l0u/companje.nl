---
title: =====CSS=====
---

nog lezen: https://www.mozilla.org/en-US/developer/css-grid/


==width/height of viewport==
<code css>
img {
  width: 50vw;
  height: 50vh;
  /*object-fit: cover; */
}
</code>
==web==
see [[web]]


==css tricks==
* http://css-tricks.com/snippets/html/base64-encode-of-1x1px-transparent-gif/

==flexbox==
* http://css-tricks.com/snippets/css/a-guide-to-flexbox/

==use css3 features if supported==
<code javascript>
var css3_support = (document.createElement("detect").style.objectFit === ""); //'objectFit' or other css3 tag
document.getElementsByTagName("html")[0].className += (css3_support ? " css3" : " nocss3");
</code>

<code css>
.css3 img { 
  /* css3 support */
}
.nocss3 img {
  /* no css3 support */
}
img {
  /* always */
}
</code>

==css names in javascript==
"background-color" becomes "backgroundColor", and "list-style-type" becomes "listStyleType"

==detect css3==
* http://www.sitepoint.com/detect-css3-property-browser-support/

==initial==
  h1 {
    color: initial; 
  }

==Foundation==
* http://foundation.zurb.com/index.html
* [[http://foundation.zurb.com/learn/video-started-with-foundation.html|video]]

==Goed boek==
(tip van Peter): http://www.cssmastery.com/

==Center==
*http://bluerobot.com/web/css/center1.html
*http://css-discuss.incutio.com/wiki/Centering_Block_Element
*http://dorward.me.uk/www/centre/

==attribute selectors==
* http://css-tricks.com/attribute-selectors/
<code css>
td[bgcolor="#00ffff"] {
	border:5px solid green;
}
</code>

==input type text==
<code css>
input[type="text"] 
</code>

==multiple columns==
<code css>
.template-front-page .intro {
	-moz-column-count:2; /* Firefox */
	-webkit-column-count:2; /* Safari and Chrome */
	column-count:2;
	-moz-column-gap:40px; /* Firefox */
	-webkit-column-gap:40px; /* Safari and Chrome */
	column-gap:40px;
	text-align: justify;
}
</code>

==position:relative==
* http://jsfiddle.net/DsTeK/2/

==style only children not descendants==
<code css>
li.page_item.current_page_item > a {
}
</code>

==center div's vertically==
<code css>
.className{
	position:absolute;
	left:50%;
	top:50%;
	width:400px;
	height:300px;
	margin-top:-150px;
	margin-left:-200px;
}
</code>
[[http://demo.tutorialzine.com/2010/03/centering-div-vertically-and-horizontally/demo.html|source]]