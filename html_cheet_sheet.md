

    
    HTML (HyperText Markup Language) defines the structure and meaning of content on a web page. CSS styles it; JavaScript adds behavior.

1. Basic HTML document
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Page</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>My first webpage.</p>
</body>
</html>
Part	Purpose
<!DOCTYPE html>	Tells the browser to use modern HTML
<html>	Root element of the page
lang="en"	Declares the page language
<head>	Metadata and resources; not page content
<meta charset="UTF-8">	Character encoding
Viewport meta	Helps the page scale on mobile devices
<title>	Text shown in browser tab/search results
<body>	Visible page content
2. Elements, tags, and attributes
<p class="intro" id="welcome">Hello!</p>

    Tag: p
    Element: opening tag + content + closing tag (<p>...</p>)
    Attribute: extra information in the opening tag (class, id)
    Content: Hello!

Paired and void elements
<p>This is a paired element.</p>
<br>
<img src="photo.jpg" alt="A mountain">
<hr>

Void elements do not have closing tags: br, hr, img, input, meta, link, area, base, col, embed, source, track, wbr.
3. Headings and text
<h1>Main heading</h1>
<h2>Section heading</h2>
<h3>Subsection</h3>
<h4>Heading level 4</h4>
<h5>Heading level 5</h5>
<h6>Heading level 6</h6>

<p>A paragraph of text.</p>
<strong>Important text</strong>
<em>Emphasized text</em>
<b>Attention without extra importance</b>
<i>Alternate voice or mood</i>
<small>Small print</small>
<mark>Highlighted text</mark>
<del>Deleted text</del>
<ins>Inserted text</ins>
<sub>Subscript: H<sub>2</sub>O</sub>
<sup>Superscript: x<sup>2</sup></sup>
<blockquote cite="https://example.com">A longer quotation.</blockquote>
<q>A short inline quotation.</q>
<abbr title="HyperText Markup Language">HTML</abbr>
<code>console.log("Hi")</code>
<pre>Text preserves spaces
and line breaks.</pre>

Best practices

    Use one meaningful main <h1> for the page (usually).
    Do not choose headings just to make text look big; use CSS for appearance.
    Use <strong> and <em> when their meaning is appropriate.

4. Links (anchors)
<a href="https://example.com">Visit Example</a>
<a href="about.html">About page</a>
<a href="#contact">Jump to Contact</a>
<a href="mailto:hello@example.com">Email us</a>
<a href="tel:+911234567890">Call us</a>
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
    Open in a new tab
</a>

<section id="contact">
    <h2>Contact</h2>
</section>
Attribute	Purpose
href	Destination URL/path/fragment
target="_blank"	Opens in a new tab/window
rel="noopener noreferrer"	Security/privacy protection for new-tab links
title	Advisory information (not a substitute for accessible text)
5. Images
<img src="images/cat.jpg" alt="A cat sitting by a window" width="400">
Attribute	Purpose
src	Image path or URL
alt	Text alternative for accessibility; use alt="" for decorative images
width, height	Dimensions; helps reserve layout space
loading="lazy"	Defers loading an image until it is near the viewport
Figure and caption
<figure>
    <img src="mountain.jpg" alt="Snow-covered mountain at sunrise">
    <figcaption>Sunrise over the mountain.</figcaption>
</figure>
6. Lists
Unordered list (bullets)
<ul>
    <li>Tea</li>
    <li>Coffee</li>
    <li>Juice</li>
</ul>
Ordered list (numbered)
<ol>
    <li>Install Python</li>
    <li>Write code</li>
    <li>Run the program</li>
</ol>
Nested list
<ul>
    <li>Frontend
        <ul>
            <li>HTML</li>
            <li>CSS</li>
        </ul>
    </li>
    <li>Backend</li>
</ul>
Description list
<dl>
    <dt>HTML</dt>
    <dd>Defines page structure.</dd>
    <dt>CSS</dt>
    <dd>Controls presentation.</dd>
</dl>
7. Tables
<table>
    <caption>Student marks</caption>
    <thead>
        <tr>
            <th scope="col">Name</th>
            <th scope="col">Marks</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Asha</td>
            <td>90</td>
        </tr>
        <tr>
            <td>Rahul</td>
            <td>85</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th scope="row">Average</th>
            <td>87.5</td>
        </tr>
    </tfoot>
</table>
Element	Purpose
<table>	Table container
<caption>	Table title/description
<thead>	Header rows
<tbody>	Main data rows
<tfoot>	Footer/summary rows
<tr>	Table row
<th>	Header cell
<td>	Data cell
colspan	Makes a cell span columns
rowspan	Makes a cell span rows

Example spanning columns:
<td colspan="2">Spans two columns</td>

Use tables for tabular data—not to lay out a webpage.
8. Forms
<form action="/submit" method="post">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>

    <button type="submit">Submit</button>
</form>
Common input types
<input type="text">
<input type="password">
<input type="email">
<input type="number">
<input type="tel">
<input type="url">
<input type="search">
<input type="date">
<input type="time">
<input type="datetime-local">
<input type="checkbox">
<input type="radio">
<input type="file">
<input type="color">
<input type="range">
<input type="hidden">
<input type="submit">
<input type="reset">
Important form attributes
Attribute	Purpose
name	Key used when form data is submitted
id	Unique identifier; connects label and element
value	Initial/current value
placeholder	Hint inside the field
required	Field must be filled
min, max	Minimum/maximum for applicable values
minlength, maxlength	Text length limits
step	Allowed increment for numeric/date inputs
checked	Initially selects checkbox/radio
disabled	Disabled control; generally not submitted
readonly	Cannot be edited, but is generally submitted
autocomplete	Browser autofill hint
Label
<label for="age">Age:</label>
<input type="number" id="age" name="age">

