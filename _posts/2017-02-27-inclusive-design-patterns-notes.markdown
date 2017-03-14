---
layout: post
title:  "Notes on Inclusive Design Patterns"
date:   2017-02-27 21:18:16 -0800
categories: accessibility
---
#Inclusive Design Patterns
##Coding Accessibility Into Web Design

### Introduction

### The Document


- `lang=fr` tells browser which language document is written in.
- Allows `<textarea>` to switch dictionaries.
- It’s possible to add lang attribute to blockquotes for quotes in different languages
- Layout should not break when user zooms
- For best pinch-to-zoom...             

```
<!-- don’t use this -->
<meta name="viewport" content="width=device-width, initial- scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
                    
<!-- use this -->
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
```

- Setting font size to 100% will et font size to the default set by the user. Unaltered, this equals 16px
- Don't set fonts sizes with pixels
- To make sure font-size, padding, and margin resize proportionally, each should use relative units -- either `em` or `rem`.
- Line-height can be set without units: `line-height: 1.5` will make the line height 1.5 times larger than the font. This is the ideal proportion, and it will resize properly
- Write media queries in `em` units. Pixel units won't work with user-defined font sizes, and   `rem` units don't work well with Safari (check out zellwk.com/blog/media-query-units)
- Viewport units (`vh` and `vw`) cannot be scaled using full-page zoom. A good work-around: `html {font-size: calc(1em + 1vh);}`. Everything will scale relative to the viewport.
- The `<main id="main">` element offers a quick and reliable way for screen readers to jump to the main content of the page. 
- Handy print style to hide all page content except for the main content area: 

```
@media print {
    body > *:not(main) {
        display: none;
    }
}
```

- Skip links: When a keyboard user enters a new page, the document itself will be the first thing to receive focus. With the above provision in place, when the user hits their Tab key they’ll focus the first interactive element on the page: the skip link. Example:

```
[href=”#main”] {
    position: absolute;
    top: 0;
    right: 100%; /* moves off screen */
}
[href=”#main”]:focus { 
    right: auto;
}
```

- Putting it all together:

```
<!DOCTYPE html>
<!-- the main language of the page declared --> 
<html lang="en">
    <head>
        <meta charset="utf-8">
        
        <!-- a viewport declaration which does not disable zooming -->
        <meta name="viewport" content="width=device-width, initial- scale=1.0">
        
        <!-- a non-blocking base64-encoded font resource -->
        <link rel="stylesheet" href="fonts.css" media="none" onload="if(media!='all')media='all'">
        <noscript>
            <link rel="stylesheet" href="fonts.css">
        </noscript>
        
        <!-- a non-blocking stylesheet -->
        <link rel="stylesheet" href="main.css" media="none" onload="if(media!='all')media='all'">
        <noscript>
            <link rel="stylesheet" href="main.css">
        </noscript>
        
        <!-- a descriptive label for the page -->
        <title>Inclusive Design Template | Heydon's Site</title>
         
    </head>
    <body>

        <!-- a handy skip link for keyboard users --> 
        <a href="#main">skip to main content</a>

        <!-- logo / page navigation etc. goes here -->
        <main id="main">

            <!-- unique content of page goes here -->
    
        </main>

        <!-- a non-blocking javascript resource -->
        
        <script src="scripts.js"></script> 
    </body>
    
</html>
```

        
### A Paragraph

