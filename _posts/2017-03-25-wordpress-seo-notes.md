---
layout: post
title: WordPress SEO Notes
---

## Introduction

- Content is always king
- Title and Site Tagline should work together and cover core keywords
- Better when both are displayed in the header of the site
- Logo: make sure to have an alt description
- Enabling "Search Engine Visibility" will do the following: 
	- WordPress does not setup a `robots.txt`. It instead uses page-level `noindex` tags that tell search engines to ignore a given page.
	- `<meta name="robots" content="noindex,follow" />`
- `Robots.txt` tells search engine crawlers which pages to index and which to ignore.
- Moz.com is a tool that shows the search results of your site given a set of search terms.

## Links: 

- types: internal, external, anchors
- Linking to authoritative sources will help SEO
- Internal site links will be bolstered by the keywords in the hyperlinked text
- Don't place external links high on the page
- Avoid "Learn More" and "Read More" links, as they are not descriptive. Alternately, you could say, "If you want to learn more, check out this article about the [start link]top five things to improve your WordPress SEO[end link]."
- Broken Link checker plugin will help ID any 404's


## Images

- Unique images are best
- Img title: just what appears internally in the media library
- Alt text: read by search engines, read by google image search. Put keywords here. Avoid over-used and popular keywords. Try to use something unique.
- Try to take advantage of image searches. If you can take your written content and put it into an image with proper alt text, you'll be able to gain users via the image search.

## Videos:

- YouTube -- not great for linking people to your site
- If you want to leverage YouTube to advertise your particular brand, YouTube is great. But if you want to drive traffic to your site, you may need to try something like "Wistia". 
- Using __video site maps__ will allow people to search google videos and find video content hosted on your site

## Categories and Tags as they relate to SEO:

- From SEO perspective, make sure to add a description for all the tags and categories. Use all relevant keywords. This is essential for sites that use category / tag links. Links will lead to category / tag archive pages that will display the description at the top of the page. 
- On archive pages in general, make sure not to list complete content. Instead, only use excerpts. Otherwise, there is a chance google will ignore the page due to duplicate content.
- Menu title attribute has a questionable affect on SEO.
- Widgets are not generally helpful re:SEO indexing. They're more effective for user interaction and generating activity.

## Title tags: 

- Since WP 4.1, this is best practice -- add this code to functions.php: `add_theme_support('title-tag');`. It automatically places the title in the header. This allows plugin developers to more easily edit title tag if they need to -- it's not longer hard-coded into the site. We can then edit the title tag by adding a filter. Good idea: set filter to only show title tag separator on subpages. 


## Meta Descriptions:

- This is the text that appears under the page title in the search results.
- Add this function to `functions.php`: `wpt_add_meta_description_tag` that hooks into `wp_head` and either shows the excerpt (single and page.php) or the generic blog description
- Note: each excerpt should be unique. Not a best practice to use the generic blog description. These meta descriptions should be kept to ~130 chars.

## Headers:

- H1 for site title on home page, then, NOT as a header on rest of the pages. On feed pages, article titles should be H2, but on single post, should be H1.
	- Site title on homepage: h1
	- Site title on all other pages: p (with appropriate aria tags, etc)
- Ideal: keep titles to under 55 characters.
- H1 should be page title. Next, headers should be sequential (H2 > H3 > H4 > etc.)
- Idea for my work: Write a custom title function for all titles that knows when to use h1's and h2's for article/page/post/etc titles both on singular pages AND on feed pages. 

## Breadcrumbs:

- Checkout the WordPress breadcrumb code on thewebtaylor.

## Schema:

- schema.org lists all the different schema types used on a website. It's very extensive. A few schemas include: book, movie, recipe, TVseries, creative works (blog posts, code snippets, etc), audio, event, health and medical types, organization, person, place, product, review, action. 
- Requires some extra markup `itemprop`, `itemscope` etc.
- Using this markup allows search engines to display specific content in the search results.
- Can check out WordPress themes that have schema built in.
- Check out a schema generator.
- Schema Creator plugin is an option
- Idea for my work: create a way for users to enter org address and have it generate schema markup in the footer.
- Idea: create A light-weight XML site map generator
- Go thru Yoast SEO to see how/what it does. What does the premium version do?

## Site Speed:

- Speed is a factor for SEO!
- Test site speed: tools.pingdom.com
- Check out the number of requests and try to reduce it. Minify and combine files

---

Outstanding questions & to-dos: Research Wired.com, other massively popular and well resourced WordPress sites and see how they markup a page with an eye towards header tags and site title/description tags.

What can we do to get breadcrumbs to work for all post types and pages?

