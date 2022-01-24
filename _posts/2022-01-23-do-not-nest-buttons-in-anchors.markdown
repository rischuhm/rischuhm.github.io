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

<iframe frameborder="0" width="100%" height="500px" src="https://replit.com/@rischuhm/Button-Anchor-Test"></iframe>


If a user would click on this button, it would not lead me to my page but delete the form's input. I can say that the inner logic would preferably be executed from testing in Chrome. If this behavior is consistent across browsers, I wouldn't know. Anyway, you'd always have to keep in mind where your buttons and anchors are placed to avoid undesired results - like submitting or deleting form inputs. 

<br>
## A better approach

Use things for what they are meant to be used. For example, use anchors to link to content on your page or different sites. On the other hand, if you interact with forms, use button tags inside the form elements. That way, you keep the separation of concerns, and you can also keep your styling clear. If you insist on your anchors looking like buttons, consider using CSS. It takes you ten lines of code (or more - depending on what you want to achieve) to generate a simple button class that looks like the default button on Google Chrome on Windows:

```
<style>
.btn{
font-family: sans-serif;
font-size: small;
border: 1px solid rgb(118, 118, 118);
border-radius: 3px;
padding: 2px 6px;
margin:2px;
background-color:  rgb(239, 239, 239);
cursor: context-menu;
}

.btn:hover{
background-color: rgb(212, 212, 212);
}
</style>

<body>
<a class="btn">Button</a>
</body>
```

<br>
## For the lazy - CSS Frameworks
If you don't feel like writing your own CSS, you can always use class-based frameworks like [Bootstrap](https://getbootstrap.com/), [TailWindCSS](https://tailwindcss.com/) or [MaterializeCSS](https://materializecss.com/). Those frameworks offer prewritten classes to style all your items. They come in handy if you work on a project that values functionality over esthetics. In such cases, you can style buttons and anchors persistently by adding a "btn"-class to both items, but you don't change or intermix their intended behavior. 