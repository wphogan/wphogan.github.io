#Improving your SASS


Modular SASS allows for more scalable, maintainable, and re-useable CSS
Styles shouldn't depend on HTML structure -- should be as 'flat' as possible. 

Bad: header nav .navbar {}
Good: .main-navbar {}

SASS Variables: 
`$blue : #xxx;`
then,
`$color-primary: $blue;`

$base__font-size: 16px;
$base__font: 24px;


// Calculate Ems from Pxs

@function em($target, $context: $base__font-size) {
	@return ($target / $context) * 1em;
}
h1 {
	padding: em(46px) 0;
	font-size: em(42px);
	line-height: (46px / 42px);
	margin-bottom: em(70px, 42px);
}

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


##BEM 
*BEM naming conventions, SMACSS categorization conventions*
Block Element Modifier
class names convey information about the 
context is in the name of the selector

base component (block, module wrapper)
	child element
	modifier of either 

can be subjective.
blocks should be able to be used in other projects without dependancies


not necessary with blocks that are not reused
break something into a module / block only if it'd be useful in another context
communicate what a block of HTML does just from it's naming convention, and selectors are easier to understand because we provide the context directly into the selector
avoid nesting so styles are not html dependent. shallow. classes over ids. 
goal: to be able to apply styles independent of location
.block__element--modifier

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

Directories in sass:
*each directory has index.scss that imports partials. Can use globbing.

Base:

-	h1,h2,h3,h4,h5,h6,p,a,body,*

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