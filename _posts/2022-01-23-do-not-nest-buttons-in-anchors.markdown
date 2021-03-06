---
layout: post
title:  "Do not nest buttons in anchors!"
date:   2022-01-23 10:00:00 +0100
categories: general, html
description: "A while ago, I've read an interesting tutorial on Reddit. Creating quick icons by wrapping buttons in anchors. That sounded a bit weird."
tags: "blog, programming, code, html, best, practice "
---

# {{ page.title }}
Published: {{page.date | date: "%d-%m-%Y"}}


I love scrolling through Reddit and seeing all the people there trying to make our lives easier. Unfortunately, though, from time to time, it happens that people push information that is not only wrong but could lead to undesired behavior on your page. For example, as stated in this [reddit post](https://www.reddit.com/r/learnprogramming/comments/rmtysh/programming_trick_1_how_to_make_html_buttons_links/?utm_medium=android_app&utm_source=share), it would be pretty easy to make link buttons by wrapping \<button\>-tags with anchors.

<br>
Here lies a misconception on what these two tags are meant for. While I've read the tutorial, I had a gut feeling that this approach was wrong and lucky me, I could find a prove. The [HTML Specs Site](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-a-element) clearly states :

>Content model (A normative description of what content must be included as children and descendants of the element):
Transparent, but there **must be no interactive content descendant**, a element descendant, or descendant with the tabindex attribute specified.

<br>
To make it even clearer -  the site specifies interactive elements as *" content that is specifically intended for user interaction."* Those are: 
- a (if the href attribute is present)
- audio (if the controls attribute is present)
- button
- details
- embed
- iframe
- img (if the usemap attribute is present)
- input (if the type attribute is not in the Hidden state)
- label
- select
- textarea
- video (if the controls attribute is present)

<br>
An idea of why this nesting would lead to different problems lies in the underlying event order if a user clicks on such a nested construct. To get a better understanding, let me show an example: 

<p class="codepen" data-height="300" data-theme-id="dark" data-default-tab="result" data-slug-hash="OJOJNBY" data-preview="true" data-user="richardschuh" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/richardschuh/pen/OJOJNBY">
  Button Anchor Nesting</a> by RichardSchuh (<a href="https://codepen.io/richardschuh">@richardschuh</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

<br>
If a user clicks on this button, it will not lead to the linked page. Instead it deletes the form's input. In conclusion, the nested element's interactive function is executed. If this behavior is consistent across all web browsers, I wouldn't know. Anyway, you'd always have to keep in mind where your buttons and anchors are placed to avoid undesired results.

<br>
## A better approach

Use things for what they are meant to be used. For example, use anchors to link to content on your page or different sites. On the other hand, if you interact with forms, use button tags inside the form elements. That way, you keep the separation of concerns, and you can also keep your styling clear. If you insist on your anchors looking like buttons, consider using CSS. It takes you ten lines of code (or more - depending on what you want to achieve) to generate a simple button class that looks like the default button on Google Chrome on Windows:

<p class="codepen" data-height="300" data-theme-id="dark" data-default-tab="result" data-slug-hash="OJOJNKK" data-preview="true" data-user="richardschuh" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/richardschuh/pen/OJOJNKK">
  Button CSS</a> by RichardSchuh (<a href="https://codepen.io/richardschuh">@richardschuh</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>


<br>
## For the lazy - CSS Frameworks
If you don't feel like writing your own CSS, you can always use class-based frameworks like [Bootstrap](https://getbootstrap.com/), [TailWindCSS](https://tailwindcss.com/) or [MaterializeCSS](https://materializecss.com/). Those frameworks offer prewritten classes to style all your items. They come in handy if you work on a project that values functionality over esthetics. In such cases, you can style buttons and anchors persistently by adding a "btn"-class to both items, but you don't change or intermix their intended behavior. 