---
layout: post
title: Learning 100 things in 100 days
categories: learning
---
## Goal: learn at least one thing related to WordPress or building websites everyday for the next 100 days and document it here.

### March

__March, 14 2017:__ Three levels of [WCAG](https://www.w3.org/WAI/intro/wcag) 
    
- Level A: impacts a very large number of users. This is typically the bare minimum requirements for calling a site "accessible". Includes providing a text based alternative to non-text content like images, and being able to navigate a site with a keyboard.
- Level AA: impacts less users than Level A. You should be hitting all these, too. Includes writing headings and labels describing the relevant content.
- Level AAA: even more specific. Not applicable to every project. Includes providing accessible alternatives to live, audio-only content. 
    
- tags: `accessibility`

__March, 15 2017:__ PHP Output Buffers are awesome

- PHP output buffer prevents functions from echoing data. For example, the following WordPress code will echo the ID only once:

		ob_start();
		the_ID();
		$id = ob_get_clean();
 	  	echo $id;  
 	  	
- Main PHP output buffer functions:
	- `ob_start();` 	starts the buffer
	- `ob_get_contents();` returns the contents of the buffer and allows it to keep running and collecting data
	- `ob_clean();` clears the buffer
	- `ob_end_clean();` stops and clears the buffer
	- `ob_get_clean();` fetches the contents of the buffer, clears the buffer, and stops the buffer
- Why is this awesome? Because it allows us to generate a lot of raw HTML without having to use quotes or other work arounds.  
	
		add_shortcode(
		    'our_fake_shortcode',
		    'fake_shortcode_function'
		);
		
		function fake_shortcode_function() {
		    ob_start();
		    echo 'REPLACED THAT SHORTCODE!!';
		    include 'path/to/your/template.php';
		    return ob_get_clean();
		} 
	
- Example template.php: 
	
		<p class="fake-template-class">This post was titled: <?php the_title(); ?></p>
		<?php custom_html_drawing_function(); ?>
	
- [link](https://wpshout.com/understanding-php-output-buffering-and-why-its-great-for-shortcodes/), tags: `php` `wordpress`

__March, 16 2017:__

- When merging a feature branch to a master branch that is ahead by a commit or two, the merge requires an extra commit of the master into the feature. This can make the git history somewhat messy and hard to understand. 
- As an alternative to git merging, you can rebase the feature branch onto master branch using the following commands:

		git checkout feature
		git rebase master
		
- Rebasing, compared to merging, makes for a cleaner, linear git history which is easy for other devs to understand. 
- `git rebase -i master` will allow you to interact with the commits. With this, you can squash minor commits into larger commits by changing them to `fixup`, further cleaning up the git history and making it easier to understand.
- Make sure to follow the "Golden Rules of Rebasing"
- [link](https://www.atlassian.com/git/tutorials/merging-vs-rebasing), tags: `temp`

__March, 17 2017:__

- Forever ignore .DS_Store from git repos!

		$ git config --global core.excludesfile ~/.gitignore
		$ echo .DS_Store >> ~/.gitignore
		
- tags: `git`

__March, 18 2017:__ Notes from [CSS for Grownups](https://www.youtube.com/watch?v=ZpFdyfs03Ug) talk

##### How to create a maintainable code base:

- __components__ -- should be able to build a component and forget about it. Place it and expect it to work. This is how manage complex systems -- modularize.
- We need to build our own constraints into CSS. Think about how we structure, organize, architect code.
- Code quality:

  - performant
  - correctness
  - web 2.0 compliant & wcag compliant
  - extensible
  - reliable
  - reusable
  - passable
  - testable
  - easily understood

- optimize code for change (aka maintainability). Code needs to be clear, simple, explicit, with good documentation. 
- We need to be able to confidently and quickly make changes, add new features.
- Good sources for inspiration: OOCSS, SMACSS, CSS Lint


Layers of CSS: 

  - Base styles
  - Modules styles
  - Layout styles

Decouple markup from styles to maximize scalability. Not scalable: 

	.promo-box {
	  color: red;
	  background: black;
	}
	.promo-box h3 {
	  font-size: 15px;  
	}


Scalable:

	.promo-box .sub-heading {
	   font-size: 15px; 
	}

What you gain in cleaner html markup, you lose in simplicity.

Use .h2, .h3 instead of h2, h3

Media queries on a specific element: can use "Selector Queries" javascript library. Adds classes to modules based on their size.

The benefits of documenting CSS:
Style-guides and module libraries -- these are the places design and dev come together. Facilitates better collaboration between devs and designers.

Questions: How to automatically build a style guide? Fabrctr? Maybe make a module library with all the modules?

- tags: `css`

__March, 19 2017:__

- temp
- tags: `temp`

__March, 20 2017:__

- temp
- tags: `temp`

__March, 21 2017:__

- temp
- tags: `temp`

__March, 22 2017:__

- temp
- tags: `temp`

__March, 23 2017:__

- temp
- tags: `temp`

__March, 24 2017:__

- temp
- tags: `temp`

__March, 25 2017:__

- temp
- tags: `temp`

__March, 26 2017:__

- temp
- tags: `temp`

__March, 27 2017:__

- temp
- tags: `temp`

__March, 28 2017:__

- temp
- tags: `temp`

__March, 29 2017:__

- temp
- tags: `temp`

__March, 30 2017:__

- temp
- tags: `temp`

__March, 31 2017:__

- temp
- tags: `temp`

### April

__April, 1 2017:__

- temp
- tags: `temp`

__April, 2 2017:__

- temp
- tags: `temp`

__April, 3 2017:__

- temp
- tags: `temp`

__April, 4 2017:__

- temp
- tags: `temp`

__April, 5 2017:__

- temp
- tags: `temp`

__April, 6 2017:__

- temp
- tags: `temp`

__April, 7 2017:__

- temp
- tags: `temp`

__April, 8 2017:__

- temp
- tags: `temp`

__April, 9 2017:__

- temp
- tags: `temp`

__April, 10 2017:__

- temp
- tags: `temp`

__April, 11 2017:__

- temp
- tags: `temp`

__April, 12 2017:__

- temp
- tags: `temp`

__April, 13 2017:__

- temp
- tags: `temp`

__April, 14 2017:__

- temp
- tags: `temp`

__April, 15 2017:__

- temp
- tags: `temp`

__April, 16 2017:__

- temp
- tags: `temp`

__April, 17 2017:__

- temp
- tags: `temp`

__April, 18 2017:__

- temp
- tags: `temp`

__April, 19 2017:__

- temp
- tags: `temp`

__April, 20 2017:__

- temp
- tags: `temp`

__April, 21 2017:__

- temp
- tags: `temp`

__April, 22 2017:__

- temp
- tags: `temp`

__April, 23 2017:__

- temp
- tags: `temp`

__April, 24 2017:__

- temp
- tags: `temp`

__April, 25 2017:__

- temp
- tags: `temp`

__April, 26 2017:__

- temp
- tags: `temp`

__April, 27 2017:__

- temp
- tags: `temp`

__April, 28 2017:__

- temp
- tags: `temp`

__April, 29 2017:__

- temp
- tags: `temp`

__April, 30 2017:__

- temp
- tags: `temp`

### May

__May, 1 2017:__

- temp
- tags: `temp`

__May, 2 2017:__

- temp
- tags: `temp`

__May, 3 2017:__

- temp
- tags: `temp`

__May, 4 2017:__

- temp
- tags: `temp`

__May, 5 2017:__

- temp
- tags: `temp`

__May, 6 2017:__

- temp
- tags: `temp`

__May, 7 2017:__

- temp
- tags: `temp`

__May, 8 2017:__

- temp
- tags: `temp`

__May, 9 2017:__

- temp
- tags: `temp`

__May, 10 2017:__

- temp
- tags: `temp`

__May, 11 2017:__

- temp
- tags: `temp`

__May, 12 2017:__

- temp
- tags: `temp`

__May, 13 2017:__

- temp
- tags: `temp`

__May, 14 2017:__

- temp
- tags: `temp`

__May, 15 2017:__

- temp
- tags: `temp`

__May, 16 2017:__

- temp
- tags: `temp`

__May, 17 2017:__

- temp
- tags: `temp`

__May, 18 2017:__

- temp
- tags: `temp`

__May, 19 2017:__

- temp
- tags: `temp`

__May, 20 2017:__

- temp
- tags: `temp`

__May, 21 2017:__

- temp
- tags: `temp`

__May, 22 2017:__

- temp
- tags: `temp`

__May, 23 2017:__

- temp
- tags: `temp`

__May, 24 2017:__

- temp
- tags: `temp`

__May, 25 2017:__

- temp
- tags: `temp`

__May, 26 2017:__

- temp
- tags: `temp`

__May, 27 2017:__

- temp
- tags: `temp`

__May, 28 2017:__

- temp
- tags: `temp`

__May, 29 2017:__

- temp
- tags: `temp`

__May, 30 2017:__

- temp
- tags: `temp`

__May, 31 2017:__

- temp
- tags: `temp`

### June

__June, 1 2017:__

- temp
- tags: `temp`

__June, 2 2017:__

- temp
- tags: `temp`

__June, 3 2017:__

- temp
- tags: `temp`

__June, 4 2017:__

- temp
- tags: `temp`

__June, 5 2017:__

- temp
- tags: `temp`

__June, 6 2017:__

- temp
- tags: `temp`

__June, 7 2017:__

- temp
- tags: `temp`

__June, 8 2017:__

- temp
- tags: `temp`

__June, 9 2017:__

- temp
- tags: `temp`

__June, 10 2017:__

- temp
- tags: `temp`

__June, 11 2017:__

- temp
- tags: `temp`

__June, 12 2017:__

- temp
- tags: `temp`

__June, 13 2017:__

- temp
- tags: `temp`

__June, 14 2017:__

- temp
- tags: `temp`

__June, 15 2017:__

- temp
- tags: `temp`

__June, 16 2017:__

- temp
- tags: `temp`

__June, 17 2017:__

- temp
- tags: `temp`

__June, 18 2017:__

- temp
- tags: `temp`

__June, 19 2017:__

- temp
- tags: `temp`

__June, 20 2017:__

- temp
- tags: `temp`

__June, 21 2017:__

- temp
- tags: `temp`

__June, 22 2017:__

- temp
- tags: `temp`
