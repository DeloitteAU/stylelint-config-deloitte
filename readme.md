# Deloitte Digital's CSS Styleguide

This styleguide has been forked from Nicolas Gallagher's [Idiomatic CSS](https://github.com/necolas/idiomatic-css) project. This is a living document and new ideas are always welcome. Please contribute.


## Table of contents

<<toc>>


## 1. General principles

> "Part of being a good steward to a successful project is realizing that writing code for yourself is a Bad Idea™. If thousands of people are using your code, then write your code for maximum clarity, not your personal preference of how to get clever within the spec." - Idan Gazit

* You are not a human code compiler/compressor, so don't try to be one.
* All code in any code-base should look like a single person typed it, no matter how many people contributed.
* Strictly enforce the agreed upon style.
* If in doubt when deciding upon a style, use existing, common patterns.


## 2. Whitespace

Only one style should exist across the entire source of your code-base. Always be consistent in your use of whitespace. Use whitespace to improve readability.

* _Never_ mix spaces and tabs for indentation.
* Always use real tabs instead of spaces. This allows other developers to set a tab width of their choice.

Tip: configure your editor to "show invisibles". This will allow you to eliminate end of line whitespace, eliminate unintended blank line whitespace, and avoid polluting commits. In Sublime Text, this can be achieved by adding `"draw_white_space": "all"` to your User Preferences file.

Tip: use an [EditorConfig](http://editorconfig.org/) file (or equivalent) to help maintain the basic whitespace conventions that have been agreed for your code-base.


## 3. Comments

Well commented code is extremely important. Take time to describe components, how they work, their limitations, and the way they are constructed. Don't leave others in the team guessing as to the purpose of uncommon or non-obvious code.

Comment style should be simple and consistent within a single code base.

* Place comments on a new line above their subject.
* Avoid end of line comments.
* Keep line-length to a sensible maximum, e.g., 80 columns.
* Make liberal use of comments to break CSS code into discrete sections.
* Use "sentence case" comments and consistent text indentation.

Tip: configure your editor to provide you with shortcuts to output agreed-upon comment patterns.

#### Example:

```css
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/**
 * Short description using Doxygen-style comment format
 *
 * Long description first sentence starts here and continues on this line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and documentation. It can include example HTML, URLs, or any other information that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * @todo This is a todo statement that describes an atomic task to be completed at a later date.
 */

/* Basic comment */
```


## 4. Format

The chosen code format must ensure that code is: easy to read; easy to clearly comment; minimizes the chance of accidentally introducing errors; and results in useful diffs and blames.

* Use one discrete selector per line in multi-selector rulesets.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include single space after the colon of a declaration.
* Use lowercase and shorthand hex values, e.g., `#aaa`.
* Use single or double quotes consistently. Preference is for double quotes, e.g., `content: ""`.
* Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* _Where allowed_, avoid specifying units for zero-values, e.g., `margin: 0`.
* Include a space after each comma in comma-separated property or function values.
* Include a semi-colon at the end of the last declaration in a declaration block.
* Place the closing brace of a ruleset in the same column as the first character of the ruleset.
* Separate each ruleset by a blank line.

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    display: block;
    font-family: helvetica, arial, sans-serif;
    color: #333;
    background: #fff;
    background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
}
```

#### Declaration order

Declarations should be ordered in accordance with a single principle. My preference is for structurally important properties (e.g. positioning and box-model) to be declared prior to all others.

```css
.selector {
    /* Positioning */
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    /* Display & Box Model */
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;

    /* Other */
    background: #000;
    color: #fff
    font-family: sans-serif;
    font-size: 16px;
    text-align: right;
}
```

Strict alphabetical ordering is also relatively popular, but the drawback is that it separates related properties. For example, position offsets are no longer grouped together and box-model properties can end up spread throughout a declaration block.

#### Exceptions and slight deviations

Large blocks of single declarations can use a slightly different, single-line format. In this case, a space should be included after the opening brace and before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values - such as collections of gradients or shadows - can be arranged across multiple lines in an effort to improve readability and produce more useful diffs. There are various formats that could be used; one example is shown below.

```css
.selector {
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
```

### Preprocessors: additional format considerations

Different CSS preprocessors have different features, functionality, and syntax. Your conventions should be extended to accommodate the particularities of any preprocessor in use. The following guidelines are in reference to Sass.

* Limit nesting to avoid overly specific CSS selectors. Only nest selectors if you would have written the output with that many selectors if you weren't using Sass.
* Always place `@extend` statements on the first lines of a declaration block.
* Where possible, group `@include` statements at the top of a declaration block, after any `@extend` statements.
* Consider prefixing custom functions with `dd-` (for Deloitte Digital) or another namespace. This helps to avoid any potential to confuse your function with a native CSS function, or to clash with functions from libraries.

```scss
.selector-1 {
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);
    width: x-grid-unit(1);
    // other declarations
}
```


## 5. Naming

Naming is hard, but very important. It's a crucial part of the process of developing a maintainable code base, and ensuring that you have a relatively scalable interface between your HTML and CSS.

* Avoid _systematic_ use of abbreviated class names. Don't make things difficult to understand.
* Use clear, thoughtful, and appropriate names for _HTML classes_.
* Pick an understandable and consistent naming pattern that makes sense both within HTML files and CSS files.
* Selectors for components should uses class names; avoid the use of generic tags and unique ids.

```css
/* Example of code with bad names */

