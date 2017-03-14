---
layout: post
title:  "Better SASS"
date:   2017-02-27 21:18:16 -0800
categories: sass css scss 
---
# Improving your SASS 



## Modularization
Modular SASS allows for more scalable, maintainable, and re-useable CSS.

## Adopting a Methodology
Styles shouldn't depend on HTML structure -- should be as 'flat' as possible. 
Bad: header nav .navbar {}
Good: .main-navbar {}
Better: [role=''] {}



## Adopt Coding Standards

Agree on some simple standards for each language you use. 


PHP: 

- Readability is more important than brevity or cleverness
- Indentation with tabs.


HTML:

- Don't add functionality like links or buttons inside a header tag 
- As with PHP, HTML indentation should always reflect logical structure. Use tabs and not spaces.

JS:

- Indentation with tabs.
- No whitespace at the end of line or on blank lines.
- Object declarations can be made on a single line if they are short

CSS: 

- Use tabs, not spaces, to indent each property.
- Add two blank lines between sections and one blank line between blocks in a section.
- Each selector should be on its own line, ending in either a comma or an opening curly brace. Property-value pairs should be on their own line, with one tab of indentation and an ending semicolon. The closing brace should be flush left, using the same level of indentation as the opening selector.
- Refrain from using over-qualified selectors, div.container can simply be stated as .container
- Line height should also be unit-less, unless necessary to be defined as a specific pixel value
- Avoid adding a unit on a zero value
- Commenting:

		/**
		* #.# Section title
		*
		* Description of section, whether or not it has media queries, etc.
		*/
		
		/* This is a comment about a selector */
		



WP coding standards
editorconfig.org

## Compiling
Source Maps
Auto-prefixer
Linting
Pixels to Ems via Gulp








### Sass maps

$ui-colors: (
    default : $fountain-blue;
    success : $emerald;
    error  : $sunglow;
    warning : $coral;
    info : $purple;
)
// Mixins

@mixin bg-colors($map) {
    @each $theme, $color in $map {
        &--#{$theme} {
            background-color: $color;
        }
    }
}

called:
.btn {
    @include bg-colors($ui-colors);
}

### nest maps:

Creating your custom CSS coding guideline:
1. Set goals
    
    - modular
    - not html dependent
    - easily reused within a project, or even, in other projects without extra dependancies
    - semantic
    - minimize contextual css -- css that's dependent on a parent. when styles are tightly coupled to the DOM will increase the chance of changes to the HTML breaking our layout. shallow', minimum nesting,
    - avoiding id selectors and using !important
    - maximize CSS reuse-ability both within a theme and with other themes
    - make projects easier to pass between developers. come up with guidelines / recommendations for CSS coding standards to encourage consistency without discouraging experimentation. Maybe come up with a list of best practices for devs to loosely follow. 
    - goal is not to have the cleanest, most minimalist markup, or 


2. While we're at it, let's define some coding standards -- let's loosely follow WP's coding standards

    - indentation char: space
    - css indentation: 2 spaces
    - php indentation: 4 spaces


##BEM 
*BEM naming conventions, SMACSS categorization conventions*
Block Element Modifier

Abstract our CSS styles into three distinct classes: block classes, element classes, modifier classes.

First, define the block -- the highest level of abstraction that contain child elements.

Modifiers can modify both blocks (.block--modifier) and elements (.block__element--modifier)

The double underscore and double hyphen allows us to clearly delimit each part of the BEM selector. 


class names convey information about the 
context is in the name of the selector


can be subjective. my idea of a module may be different than your idea of a module
blocks should be able to be used in other projects without dependancies


not everything needs to be defined with BEM naming convention -- only blocks that would be useful in another context. not necessary with blocks that are not reused

Benifit to lengthy class names: this type of class notation is expressive which helps other devs know what they mean / what is going on. can greatly assist in readabilty


.nav {
   &  
}

break something into a module / block only if it'd be useful in another context
communicate what a block of HTML does just from it's naming convention, and selectors are easier to understand because we provide the context directly into the selector
avoid nesting so styles are not html dependent. shallow. classes over ids. 
goal: to be able to apply styles independent of location
.block__element--modifier

The following will spit out child elements that are not dependent on the parent. 

```
.list {
    &__item{
        a {
        color: green;
        }
    
    }
    &__item--end{ 
    
    }
    &__item--current{
        a {
        color: black;
        }
    }
}

```

Mixin to make writing BEM selectors easier:

@mixin e($element) {
    &__#{$element} {
        @content;
    }
}

@mixin m($modifier) {
    &--#{$modifier} {
        @content;
    }
}

.list {
    @include e(item){
        a {
            color: green;
        }
        @include m(current){
            color: red;
        }   
    }
}

Placeholder selectors to make code DRYer. This helps clean up the html classes, too. Can reduce `.btn .btn--green .btn--active` to just the last class.

%nav-item-disp {

}
%nav-item-link {

}
%nav-item-on {
}


Use %btn to extend btn classes to btn elements. the placeholder will have the hover and focus states defined
%sro -- screen reader only class
.form {
    &__label{
        &--hidden {
            @extend .sro;
        }
    display: block;
    etc...
    }
}


###SMACSS Categorization:
Base, Layout, Module rules (reusable components), State Rules

Base styles -- no classes or id selectors. Stick to element selectors
Layout: header, footer, sidebar
Modules: sit inside a layout, can be reused other places, and have no parent dependancies
Directories in sass:
*each directory has index.scss that imports partials. Can use globbing.

Base:

-   h1,h2,h3,h4,h5,h6,p,a,body,*

Layout:

- .container, sidebar, header, footer, panel, main-content

Modules:

- buttons,extends, forms, headlines, icond, img, nav, navbar 
- no knowledge of parent container
- each partial represents a stand-alone module
- extends has all placeholders, important to keep them from getting obscured when working on teams

Utilites:

- mixins, functions, variables, 

## Questions 
Better to import WP google fonts via functions file, or style file?
