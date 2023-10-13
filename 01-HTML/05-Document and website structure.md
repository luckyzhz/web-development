# 05-Document and website structure

> Plan a basic website structure, and write the HTML to represent this structure.

---

## Basic sections of a document

- **header**
  - Usually a big strip across the top with a big heading, logo, and perhaps a tagline. This usually stays the same from one webpage to another.
- **navigation bar**
  - Links to the site's main sections; usually represented by menu buttons, links, or tabs. Like the header, this content usually remains consistent from one webpage to another.
- **main content**
  - A big area in the center that contains most of the unique content of a given webpage. This is the one part of the website that definitely will vary from page to page.
- **sidebar**
  - Some peripheral info, links, quotes, ads, etc. Usually, this is contextual to what is contained in the main content (for example on a news article page, the sidebar might contain the author's bio, or links to related articles).
- **footer**
  - A strip across the bottom of the page that generally contains fine print, copyright notices, or contact info. It's a place to put common information (like the header) but usually, that information is not critical or secondary to the website itself.

A "typical website" could be structured something like this:

![](../_assets/_images/typical%20website%20layout.png ':size=600')

---

## HTML for structuring content

HTML provides dedicated tags for document structure:
- `<main>` is for content unique to this page. Use `<main>` only once per page, and put it directly inside `<body>`.
- `<article>` encloses a block of related content that makes sense on its own without the rest of the page (e.g., a single blog post).
- `<section>` is similar to `<article>`, but it is more for grouping together a single part of the page that constitutes one single piece of functionality (e.g., a mini map, or a set of article headlines and summaries), or a theme.
- `<aside>` contains content that is not directly related to the main content but can provide additional information indirectly related to it (glossary entries, author biography, related links, etc.).
- `<header>` represents a group of introductory content. If it is a child of `<body>` it defines the global header of a webpage, but if it's a child of an `<article>` or `<section>` it defines a specific header for that section.
- `<nav>` contains the main navigation functionality for the page.
- `<footer>` represents a group of end content for a page.

There are also two non-semantic wrappers:
- `<span>` is an **inline** non-semantic element.
- `<div>` is a **block** level non-semantic element

---

?> {docsify-updated}