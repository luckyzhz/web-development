# 03-Common HTML elements

> Introduce some basic HTML elements.

---

## Heading and paragraph

There are six heading elements: `h1`, `h2`, `h3`, `h4`, `h5`, and `h6`. Each element represents a different level of content in the document; `<h1>` represents the main heading, `<h2>` represents subheadings, `<h3>` represents sub-subheadings, and so on. Besides, `<p>` element was used to wrap paragraphs.

Here is an example:

```html
<h1>I am the title of the story</h1>

<p>I am a paragraph.</p>

<p>I am another paragraph.</p>
```

A few best practices:
- Use a **single `<h1>`** per page — this is the top level heading, and all others sit below this in the hierarchy.
- Use the headings in the **correct order**. Don't use `<h3>` to represent subheadings, followed by `<h2>` to represent sub-subheadings.
- Of the six heading levels available, you should aim to use **no more than three** per page. If you use too many levels of headings, it is advisable to spread the content over multiple pages.

---

## List

It is OK to nest one list inside another one.

### Unordered

```html
<ul>
    <li>milk</li>
    <li>eggs</li>
    <li>bread</li>
</ul>
```

### Ordered

```html
<ol>
    <li>Drive to the end of the road</li>
    <li>Turn right</li>
    <li>Go straight across the first two roundabouts</li>
</ol>
```

---

## Emphasis and importance

### Emphasis

```html
<!-- sarcastic or passive-aggressive -->
<p>I am <em>glad</em> you weren't <em>late</em>.</p>
```

### Strong importance

```html
<p>This liquid is <strong>highly toxic</strong>.</p>
```

---

## Hyperlink

### Adding supporting information with the title attribute

```html
<p>
  I'm creating a link to
  <a
    href="https://www.mozilla.org/en-US/"
    title="The best place to find more information about Mozilla's
          mission and how to contribute">
    the Mozilla homepage</a>.
</p>
```

### Document fragments

It's possible to link to a specific part of an HTML document, known as a **document fragment**. To do this you first have to assign an `id` attribute to the element you want to link to. It normally makes sense to link to a specific heading, so this would look something like the following:

```html
<h2 id="Mailing_address">Mailing address</h2>
```

Then to link to that specific `id`, you'd include it at the end of the URL, preceded by a hash (`#`), for example:

```html
<p>
  Want to write us a letter? Use our
  <a href="contacts.html#Mailing_address">mailing address</a>.
</p>
```

You can even use the document fragment reference on its own to link to *another part of the current document*:

```html
<p>
  The <a href="#Mailing_address">company mailing address</a> can be found at the
  bottom of this page.
</p>
```

### Use the download attribute when linking to a download

When you are linking to a resource that's to be downloaded rather than opened in the browser, you can use the `download` attribute ***to provide a default save filename***. Here's an example with a download link to the latest Windows version of Firefox:

```html
<a
  href="https://download.mozilla.org/?product=firefox-latest-ssl&os=win64&lang=en-US"
  download="firefox-latest-64bit-installer.exe">
  Download Latest Firefox for Windows (64-bit) (English, US)
</a>
```

### Email links

Use the `<a>` element and the `mailto:` URL scheme:

```html
<a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>
```

In fact, **the email address is optional**. If you omit it and your `href` is `mailto:`, a new outgoing email window will be opened by the user's email client *with no destination address*. This is often useful as "**Share**" links that users can click to send an email to an address of their choosing.

#### Specifying details

In addition to the email address, you can provide other information. In fact, **any standard mail header** fields can be added to the `mailto` URL you provide. The most commonly used of these are "`subject`", "`cc`", and "`body`" (which is not a true header field, but allows you to specify a short content message for the new email). Each field and its value is specified as a **query term**.

Here's an example that includes a cc, bcc, subject and body:

```html
<a
  href="mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">
  Send mail with cc, bcc, subject and body
</a>
```

!> **Note**: The values of each field must be **URL-encoded** with non-printing characters (invisible characters like tabs, carriage returns, and page breaks) and spaces [percent-escaped](https://en.wikipedia.org/wiki/Percent-encoding). Also, note the use of the question mark (`?`) to separate the main URL from the field values, and ampersands (`&`) to separate each field in the `mailto:` URL. This is standard URL query notation. Read The [GET method](https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data#the_get_method) to understand what URL query notation is more commonly used for.

---

?> Update on: 📅 {docsify-updated}