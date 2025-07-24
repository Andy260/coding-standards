# Markdown Coding Style

This documents describes the conventions and styling used when contributing Markdown code to this project. In addition to these styles and standards, the coding standards and practises outlined by the [CodingStyle.md](CodingStyle.md) document should also be followed.

In addition to the styles and conventions outlined in this document, the general guidelines outlined within the [GeneralGuidelines.md](../GeneralGuidelines.md) document should also be followed.

These styles and conventions are inspired by [Google's Markdown style guide](https://google.github.io/styleguide/docguide/style.html).

[TOC]

## Capitalisation

Make sure to use the original names of products, tools, binaries with the original capitalisation.

```markdown
<!-- Do -->
# Markdown Style Guide

`Markdown` is a great language and platform for documentation.

<!-- Don't -->
# markdown Style Guide

`markdown` is a great language and platform for documentation.
```

## Layout

Markdown documents should follow the following layout:

1. `# Title`: The first heading should be a H1 heading, ideally the same or nearly the same as the filename. The first H1 heading is used as the page `<title>`.
2. `Short introduction`: 1-3 sentences which provide a high-level overview of the topic.
3. `[TOC]`: Table of contents. (If document isn't a README)
4. `## Topic`: The rest of the headings starting at H2.
5. `## See Also`: *Optional.* Any links that are relevant to the document.

```markdown
# Title

Short introduction.

[TOC]

## Topic

Content.

## See Also

* https://link-to-more-info
```

## Table Of Contents

### When To Use `[TOC]`

If the document isn't a README, use a `[TOC]` directive unless all of the content can be seen without having to scroll.

### `[TOC]` Placement

Place the `[TOC]` directive directly after the page's introduction and before the first H2 heading.

While the placement of the `[TOC]` isn't entirely important for the everyday user, the placement can affect how screen readers or keyboard controls are affected, since in such situations the DOM orders the document's content in the same order as the Markdown document but isn't visually displayed the same to the user.

```markdown
# My Page

This is my introduction **before** the TOC.

[TOC]

## My First Topic
```

## Character Line Limit

While the character line limit is enforced within the [CodingStyle.md](CodingStyle.md), adding new lines within Markdown documents to enforce this and actual change the way the document is rendered by certain Markdown renderers. So in the case of editing Markdown documents, word wrap should be used and only have new lines as expected by the author.

## Headings

This section describes the usage and styling of headings within Markdown documents.

### Use ATX-style Headings

Markdown provides two ways of defining a heading within the document. ATX style headings defined by one-six of the `#` character. And Setext headings with the `=` for H1 headings or `-` for H2 headings underlining the heading text.

While both are valid in the context of the spec, ATX headings should be used as there's H1-H6 available to use and is much easier to understand the current level when editing the document. Whereas Setext only allows for H1 or H2 headings and can be confusing which level a heading is when compared to ATX style headings.

```markdown
<!-- Do: ATX -->
# Heading 1

## Heading 2

### Heading 3

<!-- Don't: Setext -->
Heading 1
=========

Heading 2
---------
```

### Use A Single H1 Heading

Only use a single H1 heading at this heading will be used for the `<title>` of the document. Topic headings should be H2 or lower.

## Lists

This section outlines the usage and styling of lists within Markdown documents.

### Nested List Spacing

When nesting lists, use a 3-space indent for wrapped text within the list items.

```markdown
1. Use 1 space after the item number.
   Use a 3-space indent for wrapped text.
2. Use 1 space again for the next item.
   1. Use 1 space after the 3-space indent for nested lists.
      Use 3 spaces after the 3-space indent for nested wrapped text.

*  Use 2 spaces after a bullet.
   Use a 3-space indent for wrapped text.
   *  Use 2 spaces after the 3-space indent for nested lists.
      Use 3 spaces after the 3-space indent for nested wrapped text.
```

## Code

This section outlines the usage and styling of code displayed within Markdown documents.

### Inline

Use inline \`Backticks\` code spans for small code quotations, field names, filenames, language key words, etc. Also, use inline code when referring to file types in the generic sense.

```markdown
Make sure to read the `README.md`.

`if` statements are helpful.
```

### Use Code Span For Escaping

Wrap code which shouldn't be autolinked within a code span.

```markdown
An example endpoint: `www.google.com`
```

### Codeblocks

Use fenced code blocks with \`backticks\` for code quotations or examples which are longer than a single line.

````markdown
```csharp
MyMethod();
```

```text
Some Text.
```
````

#### Specify A Language

Always specify a language for syntax highlighting, or use `text` as the language if syntax highlighting is not needed (such as when specifying expected console output).

````markdown
<!-- Do -->
```csharp
public void MyFunction() {}
```

Results in this output
```text
It works!
```

<!-- Don't -->
```
public void MyFunction() {}
```

Results in this output
```
It works!
```
````

#### Indent Codeblocks Within Lists

When writing codeblocks within lists, indent them just the same if they were regular text.

````markdown
*  Bullet
   ```csharp
   int myVar = 1;
   ```
*  Next bullet
````

## Links

This section outlines the usage and styling of links within Markdown documents.

### Keep Links Short

Wherever possible, keep links short to ensure to keep higher readability with the source file.

### Use Explicit Paths

Use the explicit path for links to other Markdown documents rather than using the entire qualified URL.

```markdown
<!-- Do -->
[...](/path/to/other/markdown/page.md)

<!-- Don't -->
[...](https://bad-full-url.example.com/path/to/other/markdown/page.md)
```

### Use Informative Link Titles

When writing link titles, ensure they are informative. Link titles such as 'here' or 'link' aren't as informative as a short title of the actual destination such as 'main document'.

```markdown
<!-- Do -->
See the [Markdown guide](markdown.md) for more info, or check out the [style guide](/styleguide/docguide/style.html).

<!-- Don't -->
Check out the Markdown guide for more info ([here](guide.md)), or check out the style guide [here](/styleguide/docguide/style.html).
```

### Reference

For long links or image URLs, it may help if you split the link from the link definition. Readability of the document source should be prioritised.

```markdown
Check the [Markdown style guide][style], which contains suggestions for making documents more readable.

[style]: http://Markdown/corp/Markdown/docs/reference/style.md
```

## Images

Images should only be used sparingly, and simple screenshots should be preferred. A good usage would be during a case where it's easier to show the user the concept rather than describe it. Make sure to still provide appropriate text to describe the image.

## Tables

Make sure to only use tables when they help to further illustrate the given topic. If the data can be more easily read and/or represented with a list, then a table should not be used.

## Strongly Prefer Markdown to HTML

When writing Markdown documents, Markdown code should be strongly preferred over using HTML within the Markdown document. Except for big tables, Markdown should meet almost all your needs.
