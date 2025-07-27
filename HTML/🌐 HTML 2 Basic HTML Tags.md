---
Date: 2025-07-13
tags:
  - HTML
  - Web Development
  - Frontend
---

# 🌐 HTML Handbook — Chapter 2: Basic HTML Tags

> **Learning Objectives:**
> - Understand HTML elements and attributes
> - Master basic text formatting tags
> - Learn semantic HTML structure
> - Practice with media elements
> - Build accessible and SEO-friendly content

---

## 📚 Table of Contents

1. [[#🧱 HTML Fundamentals]]
2. [[#📝 Text Structure Tags]]
3. [[#🔤 Text Formatting Tags]]
4. [[#🔗 Link & Navigation]]
5. [[#🖼️ Media Elements]]
6. [[#🎯 Semantic HTML]]
7. [[#🎨 Interactive Elements]]
8. [[#📊 Table Semantics]]
9. [[#🧪 Practice Exercises]]
10. [[#🎯 Best Practices]]

---

## 🧱 HTML Fundamentals

### What is an HTML Element?

An HTML element consists of:

```html
<tagname class="element-class"> content </tagname>
```

**Components:**
- **Opening tag**: `<tagname>`
- **Content**: Text, images, or other elements
- **Closing tag**: `</tagname>`
- **Attributes**: Additional information (optional)

### What are HTML Attributes?

Attributes provide extra information about elements:

```html
<a href="https://google.com" class="external-link" target="_blank" rel="noopener">Google</a>
```

**Common Attribute Types:**
- `class` - CSS styling
- `id` - Unique identifier
- `src` - Source URL
- `alt` - Alternative text
- `href` - Hyperlink reference

> 💡 **Best Practice**: Always use quotes around attribute values (`"` or `'`)

---

## 📝 Text Structure Tags

### Heading Tags (H1-H6)

HTML provides 6 levels of headings for document hierarchy:

```html
<h1 class="main-title" id="page-title">Main Title</h1>
<h2 class="section-heading">Subsection</h2>
<h3 class="subsection-heading">Sub-subsection</h3>
<h4 class="level-4-heading">Level 4</h4>
<h5 class="level-5-heading">Level 5</h5>
<h6 class="level-6-heading">Least important</h6>
```

**Key Rules:**
- Use only **one `<h1>`** per page
- Maintain proper hierarchy (h1 → h2 → h3)
- Important for SEO and accessibility

### Paragraph Tag

```html
<p class="content-paragraph" data-type="text">This is a paragraph of text.</p>
```

**Usage:**
- Blocks of text content
- Main content sections
- Article paragraphs

### Line & Spacing Elements

```html
<br class="line-break">        <!-- Line break -->
<hr class="divider">        <!-- Horizontal rule -->
<pre class="code-block">
  Line 1
    Line 2
</pre>      <!-- Preserves whitespace and newlines -->
```

---

## 🔤 Text Formatting Tags

### Semantic Formatting (Recommended)

| Tag | Purpose | Example |
|-----|---------|---------|
| `<strong>` | Important text | `<strong class="warning-text">Warning!</strong>` |
| `<em>` | Emphasized text | `<em class="note-text">Please note</em>` |
| `<mark>` | Highlighted text | `<mark class="highlight">Key term</mark>` |
| `<code>` | Inline code | `<code class="inline-code">console.log()</code>` |

### Stylistic Formatting (Use Sparingly)

```html
<b class="bold-text">Bold</b>          <!-- stylistic -->
<i class="italic-text">Italic</i>        <!-- stylistic -->
<u class="underline-text">Underline</u>
<del class="deleted-text">Deleted</del>
<small class="small-text">Small Text</small>
```

### Mathematical Notation

```html
<p class="chemical-formula">H<sub class="subscript">2</sub>O</p>       <!-- Subscript -->
<p class="mathematical-formula">E = mc<sup class="superscript">2</sup></p>  <!-- Superscript -->
```

> 🧠 **Accessibility Tip**: Prefer `<strong>` and `<em>` for semantic meaning. Use `<b>`/`<i>` only for purely visual emphasis.

---

## 🔗 Link & Navigation

### Anchor Tag

```html
<a href="https://google.com" class="external-link" target="_blank" rel="noopener">Visit Google</a>
```

**Common Attributes:**
- `href` - Destination URL
- `target="_blank"` - Open in new tab
- `rel="noopener"` - Security for external links
- `class` - Styling classes

**Link Types:**
- External links: `https://example.com`
- Internal links: `#section-id`
- Email links: `mailto:email@example.com`
- Phone links: `tel:+1234567890`

---

## 🖼️ Media Elements

### Image Tag

```html
<img src="image.jpg" alt="Description" width="200" height="150" class="responsive-image" loading="lazy">
```

**Essential Attributes:**
- `src` - Image source URL
- `alt` - Alternative text (accessibility)
- `width`/`height` - Dimensions
- `loading="lazy"` - Performance optimization

### Video Tag

```html
<video controls width="600" poster="thumbnail.jpg" class="video-player" preload="metadata">
  <source src="movie.mp4" type="video/mp4" class="video-source">
  <p class="fallback-text">Your browser does not support the video tag.</p>
</video>
```

**Key Attributes:**
- `controls` - Show playback controls
- `autoplay` - Start automatically
- `loop` - Repeat video
- `muted` - Default muted
- `poster` - Preview image
- `preload` - Metadata/auto/none

### Audio Tag

```html
<audio controls class="audio-player" preload="metadata">
  <source src="audio.mp3" type="audio/mpeg" class="audio-source">
  <p class="fallback-text">Your browser does not support the audio element.</p>
</audio>
```

**Key Attributes:**
- `controls` - Show playback controls
- `autoplay` - Start automatically
- `loop` - Continuous playback
- `muted` - Silence audio

### SVG Graphics

```html
<svg width="100" height="100" class="svg-graphic" viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="40" 
          stroke="green" stroke-width="4" fill="yellow" class="svg-circle" />
</svg>
```

**Common SVG Elements:**
- `<rect class="svg-rectangle">` - Rectangle
- `<circle class="svg-circle">` - Circle
- `<path class="svg-path">` - Custom shapes
- `<text class="svg-text">` - SVG text

---

## 🎯 Semantic HTML

### What are Semantic Tags?

Semantic HTML tags clearly define the meaning and structure of content, making your code more accessible and SEO-friendly.

> 🧠 **Why Semantic HTML?**
> - **Accessibility**: Screen readers understand your content better
> - **SEO**: Search engines can better index your content
> - **Maintainability**: Code is self-documenting and easier to understand
> - **Future-proof**: Standards-compliant and forward-compatible

### Sectioning Elements

#### Header & Navigation

```html
<header class="page-header" role="banner">
  <h1 class="site-title">My Website</h1>
  <nav class="main-navigation" role="navigation">
    <ul class="nav-list">
      <li class="nav-item"><a href="/" class="nav-link">Home</a></li>
      <li class="nav-item"><a href="/about" class="nav-link">About</a></li>
      <li class="nav-item"><a href="/contact" class="nav-link">Contact</a></li>
    </ul>
  </nav>
</header>
```

#### Main Content

```html
<main class="main-content" role="main">
  <article class="blog-post">
    <header class="article-header">
      <h2 class="article-title">How to Use Semantic HTML</h2>
      <time datetime="2024-01-15" class="publish-date">January 15, 2024</time>
    </header>
    <section class="article-content">
      <p class="article-paragraph">Your content here...</p>
    </section>
  </article>
</main>
```

#### Sidebar & Footer

```html
<aside class="sidebar" role="complementary">
  <section class="widget">
    <h3 class="widget-title">Related Posts</h3>
    <ul class="widget-list">
      <li class="widget-item"><a href="#" class="widget-link">Post 1</a></li>
    </ul>
  </section>
</aside>

<footer class="page-footer" role="contentinfo">
  <p class="copyright">&copy; 2024 My Website</p>
</footer>
```

### Content Grouping Elements

#### Article & Section

```html
<article class="content-article">
  <header class="article-header">
    <h2 class="article-title">Article Title</h2>
    <p class="article-meta">By <cite class="author">John Doe</cite></p>
  </header>
  
  <section class="article-section">
    <h3 class="section-title">Introduction</h3>
    <p class="section-content">Article content...</p>
  </section>
</article>
```

#### Blockquote & Figure

```html
<blockquote class="quote-block" cite="https://example.com">
  <p class="quote-text">This is an important quote that needs emphasis.</p>
  <footer class="quote-footer">
    <cite class="quote-author">— Famous Person</cite>
  </footer>
</blockquote>

<figure class="image-figure">
  <img src="image.jpg" alt="Description" class="figure-image">
  <figcaption class="figure-caption">This is the image caption</figcaption>
</figure>
```

### Text-Level Semantics

#### Emphasis & Importance

```html
<p class="content-text">
  This is <strong class="important-text">very important</strong> information.
  Please <em class="emphasized-text">pay attention</em> to this detail.
</p>
```

#### Code & Technical Terms

```html
<p class="code-example">
  Use the <code class="inline-code">console.log()</code> function to debug.
  The <var class="variable">x</var> variable stores the result.
</p>

<pre class="code-block"><code class="block-code">
function greet(name) {
  return `Hello, ${name}!`;
}
</code></pre>
```

#### Abbreviations & Citations

```html
<p class="abbreviation-example">
  <abbr title="HyperText Markup Language" class="abbreviation">HTML</abbr> 
  is the standard markup language.
</p>

<p class="citation-example">
  As mentioned in <cite class="citation">The Web Developer's Guide</cite>...
</p>
```

#### Time & Data

```html
<p class="time-example">
  The event starts at <time datetime="2024-02-15T19:00" class="event-time">7:00 PM</time>.
</p>

<p class="data-example">
  Product ID: <data value="12345" class="product-id">ABC-123</data>
</p>
```

---

## 🎨 Interactive Elements

### Details & Summary

```html
<details class="collapsible-section">
  <summary class="section-summary">Click to expand</summary>
  <div class="section-content">
    <p class="hidden-content">This content is hidden by default.</p>
  </div>
</details>
```

### Mark & Highlight

```html
<p class="search-result">
  Here is the <mark class="highlighted-text">search term</mark> you were looking for.
</p>
```

### Definition Lists

```html
<dl class="definition-list">
  <dt class="definition-term">HTML</dt>
  <dd class="definition-description">HyperText Markup Language</dd>
  
  <dt class="definition-term">CSS</dt>
  <dd class="definition-description">Cascading Style Sheets</dd>
</dl>
```

---

## 📊 Table Semantics

```html
<table class="data-table" role="table">
  <caption class="table-caption">Monthly Sales Report</caption>
  
  <thead class="table-header">
    <tr class="header-row">
      <th class="header-cell" scope="col">Month</th>
      <th class="header-cell" scope="col">Sales</th>
    </tr>
  </thead>
  
  <tbody class="table-body">
    <tr class="data-row">
      <td class="data-cell">January</td>
      <td class="data-cell">$1000</td>
    </tr>
  </tbody>
  
  <tfoot class="table-footer">
    <tr class="footer-row">
      <td class="footer-cell">Total</td>
      <td class="footer-cell">$1000</td>
    </tr>
  </tfoot>
</table>
```

---

## 🧪 Practice Exercises

### Exercise 1: Basic Page Structure
Create a web page with:
- One title using `<h1 class="main-title">`
- A paragraph `<p class="content">`
- A link to another site `<a href="#" class="external-link">`

### Exercise 2: Media Gallery
Add at least 5 images from the internet using `<img class="gallery-image">`

### Exercise 3: Text Formatting
Use `<br class="spacing">` and `<hr class="divider">` to create spacing

### Exercise 4: Mathematical Notation
Write the chemical equation: `<p class="formula">C + O<sub class="subscript">2</sub> = CO<sub class="subscript">2</sub></p>`

### Exercise 5: Article Writing
Try writing a short article using:
```html
<p class="article-text"> <b class="bold"> <em class="emphasis"> <mark class="highlight">
```

### Exercise 6: Video Player
Add a video with:
- Custom thumbnail (`poster` attribute)
- Playback controls
- Responsive width
```html
<video controls class="responsive-video" poster="thumbnail.jpg">
```

### Exercise 7: Audio Player
Create an audio player with:
- Loop functionality
- Fallback text for unsupported browsers
```html
<audio controls loop class="audio-player">
```

### Exercise 8: SVG Graphics
Draw a red square using SVG:
```html
<svg class="svg-container">
  <rect width="100" height="100" fill="red" class="red-square" />
</svg>
```

### Exercise 9: Logo Creation
Combine SVG and text to create a simple logo:
```html
<svg width="200" height="100" class="logo-container">
  <rect width="200" height="100" fill="#f0f0f0" class="logo-background" />
  <text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" class="logo-text">
    My Logo
  </text>
</svg>
```

### Exercise 10: Semantic Blog Post
Create a blog post structure:
```html
<article class="blog-post">
  <header class="post-header">
    <h1 class="post-title">Your Title</h1>
    <time datetime="2024-01-15" class="post-date">Date</time>
  </header>
  <section class="post-content">
    <p class="post-paragraph">Content...</p>
  </section>
</article>
```

---

## 🎯 Best Practices

### ✅ Do's:
- Use `<main>` only once per page
- Wrap navigation in `<nav>`
- Use `<article>` for self-contained content
- Use `<section>` for thematic grouping
- Add `role` attributes for accessibility
- Use semantic class names
- Always include `alt` attributes on images
- Use proper heading hierarchy (h1 → h2 → h3)
- Prefer `<strong>` and `<em>` for semantic meaning

### ❌ Don'ts:
- Don't use `<div>` when semantic tags exist
- Don't skip heading hierarchy
- Don't use `<b>` and `<i>` for importance
- Don't forget `alt` attributes on images
- Don't use tables for layout
- Don't use deprecated tags like `<font>` or `<center>`

### 🔧 Accessibility Guidelines:
- Use semantic HTML structure
- Include proper ARIA roles
- Provide alternative text for images
- Use descriptive link text
- Maintain proper heading hierarchy
- Ensure sufficient color contrast

### 📈 SEO Tips:
- Use descriptive page titles (h1)
- Include relevant keywords in headings
- Use semantic markup for better indexing
- Provide meta descriptions
- Use proper heading structure

---

## 📚 Additional Resources

- [MDN Web Docs - HTML Elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
- [W3Schools HTML Tutorial](https://www.w3schools.com/html/)
- [HTML5 Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)
- [Web Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)

---

> [[🧱 HTML 3 Creating a Page Layout|✅ Up Next: Chapter 3 — Creating a Page Layout →]]
