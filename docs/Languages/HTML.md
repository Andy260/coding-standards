# HTML

This section describes the conventions and styling used when writing HTML. While many versions of HTML exist, this document will focus on HTML5 as it is the most modern version of HTML at the time of writing.

The style used is heavily inspired by the style recommended by [W3 Schools'](https://www.w3schools.com/html/html5_syntax.asp) and [Google's HTML](https://google.github.io/styleguide/htmlcssguide.html) style guides.

## Use Lowercase Elements Names

Use lowercase when declaring elements and tags as this is the generally accepted standard.

```html
<!-- Do -->
<body>
  <p>This is a paragraph.</p>
</body> 

<!-- Don't -->
<BODY>
  <P>This is a paragraph.</P>
</BODY> 
```

## Use Lowercase Attribute Names

When using attributes within tags, use lowercase for the names of the attributes.

```html
<!-- Do -->
<a href="https://www.google.com/">Visit Google</a>
<!-- Don't -->
<a HREF="https://www.google.com/">Visit Google</a> 
```

## Close All Elements With Content

While not strictly necessary for correctly rendering HTML elements in modern browsers, ensuring all tags are closed ensures the HTML document is compliant as well as being easy to understand and follow. This also helps to ensure hard to find bugs in the generated document are less frequent.

```html
<!-- Do -->
<section>
  <p>This is a paragraph.</p>
  <p>This is a paragraph.</p>
</section> 

<!-- Don't -->
<section>
  <p>This is a paragraph.
  <p>This is a paragraph.
</section> 
```

## Always Specify alt, width, and height for Images

Always specify the `alt` attribute for images. This attribute is helpful as it will display the `alt` text if the image cannot be loaded.

Also, always define the `width` and `height` of images. This reduces flickering, because the browser can reserve space for the image before loading (This is the only exception to not using inline css).

```html
<!-- Do -->
<img src="html5.gif" alt="HTML5" style="width:128px;height:128px"> 

<!-- Don't -->
<img src="html5.gif"> 
```

## Formatting Tags And Attributes

When defining tags and their attributes only use spaces between each attribute declaration.

```html
<!-- Do -->
<link rel="stylesheet" href="styles.css"> 

<!-- Don't -->
<link rel = "stylesheet" href = "styles.css"> 
```

## Indentation

Use two spaces for indentation, no tabs.

## Ensure The Title Is Set

In the output HTML, ensure the `<title>` tag is set as this helps with search engine optimisation (SEO), and provides a better user experience. The only time this advice can be omitted is when the resulting HTML code isn't public facing and the `<title>` tag doesn't have any perceivable effect to the user (such as when the resulting HTML is used within mobile apps).

```html
<head>
  <title>Page Title</title>
</head>
```

## Don't Omit `<html>`, `<head>` And `<body>` Tags

In the output HTML ensure the `<html>`, `<head>` and `<body>` tags aren't omitted as this ensures correct HTML document compliance. Much like the `<title>` tag, optional tags can be omitted in non-public facing HTML or when the HTML is rendered within such engines as an app's UI engine.

```html
<!DOCTYPE html>
<html lang="en-us">
<head>
  <title>Page Title</title>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html> 
```

## Ensure `lang` Attribute Is Defined

In the output HTML, ensure the `lang` attribute of the `<html>` tag is defined to declare the language of the document, as this helps with search engines and web page accessibility.

```html
<!DOCTYPE html>
<html lang="en-us">
```

## Meta Data

In the output HTML, ensure the meta data of the resulting document has both the language and character encoding defined as well as defined as early as possible in the document. This ensures proper interpretation of the HTML document and helps with search engine optimisation (SEO).

Also, ensure there's social media compatible meta data for users that share the page with other users on social media platforms. [The Open Graph protocol](https://ogp.me/) should be followed in such situations.  

Finally, ensure the viewport is also set.

```html
<html lang="en-au">
<head>
  <meta charset="UTF-8">

  <!-- Viewport settings used by Bootstrap pages -->
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

  <!-- Always set a title -->
  <title>The Rock (1996)</title>

  <!-- Social Media meta data (Defined by The Open Graph Protocol) -->
  <meta property="og:title" content="The Rock" />
  <meta property="og:type" content="video.movie" />
  <meta property="og:url" content="https://www.imdb.com/title/tt0117500/" />
  <meta property="og:image" content="https://ia.media-imdb.com/images/rock.jpg" />
...
</head>
...
</html>
```

## HTML Comments

While Razor comments should be preferred, if HTML comments in the output HTML is desired, ensure single line comments only occupy one line in the source code, and multi-line comments are wrapped by the `<!--` `-->` tags surround them.

```html
<!-- Single line comment -->

<!--
  Multi
  line
  comment.
-->
```
