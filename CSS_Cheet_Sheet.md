

CSS (Cascading Style Sheets) controls how HTML content looks: colors, fonts, spacing, layout, responsiveness, and animations.

1. Ways to add CSS
External stylesheet (recommended)

HTML:
<link rel="stylesheet" href="styles.css">

CSS (styles.css):
h1 {
    color: blue;
}
Internal stylesheet
<head>
    <style>
        p {
            color: green;
        }
    </style>
</head>
Inline style (avoid for normal projects)
<p style="color: red;">Hello</p>

External CSS is easiest to maintain and reuse.
2. CSS syntax
selector {
    property: value;
}
p {
    color: purple;
    font-size: 18px;
}

    Selector: chooses the HTML element(s).
    Property: what you want to change.
    Value: the setting for that property.
    A declaration ends with ;.
    Declarations are grouped inside { }.

3. Selectors
Element selector
p {
    color: navy;
}

Selects all <p> elements.
Class selector

HTML:
<p class="highlight">Important</p>

CSS:
.highlight {
    background-color: yellow;
}

Classes can be reused.
ID selector

HTML:
<h1 id="main-title">My Website</h1>

CSS:
#main-title {
    color: darkgreen;
}

IDs should be unique within the document.
Universal selector
* {
    box-sizing: border-box;
}

Selects every element.
Group selector
h1, h2, p {
    font-family: Arial, sans-serif;
}
Descendant selector (space)
article p {
    color: gray;
}

Selects all paragraphs anywhere inside an article.
Child selector (>)
nav > a {
    text-decoration: none;
}

Selects direct child links of nav.
Adjacent sibling selector (+)
h2 + p {
    margin-top: 0;
}

Selects the first paragraph immediately after an h2.
General sibling selector (~)
h2 ~ p {
    color: gray;
}

Selects paragraphs that follow the h2 and share its parent.
Attribute selectors
input[type="email"] {
    border: 1px solid blue;
}

a[target="_blank"] {
    color: purple;
}
4. Pseudo-classes

A pseudo-class selects an element in a particular state or position.
a:hover {
    color: red;
}

button:active {
    transform: scale(0.98);
}

input:focus {
    outline: 2px solid blue;
}

li:first-child {
    font-weight: bold;
}

li:last-child {
    color: red;
}

li:nth-child(2) {
    color: blue;
}

li:nth-child(odd) {
    background-color: #eee;
}

input:checked {
    accent-color: green;
}

input:disabled {
    opacity: 0.5;
}

input:required {
    border-left: 3px solid orange;
}

Common pseudo-classes:

    :hover
    :active
    :focus
    :focus-visible
    :first-child
    :last-child
    :nth-child(n)
    :checked
    :disabled
    :required
    :valid
    :invalid

5. Pseudo-elements

Pseudo-elements style a particular part of an element.
p::first-letter {
    font-size: 2rem;
}

p::first-line {
    font-weight: bold;
}

h1::before {
    content: "★ ";
}

h1::after {
    content: "!";
}

::selection {
    background-color: yellow;
    color: black;
}

Common pseudo-elements:

    ::before
    ::after
    ::first-letter
    ::first-line
    ::selection
    ::placeholder

`
::before

and::after` generally require the content property.
6. Colors
.box {
    color: red;
    color: #ff0000;
    color: rgb(255, 0, 0);
    color: rgba(255, 0, 0, 0.5);
    color: hsl(0, 100%, 50%);
}
Format	Example
Named	tomato
Hex	#ff6347
RGB	rgb(255, 99, 71)
RGBA	rgba(255, 99, 71, 0.5)
HSL	hsl(9, 100%, 64%)
7. Backgrounds
.box {
    background-color: lightblue;
    background-image: url("background.jpg");
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    background-attachment: scroll;
}

Shorthand:
.hero {
    background: lightblue url("hero.jpg") center / cover no-repeat;
}

Useful values:

    background-size: cover — fills the area; some image may be cropped.
    background-size: contain — shows the whole image; empty space may remain.
    background-repeat: repeat, no-repeat, repeat-x, repeat-y.

