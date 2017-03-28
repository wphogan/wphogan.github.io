---
layout: post
title: Notes on Accessibility
---
## Treehouse course


It's important to get familiar with how accessibility tools work. You may never truly understand how an assistive-tech user uses these tool but it's important to know of their features. Try switch access on your smart phone. Spend time learning how to use Voice Over, etc. Switch controls can be set to a bluetooth controller, or a motion-sensing camera that looks for head movements. 

NVDA: Window's built-in, and free, screen reader
nvda.org. It'll read text that you point to. 

Voice Over: Mac's built-in, and free, screen reader. 
Activate: Command + F5, then walk thru the tutorial

### WCAG 2.0

WCAG Principle 1: Content should be perceivable
WCAG Principle 2: Content should be operable. All functionality should be navigate-able with the keyboard.

User must have enough time to digest the content. Pause button on slider, videos, audio, etc. 

Don't create content that causes seizures. 

Heading text must describe and give more information about the content displayed (ie, no fancy or cryptic headers). Links  should make purpose clear. Avoid "click here". 

Web content needs to be understandable. 

- Must be readable
- Webpage should not change focus on it's own
- Input elements should have sufficient info. If input is rejected, make sure error is readable and accessible.

Web content must be compatible

- HTML must be complete. No stray tags, typos, etc.
- Checkboxes must be usable (custom checkboxes may not be)
- Stick with default syntax


[WCAG checklist](http://webaim.org/standards/wcag/checklist)! Great resource for all the levels of support and their corresponding success criteria. 

[Filterable and shareable WCAG checklist](https://www.w3.org/WAI/WCAG20/quickref/). This one has a sidebar can be filtered by the three levels (A, AA, and AAA). It also provides a shareable link to get an entire dev team on the same page for a given project.


### Section 508 compliance

Specific to the US
section508.gov


### Semantic HTML

- Choose the right tags, avoid "div soup"
- Alternatives to divs:
	- header (can have multiple -- can be used on post feeds)
	- footer
	- article 
	- section
	- nav
	- main (just one!)
	- button
	- look up more
	- aside
	- form

	
### ARIA: Accessible Rich Internet Apps

4 ARIA Roles:

1. Landmark
2. Document
3. Widget
4. Abstract

Landmark roles:

- banner (applied to the header)
- navigation
	- when multiple navigations, use  aria-label to differentiate: `aria-label="mainnav"` and `aria-label="pagenav"`
- main
- complementary (supports main content
- contentinfo (meta data of the site in the footer eg copyright)
- form (note: this is not needed on form elements)
- search (applied to a search bar form)
- application (don't use unless you know what you're doing

Use ARIA sparingly. 

Idea: print and format a [cheatsheet of ARIA roles](http://karlgroves-sandbox.com/CheatSheets/ARIA-Cheatsheet.html) and stick it next to my monitor.

Site should make sense with no javascript or css. This means HTML and content must be in the proper order.

Avoid "Click here" in favor for "Download PDF", or something more descriptive.

Alt text -- do it!
Idea: make it required field for WordPress media uploads.

Links, buttons, and inputs have "focus". This allows user interaction via the keyboard.

For other elements, you need to apply a tab index. A tab index of -1 will take it out of the normal flow of tabs and give it "programmatic focus". This is essential to modals and popups. Divs can't normally receive focus, but with `tabindex="-1"`, it can. A tabindex of 0 will give the element focus based on it's position in the html. A positive tab index will change the order -- starting with the lowest index first. 

[WebAIM.org](http://webaim.org/) is a good resource to learn more about appropriate tab indexing. 

### Forms: 

- Include labels for input fields.
- Labels should have "for" tag that match the id of the input field
- Alternately, we could wrap the input field with a label and that foregoes the need for the "for" tag.

### Accessible UI & Design

Colorsafe.co -- will help choose color combos that create enough contrast. 

### Responsive Design:

Pixels are not good for accessibility
Relative units are better!
Em -- width of the capital 'M' in the given typeface
Rems -- aways based on the root font size. 
Percentage based on parent element
VW, Vh based on viewport
Vmin: selects whichever is smaller -- Vw or Vh
Vmax: select whichever is larger -- Vw or Vh
Viewport units not yet fully supported in all browsers

```
h1 {
	font-size: 4vw;
}
```

### Manual Testing for Accessibility:

Tab thru the site
Use assistive tech, like a screen reader or switch controls
User testing, include different types of users 

### Automatic testing:  

Gulp has an accessibility audit plugin!! 

### Online tools: 

Contrast color checker: spectrum chrome plugin. View the page with various filters.
Chrome Accessibility Audit plugin -- will run series of test and note if they pass or fail
BBC Mobile Accessibility Guidelines -- nicely labeled and organized

----

### Outstanding questions and to-dos:

Research Skeleton CSS boilerplate