- Characters per line should fall between 45 and 75
- A paragraph 60rem wide with 1rem font-size has measure of 60.
- Improved + customizable link underlines (won't cross thru letters:

```
p a {
    text-decoration: none;
    text-shadow: 0.05em 0 0 #fff, -0.05em 0 0 #fff, 0 0.05em 0 #fff, 0 -0.05em 0 #fff, 0.1em 0 0 #fff,  -0.1em 0 0 #fff, 0 0.1em 0 #fff, 0 -0.1em 0 #fff;
    background-image: linear-gradient(to right, currentColor 0%, currentColor 100%);
    background-repeat: repeat-x; 
    background-position: bottom 0.05em center;
    background-size: 100% 0.05em;
}
```

- Improve a focused link -- remove barely perceivable outline and add background color (endorsed by GOV.UK):

```
p a:focus {
    outline: none;
    background-color: #cef;
    text-shadow: 0.05em 0 0 #cef, -0.05em 0 0 #cef, 0 0.05em 0 #cef, 0 -0.05em 0 #cef, 0.1em 0 0 #cef, -0.1em 0 0 #cef, 0 0.1em 0 #cef, 0 -0.1em 0 #cef;
}
```

- denote external links by placing an icon after the link: `[href^="http"]:not([href*="heydonworks.com"])::after { ... }`

### A Blog Post

- subtitles -- instead of h1 and h2 for title and subtitle, use this. It creates the best outline: `<h1>
How To Mark Up Blog Articles <span>In Seven Simple Steps
</span> </h1>`
- some semantic html5 elements such as `<article>` are not supported by any accessibility tool and therefore do not increase accessibility
- test structure of a page by turning off css and viewing the page -- it should still be navigable and usable
- test screen readers your self (NVDA for Windows, VoiceOver for Mac)


### Evaluation By Pattern

- SVG benefits from being scalable, small in file size and — unlike icon fonts — not breakable by user font preferences
- a button with a svg icon: 

```
<button data-action="upvote" aria-label="upvote"> 
    <svg>
        <use xlink:href="#upvote"></use> 
    </svg>
</button>
```

### Navigation Regions

- make it visually clear to users where they are relative to the main navigation
- cool tip to add a screen-reader-friendly "you are here" to a menu item: 

```
<nav> 
    <ul>
        <li><a href="/">home</a></li>
        <li><a href="/about"><span class="visually- hidden">Current page</span> about</a></li>
        ...
        <!-- OR, this: -->
        <li><a href="/about" aria-describedby="current">about</ a></li>
        ...
    ...
...

```

- another navigation tip for non-single page sites: have current menu item link to `#main` (`<li><a href="#main">about</a></li>`) 

-  The HTML5 hidden attribute is used to hide the description both visually and from screen readers. It works like display: none; but is syntactically neater. Despite being hidden, because it has a relationship to the link, the link still has access to “Current page” and it will be announced on focusing the link. (Note that Internet Explorer does not support hidden at the time of writing, but you can force it to by adding `[hidden] { display: none; }` to your style sheet.
- add ` <header role="banner">` to header that contains main nav 


### A Menu Button

- SVG sprites are fast becoming the de facto solution for icon rendering — and with good reason. As Google’s 305-byte logo implementation112 attests, they can make very small assets. They are scalable by nature and can even change color in accordance with changes to font color.
- SVG sprites work best cross-browser when they’re embedded in the page. This also eliminates a separate HTTP request. The following should appear directly inside the <body>:

```
<svg style="display: none;">
    <symbol id="navicon" viewBox="0 0 20 20">
        <path d="m0-0v4h20v-4h-20zm0 8v4h20v-4h-20zm0 8v4h20v- 4h-20z"/>
    </symbol> 
</svg>
```

- The <symbol> can be used within our menu button by refer- encing its id with a <use> element.

```
<button aria-label="menu">
    <svg>
        <use xlink:href="#navicon"></use>
    </svg>
</button>
```

- To make the icon adopt the color of the button element’s font — both with high contrast mode on or off — we can use CSS’s currentColor value and set it on the <path>’s fill prop- erty. SVG is clearly the most robust solution and already has very good support.

```
<svg style="display: none;">
    <symbol id="navicon" viewBox="0 0 20 20">
        <path d="m0-0v4h20v-4h-20zm0 8v4h20v-4h-20zm0 8v4h20v- 4h-20z" fill="currentColor" />
    </symbol> 
</svg>
```

- for instances when you want to display the button and not the 'menu' text, wrap 'menu' in a span with the 'visually-hidden' class
- Support for SVG is pretty much universal,117 with the stipulation that IE9–11 cannot reference external files using `xlink:href`
- IE SVG fallback:

```
<button aria-label="menu"> 
    <svg>
        <switch>
            <use xlink:href="#navicon"></use> 
            <foreignObject>
                <img src="path/to/navicon.png" alt="" />
            </foreignObject>
        </switch> 
    </svg>
</button>
```

### Inclusive Prototyping

### A List of Products

### A Filter Widget

- avoid infinite scrolling

### A Registration Form

### Test-Driven Markup

### Further Reading


### My Questions + Notes:
What are base64-encoded fonts, and how do you embed them into a stylesheet after the page loads (progressive enhancement)?
Why aren't we using rem/em's?
What are `<dd>` and `<dt>` elements?