A label's for value should match the input's id.
Textarea
<label for="message">Message:</label>
<textarea id="message" name="message" rows="4" cols="30"></textarea>
Select / dropdown
<label for="city">City:</label>
<select id="city" name="city">
    <option value="">Choose a city</option>
    <option value="pune">Pune</option>
    <option value="mumbai">Mumbai</option>
</select>
Radio buttons (choose one)
<p>Choose a plan:</p>
<label><input type="radio" name="plan" value="basic"> Basic</label>
<label><input type="radio" name="plan" value="pro"> Pro</label>

Radio buttons in the same group share the same name.
Checkboxes (choose multiple)
<p>Skills:</p>
<label><input type="checkbox" name="skill" value="html"> HTML</label>
<label><input type="checkbox" name="skill" value="css"> CSS</label>
Fieldset and legend
<fieldset>
    <legend>Personal details</legend>
    <label for="full-name">Name:</label>
    <input id="full-name" name="full-name">
</fieldset>
Form methods

    GET: form values are appended to the URL; suitable for searches/filtering.
    POST: sends data in the request body; often used to submit/change data.
    HTML validation is helpful but server-side validation is still required.

9. Semantic HTML (meaningful page structure)
<header>
    <h1>Website name</h1>
</header>

<nav aria-label="Main navigation">
    <a href="/">Home</a>
    <a href="/about">About</a>
</nav>

<main>
    <section>
        <h2>About us</h2>
        <p>Section content.</p>
    </section>

    <article>
        <h2>News article</h2>
        <p>Independent content.</p>
    </article>

    <aside>
        <p>Related information.</p>
    </aside>
</main>

<footer>
    <p>Copyright information</p>
</footer>
Element	Typical purpose
<header>	Introductory content for page/section
<nav>	Navigation links
<main>	Main content of the page
<section>	Thematic section, usually with a heading
<article>	Self-contained content that can stand on its own
<aside>	Complementary/sidebar content
<footer>	Footer for page/section
<div>	Generic block container; no semantic meaning
<span>	Generic inline container; no semantic meaning
10. Audio and video
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    Your browser does not support audio.
</audio>

<video controls width="640" poster="thumbnail.jpg">
    <source src="video.mp4" type="video/mp4">
    Your browser does not support video.
</video>

Common attributes: controls, autoplay, muted, loop, preload, poster (video).

Autoplay is often blocked unless media is muted or the user has interacted.
11. Useful miscellaneous elements
<details>
    <summary>Show more</summary>
    <p>Hidden content appears when expanded.</p>
</details>

<time datetime="2026-11-23">23 November 2026</time>

<address>
    Contact: hello@example.com
</address>

<hr>
<br>
12. Div vs Span
<div class="card">
    <h2>Card title</h2>
    <p>Card content.</p>
</div>

<p>This is <span class="highlight">highlighted text</span> within a sentence.</p>

    <div>: generic block-level container (commonly used to group/layout content).
    <span>: generic inline container (commonly used to style a small piece of text).
    Prefer semantic elements when they accurately describe the content.

13. Classes and IDs
<p class="note">First note</p>
<p class="note">Second note</p>
<p id="unique-note">Unique note</p>

    class: reusable; multiple elements can share a class; an element can have multiple classes.
    id: should be unique within the document.
    CSS class selector: .note
    CSS ID selector: #unique-note

14. HTML entities
Character	Entity
<	&lt;
>	&gt;
&	&amp;
"	&quot;
'	&apos;
Non-breaking space	&nbsp;
©	&copy;
®	&reg;
₹	&#8377; or &₹; is not a standard named entity

Example:
<p>Use &lt;p&gt; to create a paragraph.</p>
<p>Tom &amp; Jerry</p>
15. Comments
<!-- This is an HTML comment.
It is not displayed as page content. -->
16. Metadata and linking CSS/JavaScript
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="A short description of this webpage.">
    <title>My Website</title>

    <link rel="stylesheet" href="styles.css">
    <link rel="icon" href="favicon.ico">
</head>
<body>
    <script src="script.js" defer></script>
</body>

    <link> commonly connects external resources such as CSS and favicon.
    <script> loads or contains JavaScript.
    defer downloads the external script while parsing and runs it after parsing, before DOMContentLoaded.
    Keep page-specific metadata inside <head>.

17. Accessibility essentials

    Use semantic HTML elements whenever possible.
    Give meaningful images descriptive alt text; decorative images should usually have alt="".
    Associate every form control with a <label>.
    Use headings in a logical hierarchy.
    Make link text describe its destination (avoid “click here”).
    Ensure controls can be operated with a keyboard.
    Do not rely on color alone to communicate meaning.
    Use table headers (<th>) for data tables.

18. Common beginner mistakes

    Forgetting <!DOCTYPE html>.
    Forgetting to close non-void elements.
    Nesting elements incorrectly.
    Using headings only for their visual size.
    Using <br> repeatedly to create spacing (use CSS).
    Using tables for layout.
    Missing alt on images.
    Using duplicate id values.
    Using a <button> without an appropriate type inside forms (it defaults to submit).
    Forgetting name on form fields that need to be submitted.
    Assuming client-side validation makes data secure.

19. Quick page template
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Describe your page briefly.">
    <title>Page Title</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>Website Title</h1>
        <nav aria-label="Main navigation">
            <a href="#home">Home</a>
            <a href="#about">About</a>
        </nav>
    </header>

    <main id="home">
        <section id="about">
            <h2>About</h2>
            <p>Write your content here.</p>
        </section>
    </main>

    <footer>
        <p>&copy; 2026 My Website</p>
    </footer>

    <script src="script.js" defer></script>
</body>
</html>
