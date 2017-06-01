---
layout: post
title: Learning 14 things in 14 days
categories: learning
---
## Goal: learn at least one thing related to WordPress or building websites everyday for the next two weeks and document it here.


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
  - web 2.0 compliant & WCAG compliant
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

__March, 19 2017:__ Change Management 

- Not explicitly related to WordPress or web development, but very relevant when working with a team and introducing new workflows / tools / methodologies / etc. 

![Managing Complex Change](https://lh3.googleusercontent.com/-ZQ2Wro8y55Q/VT14xhFJvAI/AAAAAAAAV0A/9S9b7I542aA/w2048-h1536/Managing%2BComplex%2BChange.jpg)

- And for larger teams, Kotter's Change Management Model:
![Kotters Change Mgmt](http://www.eurogeography.eu/SoC/guidelines/change-management-big.jpg)

__March, 20 2017:__ Yarn is a lot faster than NPM

- Yarn installs faster and creates a lock file that ensures every dev on a project is using the same dependencies. 
- install it globally: `npm install -g yarn`
- install modules from a `package.json` file: `yarn install`
- [link](https://www.youtube.com/watch?v=OCW3Jz6F8Ek&index=48&list=WL&t=26s), tags: `gulp` `yarn` `npm`

__March, 21 2017:__ Best-practice for headers

- H1 for site title on home page, then, NOT as a header on rest of the pages. On feed pages, article titles should be H2, but on single post, should be H1.
	- Site title on homepage: h1
	- Site title on all other pages: p (with appropriate aria tags, etc)
- Ideal: keep titles to under 55 characters.
- H1 should be page title. Next, headers should be sequential (H2 > H3 > H4 > etc.)
- Idea for my work: Write a custom title function for all titles that knows when to use h1's and h2's for article/page/post/etc titles both on singular pages AND on feed pages. 
- tags: `SEO`

__March, 22 2017:__

- schema.org lists all the different schema types used on a website. It's very extensive. A few schemas include: book, movie, recipe, TVseries, creative works (blog posts, code snippets, etc), audio, event, health and medical types, organization, person, place, product, review, action. 
- Requires some extra markup `itemprop`, `itemscope` etc.
- Using this markup allows search engines to display specific content in the search results.
- Can check out WordPress themes that have schema built in.
- Check out a schema generator.
- Schema Creator plugin is an option
- Idea for my work: create a way for users to enter org address and have it generate schema markup in the footer.
- Idea: create A light-weight XML site map generator
- Go thru Yoast SEO to see how/what it does. What does the premium version do?
- tags: `SEO`

__March, 23 2017:__ WordPress site title function

- Since WP 4.1, this is best practice -- add this code to functions.php: `add_theme_support('title-tag');`. It automatically places the title in the header. This allows plugin developers to more easily edit title tag if they need to -- it's not longer hard-coded into the site. We can then edit the title tag by adding a filter. Good idea: set filter to only show title tag separator on subpages. 
- tags: `temp`

__March, 24 2017:__ Highlights from Treehouse Web Accessibility course

- [Filterable and shareable WCAG checklist](https://www.w3.org/WAI/WCAG20/quickref/). This allow you to filter by the three WCAG levels (A, AA, and AAA). It also provides a shareable link to get an entire dev team on the same page for a given project.
- HTML5 alternatives to div tags:
	- header (can have multiple on one page -- can be used on post feeds)
	- footer
	- article 
	- section
	- nav
	- main (just one!)
	- button
	- look up more
	- aside
- replace pxs with rems for more accessibly sites
- chrome AND gulp plugin to audit accessibility
- Skeleton CSS Boilerplate could be a perfect lightweight replacement for Bootstrap
- Get better at using all 4 ARIA Roles (1. Landmark, 2. Document, 3. Widget, 4. Abstract)]
- tags: `temp`

__March, 25 2017:__ GitLab

- GitLab is a free, open source version of GitHub
- Allows you to keep to-do lists, similar to Trello
- Can be self hosted behind a VPN for maximum security
- GitLab's "Pipelines" are scripts that deploy code. This takes the place of Code Ship.
- GitLab has a git importer that allows you to import repos with issues, wikis, etc. 
- Idea: setup GitLab as a document library with a wiki, in addition to hosting private repos
- tags: `git`

__March, 26 2017:__ PHP best practices

- Errors vs warnings -- errors are unrecoverable and cause a crash, warnings just echo a warning
- Important to fix deprecation warnings as they will eventually become breaking errors when they're no longer supported
- Semantic versioning ('semver') [major#.minor#.patch#]
- Major change: major, backwards incompatible changes 
- Minor change: backwards compatible changes
- Patch change: bug fixes, performance patches, etc
- Start with 0.1.0 -- leading 0 says API is not fully stable
- [PSR-1](http://www.php-fig.org/psr/psr-1/) -- basic PHP coding standards that all PHP packages should follow
- [PSR-2](http://www.php-fig.org/psr/psr-2/) -- code stylesheet <3
- tags: `temp`

__March, 27 2017:__ Site Reliability Engineering

- Today I learned what a Site Reliability Engineer is -- a combination of a system administrator and a software engineer. It's a highly specialized position that is very new. Essentially, they are Unix experts who also know programming. This blend of skills makes for some creative and automated solutions to problems that typically require many human hours to complete. 
- When an issue arises, it's important to build in the time and capacity to document the problem and describe the solution. These solutions are compiled into a "playbook" which is then used when future issues arise. A good SRE will rely on a "playbook" to diagnose and solve problems and avoid winging it. 
- [link](https://landing.google.com/sre/book.html)tags: `devops`

__March, 28 2017:__ Accessibility auditing tool

- This! [https://github.com/addyosmani/a11y](https://github.com/addyosmani/a11y)
- Cool accessibility auditing tool that works on local sites. It has also been made into a Gulp plugin :)
- tags: `accessibility`