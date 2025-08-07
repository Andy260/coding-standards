# CSS Coding Style

This documents describes the conventions and styling used when contributing CSS code to the project.

In addition to the styles and conventions outlined in this document, the general guidelines outlined within the [GeneralGuidelines.md](../GeneralGuidelines.md) document should also be followed.

These styles and conventions are inspired by the CSS section of [Google's HTML/CSS style guide](https://google.github.io/styleguide/htmlcssguide.html#CSS), and the (Object Oriented CSS (OOCSS))[https://github.com/stubbornella/oocss/wiki] methodology.

[TOC]

## Formatting

This section describes the expected formatting of CSS source files.

### Put Declaration Blocks On Their Own Line

While most typical CSS style guide may disagree, I prefer to put declaration blocks on their own line. This makes it easier to visually see where blocks start and end at a glance.

```css
/* Do */
.myClass
{
    /* ... */
}

/* Don't */
.myClass {
    /* ... */
}
```

### Alphabetise Declaration Order

When defining declarations within a block, ensure all declarations within the block are alphabetised.

```css
.page 
{
    display: flex;
    flex-direction: column;
    position: relative;
}
```

### Indent Block Content

Ensure all block content (rules within rules) are indented to reflect the hierarchy of the styles to aid in understanding the styles.

```css
.grid
{
    /* ... */

    .row
    {
        /* ... */
    }

    .column
    {
        /* ... */        
    }
}
```

### End Declarations With A Semicolon

After each declaration within a block, end the line with a semicolon.

```css
.myStyle
{
    /* Do */
    color: red;
    display: block;
    position: relative;
}

.myStyle
{
    /* Don't */
    color: red
    display: block
    position: relative
}
```

### Separate Names With A Space

Always use a space after a property name's colon.

```css
.text
{
    /* Do */
    color: red;

    /* Don't */
    color:red;
}
```

### Separate Selectors And Declarations With New Lines

When defining styles with multiple selectors, separate each selector with a new line. This also applies to declarations as well.

```css
/* Do */
h1, 
h2, 
h3
{
    font-weight: normal; 
    position: relative;
}

/* Don't */
h1, h2, h3
{
    font-weight: normal; position: relative;
}
```

### Separate Rules With A New Line

When defining multiple rules within a source file, ensure a new line separates each rule.

```css
/* Do */
.navBar
{
    /* ... */
}

.sidebar
{
    /* ... */
}

/* Don't */
.navBar
{
    /* ... */
}
.sidebar
{
    /* ... */
}
```

### Use Double Quotation Marks

Use double quotation marks for attribute selectors, property values, and within URI values.

```css
/* Do */
@import url("https://cdn.jsdelivr.net/npm/bootstrap@5.3.7/dist/css/bootstrap.min.css");

html
{
    font-family: "open-sans", arial, sans-serif;
}

/* Don't */
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.3.7/dist/css/bootstrap.min.css');
@import url(https://cdn.jsdelivr.net/npm/bootstrap@5.3.7/dist/css/bootstrap.min.css)

html
{
    font-family: 'open-sans', arial, sans-serif;
}
```

## Language Usage

This section specifies coding standards, styles, and/or guidelines relating to the specific usage of the CSS language.

### Use Valid CSS

Always use valid CSS. This helps ensures expected behaviour of the styles on compliant browsers and ensure the codebase is portable and not reliant on the presence of proprietary syntax.

CSS validators can be provided by your IDE of choice, or by using tools such as the [W3C CSS validator](https://jigsaw.w3.org/css-validator/).

```css
/* Do */
.valid-css
{
    background-color: #eee;
    color: #111;
}

/* Don't */
.invalid-css
{
    background-colour: #eee; /* 'background-colour' is not a valid CSS property */
    color: #111;
}

.example
{
    -webkit-border-radius: 10px; /* Vendor-prefixed property */
    border-radius: 10px;
}
```

### Class Naming

When naming classes within CSS source files, use generic and meaningful names. Names should infer the intended usage of the class, and be generic enough that they can be used by multiple elements within an application if the styling is able to be used in multiple places within the application. This ensures that classes are easy to understand in their intended usage and promotes a modular design.

Make sure to also follow the [(Object Oriented CSS (OOCSS)](https://github.com/stubbornella/oocss/wiki) methodology, naming classes in a generic style which allows for classes to be used in multiple locations.

```css
/* Do: Use meaningful, generic names that describe the component's purpose or structure. */
.card
{
    border: 1px solid #ccc;
    padding: 15px;
}

.alert-danger
{
    color: #a94442;
    background-color: #f2dede;
}

/* Don't: Use names that are too specific, not reusable, or tied to content. */
.news-article-box
{
    border: 1px solid #ccc;
    padding: 15px;
}

.red-text
{
    color: #a94442;
    background-color: #f2dede;
}
```

#### Ensure Class Names Are Short But As Long As Needed

When naming classes, ensure the length of the chosen name is both short but as long as needed to help convey the intended usage of the class. This is a balancing act, where code must be descriptive enough to explain its intent but brief enough that it isn't too verbose and hard to read at a glance.

```css
/* Do: Descriptive but concise */
.user-profile
{
    /* ... */
}

.btn-primary
{
    /* ... */
}

/* Don't: Too short or too verbose */
.up
{
    /* Too short, meaning is unclear */
}

.user-profile-section-with-all-the-details
{
    /* Too verbose and hard to read */
}
```

#### Separate Words In Class Names With A Hyphen

When naming a class, make sure to use a hyphen to separate words within the name. Don't use any other characters to separate words in the class names, as hyphens are expected within the CSS world.

```css
/* Do */
.my-class
{
    /* ... */
}

/* Don't */
.MyClass
{
    /* ... */
}
```

### Avoid Type Selectors

When defining a class style, type selectors should be avoided unless absolutely necessary as type selectors occur a performance cost. Situations such as defining a tag specific style for a class (in order to ensure specific behaviour) are acceptable but should be avoided if a solution exists without using a type selector for the style.

A good example of this is how Bootstrap defines styles for elements such as `<button>` and similar tags with a specific `.btn` class. Aim to take a similar approach as much as possible.

```css
/* Do: Define the class independently of the element type for better reusability. */
.nav-list
{
    list-style: none;
    padding: 0;
}

/* Don't: Tying a class to a specific element type reduces reusability and can impact performance. */
ul.nav-list
{
    list-style: none;
    padding: 0;
}
```

### Avoid ID Selectors

ID selectors should be avoided as much as possible as each ID within a page is expected to be unique. This is especially important in PWA frameworks which don't ensure component ID isolation, as this will require the developer to define unique IDs for each ID selector.

Class selectors should be preferred in all situations as they are much more reusable and are much more maintainable compared to ID selectors.

```css
/* Do: Use classes for styling to ensure reusability. */
.main-content
{
    padding: 20px;
}

/* Don't: ID selectors are not reusable and have high specificity, which can lead to maintenance issues. */
#main-content
{
    padding: 20px;
}
```

### Use Shorthand Properties Where Possible

In order to help keep source files as readable as possible, use shorthand properties as much as possible. Not only does this cut down on unnecessary lines of code, it helps keep the source files easier to reason with and understand at a glance.

```css
/* Do */
.element 
{
    border: 1px solid #ccc;
    margin: 10px 5px;
}

/* Don't */
.element 
{
    border-color: #ccc;
    border-style: solid;
    border-width: 1px;
    margin-bottom: 10px;
    margin-left: 5px;
    margin-right: 5px;
    margin-top: 10px;
}
```

### Omit Units after “0” values Unless Required

When defining values to a rule, omit the unit if the value is "0" unless they are required (such as due to a quirk with the language, a requirement with a specific type of rule, or to reduce undefined behaviour).

```css
/* Do */
.element
{
    margin: 0;
    padding: 0;
}

/*
    Sometimes, units are required for '0' values, such as with time-based properties
    or in specific contexts like CSS Grid's fr unit.
*/
.animated-element
{
    transition-delay: 0s;
}

/* Don't */
.other-element
{
    margin: 0px;
    padding: 0em;
}
```

### Always Include Leading 0s In Fractional Values

When defining values between -1 and 1, always ensure to include the leading zero.

```css
/* Do */
.element
{
    opacity: 0.5;
}

/* Don't */
.element
{
    opacity: .5;
}
```

### Always Specify Hexadecimal Values With 6 Characters

Hexadecimal values in CSS (such as colours) can sometimes be defined with three characters. While this can reduce the number of characters needed to define a colour, the full six character definition should be preferred to keep consistency.

In addition to this, most IDEs will use the six character notation when defining a hexadecimal value, as well as display the resolved colour, and often don't resolve colours for hexadecimal values defined with three characters.

```css
/* Do */
.element
{
    color: #ffffff;
}

/* Don't */
.element
{
    color: #fff;
}
```

### Avoid Using `!important` Declarations

The `!important` declaration should be avoided as it disrupts the natural cascade of stylesheets, making it difficult to debug and maintain the CSS. When `!important` is used, it overrides any other declaration for that property, regardless of selector specificity. This can lead to a situation where the only way to override a style is to use another `!important` declaration, creating a fragile and hard-to-manage codebase.

Instead of relying on `!important`, prefer to use CSS specificity rules to achieve the desired styling. By carefully structuring your selectors, you can ensure that the correct styles are applied without breaking the cascade.

```css
/* Do: Use higher specificity to override styles when needed. */
.widget .btn
{
    background-color: #007bff;
}

/* Don't: Using !important disrupts the natural cascade and makes debugging harder. */
.btn
{
    background-color: #ff0000 !important; /* This is hard to override. */
}
```

### Avoid Using "CSS Hacks"

CSS hacks and user agent sniffing should be avoided. These techniques often rely on non-standard syntax or browser-specific parsing bugs to target certain browsers. While they might seem like a quick fix, they are fragile, hard to maintain, and can break with future browser updates. They also often result in invalid CSS.

Instead, prefer modern, standards-compliant approaches like feature queries (`@supports`) to handle cross-browser differences. This allows for progressive enhancement, where you provide a baseline experience for all browsers and enhance it for browsers that support newer features.

```css
/* Do: Use feature queries for progressive enhancement. */
.element
{
    display: flex; /* Fallback for older browsers */
}

@supports (display: grid)
{
    .element
    {
        display: grid; /* Use a more modern layout if supported */
    }
}

/* Don't: CSS hacks are brittle and make code hard to maintain. */
.another-element
{
    color: #000; /* Standard */
    *color: #f00; /* IE7 and below hack */
    _color: #0f0; /* IE6 hack */
}
```
