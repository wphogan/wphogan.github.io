---
layout: post
title:  "4 Ways to Improve Your SASS"
date:   2017-02-27 21:18:16 -0800
categories: sass css scss 
---

## 1. Adopt a Methodology

The sooner you can choose (and stick to) a SASS methodology in your web development career, the better. It'll make your styles more maintainable, easier to read, easier to pass to other developers, and your future self will thank you. 

There are a bunch of SASS methodologies out there and, at their core, they follow basic CSS best-practices. Two of the most popular methodologies are BEM and SMACSS. After trying both BEM and SMACSS, I've developed my personal blend of the two -- BEM naming conventions mixed with SMACSS modularization and categorization of partials. Here are some links I found helpful:

1. [Intro to BEM and SMACSS](https://www.sitepoint.com/bem-smacss-advice-from-developers/)
2. [Meaningful CSS] (https://alistapart.com/article/meaningful-css-style-like-you-mean-it)
3. [BEM 101](https://css-tricks.com/bem-101/)


### Notes on BEM

__B__lock __E__lement __M__odifier

`.block__element--modifier`

Abstract your CSS styles into three distinct classes: block classes, element classes, modifier classes.

First, define the block -- the highest level of abstraction that contain child elements.

Modifiers can modify both blocks (.block--modifier) and elements (.block__element--modifier)

The double underscore and double hyphen allows us to clearly delimit each part of the BEM selector. 

Class names are expressive -- they convey information about their context and how they're used. This helps other developers know what's going on, and it can greatly assist in code readability.

Naming can be subjective. My idea of a module may be different than your idea of a module, but the principle should remain the same -- blocks should have no HTML dependancies. Goal: to be able reuse blocks and apply styles independent of location.

Not everything needs to be defined with BEM naming convention -- only blocks that would be useful in another context. 

Other BEM practices (and general CSS best-practices): 

 - avoid nesting so styles are not HTML dependent
 - keep selectors "shallow"
 - use element selectors, meta-field selectors, and classes over ids
 - avoid `!important`


With SASS 3.0+, The following will spit out child elements that are not dependent on the parent. 

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

```
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
```

## 2. Modularization and DRY code

Instead of writing all your SASS in a single, overflowing file, break up the code into smaller, more maintainable chunks. These smaller chunks are called _partials_ and here's my current preferred method to organizing them:

### SMACSS-inspired Categories for Partials*:

**Note: these are not the official SMACSS categories. I've adjusted them to meet my needs building WordPress themes.*

- Base
- Templates
- Modules (reusable components)
- Vendor
- States

__Base__: No class or ID selectors. Stick to element selectors. Includes any utilities such as partials, variables, and mixins. 

- ` h1, h2, h3, h4, h5, h6, p, a, body, html, blockquote, *`, etc.

__Layout__: header, footer, sidebar, etc. 

- `.container, sidebar, header, footer, panel, main-content`, etc.

__Modules__: sit inside a layout, can be reused other places and have no parent dependancies

- `buttons, extends, forms, headlines, icons, img, nav, navbar`, etc. 
- each partial represents a stand-alone module

__Vendor__: styles from third-parties

__States__: styles that affect a module's state (e.g. `.is-hidden, .is-red`, etc.)

Each directory has `index.scss` that imports the partials with in that directory. Each partial has it's own corresponding media queries.

### DRY SASS

[DRYing Out Your SASS Mixins](https://alistapart.com/article/dry-ing-out-your-sass-mixins)

Use placeholder selectors to make code DRYer. This helps clean up the html classes, too. Can reduce `.btn .btn--green .btn--active` to just the last class. The placeholder will have the hover and focus states defined.

```
%nav-item-disp {
 ...
}
%nav-item-link {
 ...
}
%nav-item-on {
 ...
}
%screen-reader-only {
 ...
}
```

## 3. Adopt Coding Standards

Agree on some simple standards for each language you use. Here's a slimmed down version of  WordPress's core-contributor coding standards.

This will make your code easier to maintain, read, debug, etc, and it's essential if you're working on a team.


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
        



## 4. Leverage Task-runner Tools

These are some Gulp plugins that will take your SASS to the next level. They're also available for Grunt.

 - [Source Maps](https://www.npmjs.com/package/gulp-sourcemaps)
 - [Auto-prefixer](https://www.npmjs.com/package/gulp-autoprefixer)
 - [SASS Linting](https://www.npmjs.com/package/gulp-sass-lint)
 - [Pixels to Ems](https://www.npmjs.com/package/gulp-pixrem)