8. Text and fonts
p {
    color: #333;
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;
    font-weight: 400;
    font-style: normal;
    text-align: left;
    text-decoration: none;
    text-transform: none;
    line-height: 1.5;
    letter-spacing: 1px;
    word-spacing: 3px;
}

Common values:

    font-weight: normal, bold, 100–`900`.
    text-align: left, right, center, justify.
    text-decoration: none, underline, overline, line-through.
    text-transform: uppercase, lowercase, capitalize.
    line-height: controls distance between text lines.

9. Units
Unit	Meaning
px	CSS pixel; fixed CSS length
%	Relative to a relevant parent/reference
em	Relative to the element's font size (for font-size, relative to parent font size)
rem	Relative to root (html) font size
vw	1% of viewport width
vh	1% of viewport height
dvh	Dynamic viewport height
fr	Fraction of available space in CSS Grid
ch	Approximate width of the 0 glyph in the font

Example:
html {
    font-size: 16px;
}

.card {
    width: 80%;
    padding: 1rem;
    font-size: 1.2rem;
}

.hero {
    min-height: 100vh;
}
10. Box model

Every element is represented by:

Content → Padding → Border → Margin
.box {
    width: 300px;
    height: 150px;
    padding: 20px;
    border: 5px solid black;
    margin: 10px;
}

With default content-box, declared width excludes padding and border.

Recommended global setting:
*,
*::before,
*::after {
    box-sizing: border-box;
}

With border-box, declared width includes content + padding + border.
Box model properties
.box {
    margin: 20px;
    padding: 20px;
    border: 1px solid black;
    border-radius: 10px;
}

Individual sides:
.box {
    margin-top: 10px;
    margin-right: 20px;
    margin-bottom: 10px;
    margin-left: 20px;

    padding-top: 5px;
    padding-right: 10px;
    padding-bottom: 5px;
    padding-left: 10px;
}

Shorthand order: top → right → bottom → left.
margin: 10px;                 /* all sides */
margin: 10px 20px;            /* top/bottom, left/right */
margin: 10px 20px 30px;       /* top, left/right, bottom */
margin: 10px 20px 30px 40px;  /* top, right, bottom, left */
11. Display
.block {
    display: block;
}

.inline {
    display: inline;
}

.inline-block {
    display: inline-block;
}

.hidden {
    display: none;
}
Value	Behavior
block	Starts on a new line; typically takes available width
inline	Flows within text; width/height generally don't apply as expected
inline-block	Flows inline but accepts width/height
none	Element is not displayed and takes no layout space
flex	Creates a flex container
grid	Creates a grid container
12. Position
.static {
    position: static;
}

.relative {
    position: relative;
    top: 10px;
    left: 10px;
}

.absolute {
    position: absolute;
    top: 0;
    right: 0;
}

.fixed {
    position: fixed;
    bottom: 20px;
    right: 20px;
}

.sticky {
    position: sticky;
    top: 0;
}
Position	Meaning
static	Default; normal flow; offsets don't position it
relative	Remains in flow; can be offset; establishes containing block for positioned descendants
absolute	Removed from normal flow; positioned relative to its containing block
fixed	Usually positioned relative to viewport; removed from flow
sticky	Behaves normally until a scroll threshold, then sticks within its scrolling context

Positioning properties:

    top
    right
    bottom
    left
    inset (shorthand)

13. z-index
.card {
    position: relative;
    z-index: 2;
}

.overlay {
    position: fixed;
    inset: 0;
    z-index: 100;
}

z-index controls stacking order within stacking contexts. A larger number does not necessarily appear above everything if elements are in different stacking contexts.
14. Flexbox

Flexbox is primarily a one-dimensional layout system (row or column).

HTML:
<div class="container">
    <div class="item">One</div>
    <div class="item">Two</div>
    <div class="item">Three</div>
</div>