.s-scr {
    overflow: auto;
}

.cb {
    background: #000;
}

/* Example of code with better names */

.is-scrollable {
    overflow: auto;
}

.column-body {
    background: #000;
}
```


## 6. Practical example

An example of various conventions.

```css
/* ==========================================================================
   Grid layout
   ========================================================================== */

/**
 * Example HTML:
 *
 * <div class="grid">
 *     <div class="cell cell-5"></div>
 *     <div class="cell cell-5"></div>
 * </div>
 */

.grid {
    overflow: visible;
    height: 100%;
    /* Prevent inline-block cells wrapping */
    white-space: nowrap;
    /* Remove inter-cell whitespace */
    font-size: 0;
}

.cell {
    position: relative;
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 20%;
    height: 100%;
    /* Set the inter-cell spacing */
    padding: 0 10px;
    border: 2px solid #333;
    vertical-align: top;
    /* Reset white-space */
    white-space: normal;
    /* Reset font-size */
    font-size: 16px;
}

/* Cell states */

.cell.is-animating {
    background-color: #fffdec;
}

/* Cell dimensions
   ========================================================================== */

.cell-1 { width: 10%; }
.cell-2 { width: 20%; }
.cell-3 { width: 30%; }
.cell-4 { width: 40%; }
.cell-5 { width: 50%; }

/* Cell modifiers
   ========================================================================== */

.cell--detail,
.cell--important {
    border-width: 4px;
}
```


## 7. Organization

Code organization is an important part of any CSS code base, and crucial for large code bases.

* Logically separate distinct pieces of code.
* Use separate files (concatenated by Middleman) to help break up code for distinct components.
* When using Sass or Less, abstract common code into variables for color, typography, etc.


## 8. Build and deployment

Projects should always attempt to include some generic means by which source can be linted, tested, compressed, and versioned in preparation for production use. For this task, Deloitte Digital normally uses [Middleman](http://middlemanapp.com). [grunt](https://github.com/cowboy/grunt) by Ben Alman is another excellent tool.


## Acknowledgements

Thanks to everyone who has provided translations and to all those who contributed to [idiomatic.js](https://github.com/rwldrn/idiomatic.js). It was a source of inspiration, quotations, and guidelines.


## License

_Principles of writing consistent, idiomatic CSS_ by Nicolas Gallagher is licensed under the [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/). This applies to all documents and translations in this repository.

Based on a work at [github.com/necolas/idiomatic-css](https://github.com/necolas/idiomatic-css).
