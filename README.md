# Burnham

Burnham is a simple set of Sass (SCSS) mixins to create fixed-size, responsive, grid-based layouts in CSS with minimal changes required to HTML. It does _not_ use [CSS Grid](https://www.w3.org/TR/css-grid-1/).

[Demo →](#@joseph)

## Getting started

1. Place the ```_burnham.scss``` file in the same directory as your other Sass files.

2. In the Sass file you wish to use Burnham include near the top of the file:

	```sass
	@import '_burnham';
	```

3. For each section of the page where you want to use the grid:

	```sass
	main {
		@include container($width: (0: 6, 8: 4));
	}
	```

4. For each element you want to style, include the mixin:

	```sass
	nav {
		@include block($width: (0: 6, 8: 3))
	}

	article {
		@include block($width: (0: 6, 8: 5));
	}
	```

## Basic concepts

[@joseph: insert basic labeled grid parts: column, gutter; note outer-most gutter handling]

@marvin: what's the largest concept? a grid or a container?

*Column widths and gutters have a fixed size specified in rems.* That's different than many (most?) other responsive grid systems ([Bootstrap](http://getbootstrap.com), [Material](https://material.io/components/web/catalog/layout-grids/), [Foundation](http://foundation.zurb.com/sites/docs/xy-grid.html), [Skeleton](http://getskeleton.com), [Tachyons](http://tachyons.io), the [Gridset specimens](https://gridsetapp.com), etc.).<sup>[1](#footnote-1)</sup> They typically assume you want to divide a horizontal space into an arbitrary number of proportionally-sized columns. Sometimes they even let you nest proportionally sized columns, which seems prone to odd alignments. Because these other grid systems assume columns should be proportionally-sized subdivisions, they specify widths in percentages. So, often, columns grow and shrink in size as the browser window is resized. In contrast, Burnham's columns _don't_ change size as the browser is resized. Instead...

*The number of columns that an element occipies is based on media queries.* You specify how many columns wide each element should be for each breakpoint. So, there are discrete rather than continuous changes in the width of elements. Through some clever syntax, you can apply simple constraints to elements, for example:

- When there are 12 columns on the screen, be 3 columns wide; when there are 16+ columns on the screen, be 4 columns wide
- Occupy all the available columns until there are 6+ columns available, then remain 6 columns wide
- Occupy 4 columns, but if there are 6+ columns available, indent one column

[@joseph: make an animated gif with various annotated positionings]

*Breakpoints are defined the number of columns that appear on the screen.* Continuous ranges... all the math done for you... @joseph - merge the above two, and the below one?

*Elements may be positioned by skipping a number of columns.*

*Grids (@marvin: containers?) can be locked to only grow in even or odd numbers of columns—or to only grow when a certain minimum number of columns are reached.* Watch out, though, because if you change this between pages, then your web site will have different widths from page to page at the same browser size.

*Column sizing should not be nested.* Burnham assumes an orientation to the larger layout, so you shouldn't nest column sizes. Instead, make sure each block element has a defined width in columns.

There are two ways to position elements in the grid. They may not be nested inside each other, but both may be used on an HTML page. [@marvin: is that true?]


### 1. Apply to relatively-positioned block elements

<!--[@joseph: convert diagram to non-ascii style?]-->

```
+-----------------------------------------------------------------------------+
|                                                                             |
|  @include container or centered-container (div-like, fixed-width)           |
|                                                                             |
|    +-------------------------------------------------------------------+    |
|    |                                                                   |    |
|    |  @include block-wrap (div-like, optional)                         |    |
|    |                                                                   |    |
|    |    +---------------------------------------------------------+    |    |
|    |    |                                                         |    |    |
|    |    |  @include block                                         |    |    |
|    |    |                                                         |    |    |
|    |    |                                                         |    |    |
|    |    +---------------------------------------------------------+    |    |
|    |                                                                   |    |
|    |                                                                   |    |
|    +-------------------------------------------------------------------+    |
|                                                                             |
|                                                                             |
+-----------------------------------------------------------------------------+
```

### 2. Apply to absolutely positioned block elements

<!--[@joseph: convert diagram to non-ascii style?]-->

```
+-----------------------------------------------------------------------------+
|                                                                             |
|  @include absolute-block                                                    |
|                                                                             |
|                                                                             |
+-----------------------------------------------------------------------------+
```


## Origin

Burnham is named in honor of [Daniel Burnham's plan for the city of Chicago](https://en.wikipedia.org/wiki/Burnham_Plan_of_Chicago).

Various versions of the original implementation were written by [Marvin Klein](http://marvinklein.com/for/burnham) in 2017, drawing on frequent discussions with [Joseph Dombroski](http://jwdomb.com/for/burnham), who wanted a grid system that would facilitate [International Typographic Style](https://en.wikipedia.org/wiki/International_Typographic_Style) without the mess of class names and liquid column widths used by other systems. It was first applied to the [Netcapital web site](https://netcapital.com/for/burnham) in January 2017. Together, Marvin and Joseph prepared this repository to share as an open source project in the summer of 2017.


## Versioning

**Until our 1.0 release, everything is subject to change.**

We use [semantic versioning](http://semver.org/spec/v2.0.0.html) to indicate changes to our interfaces and behaviors. That means that major releases (like 1.0.0, 2.0.0, etc.) are allowed to have features that might _not_ be backwards-compatible; however, minor releases (like 1.1.0, 1.2.0, etc.) contain only backwards-compatible features. Patch releases (like 1.1.1, 1.1.2, etc.) contain only bug fixes. There might be exceptions (particularly if there are bugs), but we try to follow this set of rules closely. 

## Contributing

See the ```CONTRIBUTING.md``` file in this folder.

## License

See the ```LICENSE``` file in this folder.

## Notes

[<a name="footnote-1">1</a>]: Burnham provides a grid that's kinda similar in effect to Salesforce's Lightning Design System's ["no column stretch w/ gutters" grid system](https://www.lightningdesignsystem.com/utilities/grid/), except, in Burnham, the outer-most gutters fall outside the parent container. We didn't know this when we made it.