CSS:
.container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 20px;
}
Flex container properties
.container {
    display: flex;
    flex-direction: row;       /* row | row-reverse | column | column-reverse */
    flex-wrap: wrap;           /* nowrap | wrap | wrap-reverse */
    justify-content: center;
    align-items: center;
    align-content: center;
    gap: 20px;
    row-gap: 10px;
    column-gap: 20px;
}
Property	Controls
flex-direction	Main axis direction
flex-wrap	Whether items wrap
justify-content	Distribution along main axis
align-items	Alignment along cross axis for a line
align-content	Distribution of multiple flex lines
gap	Space between items
justify-content values

    flex-start
    flex-end
    center
    space-between
    space-around
    space-evenly

align-items values

    stretch
    flex-start
    flex-end
    center
    baseline

Flex item properties
.item {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 200px;
    align-self: center;
    order: 2;
}

Common shorthand:
.item {
    flex: 1; /* commonly allows items to grow and share space */
}
15. CSS Grid

Grid is a two-dimensional layout system (rows and columns).
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: auto;
    gap: 20px;
}
Grid columns
.container {
    grid-template-columns: 200px 1fr 2fr;
}
Repeat
.container {
    grid-template-columns: repeat(3, 1fr);
}
Responsive grid
.container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
}
Grid placement
.item {
    grid-column: 1 / 3;
    grid-row: 1 / 3;
}
Named areas
.container {
    display: grid;
    grid-template-areas:
        "header header"
        "sidebar content"
        "footer footer";
    grid-template-columns: 200px 1fr;
}

.header {
    grid-area: header;
}

.sidebar {
    grid-area: sidebar;
}

.content {
    grid-area: content;
}

.footer {
    grid-area: footer;
}
16. Width and height
.box {
    width: 300px;
    height: 200px;
    min-width: 200px;
    max-width: 100%;
    min-height: 100px;
    max-height: 400px;
}

Useful responsive pattern:
.container {
    width: min(100% - 2rem, 1200px);
    margin-inline: auto;
}
17. Overflow
.box {
    overflow: visible;
    overflow: hidden;
    overflow: scroll;
    overflow: auto;
}

    visible: content may overflow.
    hidden: clips overflow.
    scroll: scrollbars are provided.
    auto: scrollbars when needed.

Separate axes:
.box {
    overflow-x: auto;
    overflow-y: hidden;
}
18. Borders, outlines, and shadows
.card {
    border: 1px solid #ddd;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

button:focus-visible {
    outline: 3px solid blue;
    outline-offset: 3px;
}

    border occupies box-model space.
    outline does not occupy box-model space.
    box-shadow adds a shadow around a box.
    border-radius rounds corners.

19. Opacity and visibility
.transparent {
    opacity: 0.5;
}

.invisible {
    visibility: hidden;
}

.removed {
    display: none;
}
Property	Space retained?	Visible?
opacity: 0	Yes	No
visibility: hidden	Yes	No
display: none	No	No

opacity also affects the appearance of descendants and can create a stacking context.
20. Transitions
.button {
    background-color: blue;
    transform: scale(1);
    transition: background-color 0.3s ease, transform 0.3s ease;
}

.button:hover {
    background-color: darkblue;
    transform: scale(1.05);
}

Syntax:
transition: property duration timing-function delay;

Common timing functions:

    ease
    linear
    ease-in
    ease-out
    ease-in-out

21. Transform
.box {
    transform: translateX(20px);
    transform: rotate(10deg);
    transform: scale(1.2);
    transform: skew(10deg);
}

Combine transforms:
.box {
    transform: translate(10px, 20px) rotate(5deg) scale(1.1);
}

Common functions:

    translate()
    translateX(), translateY()
    rotate()
    scale()
    skew()

22. Animations
.box {
    animation: move 2s ease-in-out infinite alternate;
}

@keyframes move {
    from {
        transform: translateX(0);
    }

    to {
        transform: translateX(100px);
    }
}

Animation properties:

    animation-name
    animation-duration
    animation-timing-function
    animation-delay
    animation-iteration-count
    animation-direction
    animation-fill-mode
    animation-play-state

Respect reduced-motion preferences:
@media (prefers-reduced-motion: reduce) {
    *,
    *::before,
    *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.01ms !important;
    }
}
23. Responsive design and media queries
.card {
    width: 50%;
}

