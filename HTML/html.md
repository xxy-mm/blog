# HTML

## what and what is not

- what is presented to the viewer
- not how is presented to the viewer

## self closing tags

- meta
- input
- img
- link

## headers

- h1 to h6
- search engines and other user agents usually index page content based on heading elements.

## paragraphs

- p
- br
- pre

> With HTML, you cannot change the output by adding extra spaces or extra lines in your HTML code

```html
<p>This is another paragraph, extra spaces will be removed by browsers</p>
```

## text formatting

- mark: relevance in another context
- strong: important text
- b: just bold text
- i: identifying
- em: stress
- u: underline
- ins: inserted
- sup: superscript
- sub: subscript
- del: deleted
- s: struck-through
- abbr: abbreviation

## anchors and hyperlinks

- href
- hreflang
- rel:
  - [https://www.w3.org/TR/2014/REC-html5-20141028/links.html#linkTypes]
  - [https://microformats.org/wiki/existing-rel-values#HTML5_link_type_extensions]
- target: \_blank,\_self,\_parent,\_top
- title
- download

```html
<a
  href="./demo.css"
  download="test.pdf">
  download
</a>

<a
  href="http://example.com/"
  rel="external">
  example site
</a>

<a href="ftp://example.com/">This could be a link to a FTP site</a>
```

- link to an anchor

```html
<h2 id="Topic1">First topic</h2>
<a href="#Topic1">Click to jump to the First Topic</a>
```

- relative path

consider you're at `https://example.com`

```html
<a href="/page1">page1</a>
// is the same as
<a href="https://example.com/page1">page1</a>
```

- dials a number

- mobile devices
- computers/tablets running software like Skype/FaceTime that can make phone calls.

```html
<a href="tel:11234567890">Call us</a>
```

- open link in new tab/window

```html
<a
  href="example.com"
  target="_blank">
  Text Here
</a>
```

> SECURITY VULNERABILITY WARNING!  
> Using `target="_blank"` gives the opening site partial access to the window.opener object via JavaScript, which allows that page to then access and change the window.opener.location of your page and potentially redirect users to malware or phishing sites.  
> Whenever using this for pages you do not control, add `rel="noopener"` to your link to prevent the window.opener object from being sent with the request.  
> Currently, Firefox does not support `noopener`, so you will need to use `rel="noopener noreferrer"` for maximum effect.  
> The opener can be omitted by specifying `rel=noopener` on a link, or passing `noopener` in the windowFeatures parameter.  
> Windows opened because of links with a target of `_blank` don't get an opener, unless explicitly requested with `rel=opener`.  
> Having a `Cross-Origin-Opener-Policy` header with a value of `same-origin` prevents setting `opener`. Since the new window is loaded in a different browsing context, it won't have a reference to the opening window.

- email

```html
<a href="mailto:example@example.com">Send email</a>

<a
  href="mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">
  Send mail with cc, bcc, subject and body
</a>
```

## list

### ordered list

```html
<ol>
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ol>
```

- manually changing the numbers

```html
<ol start="3">
  <li>This will be 3</li>
</ol>
```

```html
<ol>
  <li value="4">This will chang the number to 4</li>
  <li>This will be 5</li>
</ol>
```

- reversed

```html
<!--produces 3 2 1 -->
<ol reversed>
  <li>item</li>
  <li>item</li>
  <li>item</li>
</ol>
```

- change the type of numeral

- 1: decimal numbers
- a/A: alphabetically ordered (lowercase/uppercase)
- i/I: roman numbers (lowercase/uppercase)

```html
<ol type="I"></ol>
```

### unordered lists

```html
<ul>
  <li>item</li>
  <li>
    item
    <ul>
      <li>sub-item</li>
      <li>sub-item</li>
    </ul>
  </li>
</ul>
```

### description list

```html
<dl>
  <dt>name 1</dt>
  <dt>name 2</dt>
  <dd>value for 1 and 2</dd>
  <dt>name 3</dt>
  <dd>value for 3</dd>
  <dd>value for 3</dd>
</dl>
```

## table

- table
- caption
- colgroup
  - col
- thead
  - tr
  - th
- tbody
  - tr
  - td
    - rowspan
    - colspan
- tfoot
  - tr
  - td

## comment

Inline display elements, usually such as span or a, will include up to one white-space character before and after them in the document. In order to avoid very long lines in the markup (that are hard to read) and unintentional white-space (which affects formatting), the white-space can be commented out.

![whitespace](2024-01-02-12-01-08.png)

## classes and ids