@media (max-width: 768px) {
    .card {
        width: 100%;
    }
}

Mobile-first approach:
/* Base styles for smaller screens */
.container {
    display: grid;
    grid-template-columns: 1fr;
}

/* Larger screens */
@media (min-width: 768px) {
    .container {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (min-width: 1024px) {
    .container {
        grid-template-columns: repeat(3, 1fr);
    }
}

Media query examples:
@media (max-width: 600px) { }
@media (min-width: 768px) { }
@media (orientation: landscape) { }
@media (prefers-color-scheme: dark) { }

Breakpoints should be chosen based on when your layout needs to change, not just specific devices.
24. CSS variables (custom properties)
:root {
    --primary-color: #2563eb;
    --spacing: 16px;
    --border-radius: 8px;
}

.button {
    background-color: var(--primary-color);
    padding: var(--spacing);
    border-radius: var(--border-radius);
}

Fallback:
color: var(--text-color, black);

Custom properties usually inherit and can be changed at runtime.
25. Specificity and cascade

When multiple CSS rules apply, the browser considers cascade origin/layers, importance, specificity, and source order.

Simplified specificity comparison:

    Inline style
    ID selectors
    Class, attribute, and pseudo-class selectors
    Element and pseudo-element selectors

Example:
p {
    color: black;
}

.note {
    color: blue;
}

#special {
    color: red;
}
<p class="note" id="special">This text is red.</p>

Avoid overusing !important:
p {
    color: red !important;
}
26. Common CSS properties quick reference
Color and background
color: black;
background-color: white;
background-image: url("image.jpg");
Text
font-family: Arial, sans-serif;
font-size: 1rem;
font-weight: bold;
text-align: center;
line-height: 1.5;
text-decoration: underline;
Box
width: 100%;
max-width: 1200px;
padding: 1rem;
margin: 0 auto;
border: 1px solid black;
border-radius: 8px;
Layout
display: flex;
display: grid;
position: relative;
gap: 1rem;
Flex
justify-content: space-between;
align-items: center;
flex-direction: row;
flex-wrap: wrap;
Grid
grid-template-columns: repeat(3, 1fr);
grid-template-rows: auto;
grid-column: span 2;
Visual
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
opacity: 0.8;
overflow: hidden;
cursor: pointer;
27. Useful cursor values
button {
    cursor: pointer;
}

.disabled {
    cursor: not-allowed;
}

.text {
    cursor: text;
}

.resize {
    cursor: crosshair;
}

Common values: pointer, default, text, move, not-allowed, wait, grab, grabbing, crosshair.
28. Common beginner mistakes

    Forgetting the semicolon between declarations.
    Forgetting the closing brace }.
    Using # for a class instead of ..
    Using . for an ID instead of #.
    Confusing margin (outside) with padding (inside).
    Forgetting the box model when calculating width.
    Expecting top/`left` to work with static positioning.
    Confusing justify-content and align-items in Flexbox.
    Using z-index without understanding stacking contexts.
    Making fixed-width layouts that overflow on small screens.
    Overusing !important.
    Styling everything with IDs instead of reusable classes.
    Forgetting the viewport meta tag in HTML.

29. Starter CSS reset
*,
*::before,
*::after {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.5;
}

img,
video {
    max-width: 100%;
    height: auto;
}

button,
input,
textarea,
select {
    font: inherit;
}

This is a small starter reset—not a complete replacement for every browser default.
30. Mini layout patterns
Center a container
.container {
    width: min(100% - 2rem, 1100px);
    margin-inline: auto;
}
Center content with Flexbox
.center {
    display: flex;
    justify-content: center;
    align-items: center;
}
Center content with Grid
.center {
    display: grid;
    place-items: center;
}
Responsive card grid
.cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
}
Sticky header
header {
    position: sticky;
    top: 0;
    z-index: 10;
}
