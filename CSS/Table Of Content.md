---
tags:
  - css
  - toc
  - "#needs_review"
date: 2025-07-21
---
# 🧭 CSS Learning Notes - Comprehensive Table of Contents

Based on my research of modern CSS learning resources and best practices, here is a detailed table of contents for your CSS learning notes that progresses from fundamental concepts to advanced techniques:

## 📚 CSS Learning Notes - Complete Table of Contents

### **Part I: 💎 CSS Fundamentals (Beginner)**

#### **1. 🏁 [[1. CSS Introduction & Setup|CSS Introduction & Setup]]**
- What is CSS and its role in web development
- CSS evolution from CSS1 to CSS3
- Importance of CSS in separating content from presentation
- Setting up development environment and CSS editors
- Including CSS in HTML (inline, internal, external)
- CSS validation and browser-specific prefixes
- Cross-browser testing fundamentals

#### **2. 📖 [[2. CSS Syntax & Core Concepts|CSS Syntax & Core Concepts]]**
- CSS syntax structure (selectors, properties, values)
- CSS rules and declaration blocks
- Understanding keywords (auto, multiple, string)
- CSS comments and code organization
- Basic CSS example walkthrough

#### **3. 👉 [[3. CSS Selectors Fundamentals|CSS Selectors Fundamentals]]**
- **Basic Selectors:**
  - Universal selector (`*`)
  - Type/Element selectors (`h1`, `p`, `div`)
  - Class selectors (`.className`)
  - ID selectors (`#idName`)
  - Grouping selectors
- **Attribute Selectors:**
  - Exact match (`[attribute="value"]`)
  - Contains word (`[attribute~="value"]`)
  - Starts with (`[attribute^="value"]`)
  - Ends with (`[attribute$="value"]`)
  - Contains substring (`[attribute*="value"]`)
- **Combinator Selectors:**
  - Descendant combinator (space)
  - Child combinator (`>`)
  - Adjacent sibling (`+`)
  - General sibling (`~`)

#### **4. 🌊 [[4. CSS Specificity & Cascade|CSS Specificity & Cascade]]**
- Understanding specificity hierarchy
- Inline styles vs IDs vs Classes vs Elements
- CSS cascade and inheritance
- Using `!important` and when to avoid it
- CSS inheritance principles

#### **5. 🎨 [[5. Colors & Backgrounds|Colors & Backgrounds]]**
- **Color Values:**
  - Named colors (`red`, `blue`)
  - Hex codes (`#FF0000`, `#F00`)
  - RGB/RGBA (`rgb(255,0,0)`, `rgba(255,0,0,0.5)`)
  - HSL/HSLA (`hsl(0,100%,50%)`)
- **Background Properties:**
  - Background color
  - Background images
  - Background position, repeat, size, attachment
  - **Gradients:**
    - Linear gradients
    - Radial gradients
    - Conic gradients

#### **6. ✒️ [[6. Typography & Text Styling|Typography & Text Styling]]**
- **Font Properties:**
  - Font families and web-safe fonts
  - Google Fonts integration
  - Font size, weight, style
  - Line height and letter spacing
- **Text Properties:**
  - Text alignment, decoration, transform
  - Text spacing and indentation
  - Word break and text overflow
  - Text shadows

### **Part II: 📐 Layout Foundations (Intermediate)**

#### **7. 📦 [[7. CSS Box Model|CSS Box Model]]**
- Understanding the box model concept
- Content, padding, border, margin
- Box-sizing property (`content-box` vs `border-box`)
- Outline vs border differences
- Box model calculations and debugging

#### **8. 📏 [[8. CSS Units & Sizing|CSS Units & Sizing]]**
- **Absolute Units:**
  - Pixels (`px`)
  - Points (`pt`), centimeters (`cm`)
- **Relative Units:**
  - Em (`em`) - relative to element font-size
  - Rem (`rem`) - relative to root font-size
  - Percentage (`%`) - relative to parent
  - Viewport units (`vw`, `vh`, `vmin`, `vmax`)
- **When to use each unit type**

#### **9. 🖼️ [[9. Display Properties|Display Properties]]**
- Block vs inline vs inline-block
- Display none vs visibility hidden
- Display table and table-cell
- Display flex (introduction)
- Display grid (introduction)

#### **10. 📍 [[10. CSS Positioning|CSS Positioning]]**
- **Position Types:**
  - Static (default)
  - Relative positioning
  - Absolute positioning
  - Fixed positioning
  - Sticky positioning
- Z-index and stacking context
- Positioning best practices and use cases

#### **11. 🏊 [[11. Float, Clear & Overflow|Float, Clear & Overflow]]**
- Understanding float behavior
- Float left, right, and none
- Clear property (left, right, both)
- Overflow property (visible, hidden, scroll, auto)
- **Block Formatting Context (BFC):**
  - Creating BFC with overflow
  - Modern alternative: `display: flow-root`
- Clearfix techniques

### **Part III: 🍱 Modern Layout Systems (Intermediate-Advanced)**

#### **12. 💪 [[12. Flexbox Layout System|Flexbox Layout System]]**
- **Flex Container Properties:**
  - `display: flex`
  - `flex-direction` (row, column, reverse)
  - `flex-wrap` (nowrap, wrap, wrap-reverse)
  - `flex-flow` (shorthand)
  - `justify-content` (alignment on main axis)
  - `align-items` (alignment on cross axis)
  - `align-content` (multi-line alignment)
  - `gap` (spacing between items)
- **Flex Item Properties:**
  - `order` (visual reordering)
  - `flex-grow` (growth factor)
  - `flex-shrink` (shrink factor)
  - `flex-basis` (initial size)
  - `flex` (shorthand)
  - `align-self` (individual alignment)
- **Flexbox Patterns:**
  - Centering content
  - Navigation bars
  - Equal height columns
  - Flexible card layouts

#### **13. ▦ [[13. CSS Grid Layout System|CSS Grid Layout System]]**
- **Grid Container Properties:**
  - `display: grid`
  - `grid-template-rows` and `grid-template-columns`
  - `grid-template-areas` (named areas)
  - `grid-gap` / `gap` (spacing)
  - `justify-items` and `align-items`
  - `justify-content` and `align-content`
- **Grid Item Properties:**
  - `grid-row` and `grid-column` (positioning)
  - `grid-area` (named area assignment)
  - `justify-self` and `align-self`
- **Advanced Grid Features:**
  - Fractional units (`fr`)
  - `repeat()` function
  - `minmax()` function
  - Auto-placement algorithm
  - **Subgrid** (modern feature)

#### **14. 📱 [[14. Responsive Design|Responsive Design]]**
- **Media Queries:**
  - Syntax and structure
  - Common breakpoints
  - Mobile-first vs desktop-first approach
  - Print styles
- **Responsive Units:**
  - Viewport-relative units
  - Flexible sizing strategies
- **Responsive Images:**
  - `max-width: 100%` technique
  - Picture element integration
- **Modern Responsive Features:**
  - **Container Queries** (2025 feature)
  - Intrinsic web design principles

### **Part IV: ✨ Visual Effects & Animations (Advanced)**

#### **15. ✨ [[15. Borders, Shadows & Visual Effects|Borders, Shadows & Visual Effects]]**
- **Border Properties:**
  - Border width, style, color
  - Border radius for rounded corners
  - Border images (advanced)
- **Box Shadows:**
  - Basic shadow syntax
  - Multiple shadows
  - Inset shadows
  - Creative shadow effects
- **Text Shadows:**
  - Basic text shadow
  - Glowing text effects
- **Advanced Visual Effects:**
  - **CSS Filters:**
    - `blur()`, `grayscale()`, `sepia()`
    - `drop-shadow()`, `brightness()`
  - **Blend Modes:**
    - `mix-blend-mode`
    - `background-blend-mode`
  - **Clipping and Masking:**
    - `clip-path` for custom shapes
    - `mask-image` for layered effects

#### **16. 🔄 [[16. CSS Transforms|CSS Transforms]]**
- **2D Transforms:**
  - `translateX()`, `translateY()`, `translate()`
  - `rotate()` for rotation
  - `scale()`, `scaleX()`, `scaleY()`
  - `skew()`, `skewX()`, `skewY()`
- **3D Transforms:**
  - `translateZ()`, `translate3d()`
  - `rotateX()`, `rotateY()`, `rotateZ()`
  - `perspective` property
  - `transform-style: preserve-3d`
- **Transform Optimization:**
  - Hardware acceleration benefits
  - Performance considerations

#### **17. ⏯️ [[17. CSS Transitions|CSS Transitions]]**
- **Transition Properties:**
  - `transition-property`
  - `transition-duration`
  - `transition-timing-function`
  - `transition-delay`
  - `transition` (shorthand)
- **Timing Functions:**
  - Ease, linear, ease-in, ease-out
  - `cubic-bezier()` custom curves
- **Practical Applications:**
  - Hover effects
  - Smooth state changes
  - Loading animations

#### **18. 🎬 [[18. CSS Animations|CSS Animations]]**
- **Animation Properties:**
  - `@keyframes` rule creation
  - `animation-name`
  - `animation-duration`
  - `animation-timing-function`
  - `animation-delay`
  - `animation-iteration-count`
  - `animation-direction`
  - `animation-fill-mode`
  - `animation-play-state`
  - `animation` (shorthand)
- **Advanced Animation Techniques:**
  - Keyframe optimization
  - Performance best practices
  - Complex multi-step animations

### **Part V: 🚀 Advanced CSS Features (Expert)**

#### **19. 🔍 [[19. Modern CSS Selectors & Pseudo-classes|Modern CSS Selectors & Pseudo-classes]]**
- **Advanced Pseudo-classes:**
  - `:nth-child()`, `:nth-of-type()`
  - `:first-child`, `:last-child`
  - `:only-child`, `:empty`
  - `:focus-within`, `:focus-visible`
  - **`:has()` - Parent Selector (2025)**
- **Pseudo-elements:**
  - `::before` and `::after`
  - `::first-line`, `::first-letter`
  - `::selection`
  - `::placeholder`
  - `::backdrop` (modern feature)
- **State-based Selectors:**
  - `:hover`, `:active`, `:focus`
  - `:visited`, `:target`
  - `:disabled`, `:checked`

#### **20. 🔧 [[20. CSS Variables (Custom Properties)|CSS Variables (Custom Properties)]]**
- **Variable Declaration and Usage:**
  - `:root` scope for global variables
  - Local variable scoping
  - `var()` function with fallbacks
- **Dynamic Variables:**
  - JavaScript integration
  - Theme switching
  - Responsive variables
- **Advanced Patterns:**
  - Component-based variables
  - Calculations with variables
  - **`@property` registration (2025)**

#### **21. 🧮 [[21. CSS Functions & Calculations|CSS Functions & Calculations]]**
- **Mathematical Functions:**
  - `calc()` for dynamic calculations
  - `min()`, `max()`, `clamp()` for responsive sizing
  - `round()`, `mod()`, `rem()` (modern functions)
- **Color Functions:**
  - `color-mix()` for color blending
  - `color-contrast()` for accessibility
  - **Relative Color Syntax (2025)**
- **Layout Functions:**
  - `repeat()` in Grid
  - `minmax()` for flexible sizing
  - `fit-content()` for optimal sizing

#### **22. 🆕 [[22. Modern CSS Layout Features (2025)|Modern CSS Layout Features (2025)]]**
- **CSS Nesting (Native)**
  - Nested selectors syntax
  - Benefits over preprocessors
- **Container Queries**
  - Container-based responsive design
  - `@container` rule syntax
- **CSS Subgrid**
  - Inheriting parent grid definitions
  - Advanced layout patterns
- **CSS Layers (`@layer`)**
  - Organizing CSS specificity
  - Managing large codebases
- **Anchor Positioning**
  - Tooltip and popup positioning
  - Dynamic element alignment

### **Part VI: 🛠️ Applied CSS & Workflows**

#### **23. 🏛️ [[23. CSS Methodologies|CSS Methodologies]]**
- **BEM (Block Element Modifier):**
  - Naming conventions
  - Component structure
  - Scalability benefits
- **OOCSS (Object-Oriented CSS):**
  - Separating structure from skin
  - Container/content separation
- **SMACSS (Scalable and Modular Architecture):**
  - Base, layout, module, state, theme rules
- **ITCSS (Inverted Triangle CSS):**
  - CSS organization by specificity

#### **24. ⚙️ [[24. CSS Preprocessors|CSS Preprocessors]]**
- **Sass/SCSS:**
  - Variables and nesting
  - Mixins and functions
  - Inheritance (`@extend`)
  - Control directives
  - Sass vs SCSS syntax
- **Less:**
  - JavaScript-based compilation
  - Variable syntax differences
  - Mixin capabilities
- **Stylus:**
  - Flexible syntax options
  - Built-in functions
- **Modern Alternatives:**
  - Native CSS nesting
  - CSS custom properties
  - PostCSS ecosystem

#### **25. 🏗️ [[25. CSS Frameworks|CSS Frameworks]]**
- **Bootstrap:**
  - Component-based approach
  - Grid system
  - Pre-built components
  - Customization options
- **Tailwind CSS:**
  - Utility-first methodology
  - Configuration and customization
  - Responsive utilities
  - Build optimization
- **Framework Comparison:**
  - Use case scenarios
  - Learning curves
  - Performance implications

#### **26. ⚡ [[26. Performance Optimization|Performance Optimization]]**
- **CSS Performance Best Practices:**
  - Efficient selector strategies
  - Minimizing repaints and reflows
  - Hardware acceleration techniques
- **CSS Minification:**
  - File size optimization
  - Build process integration
- **Critical CSS:**
  - Above-the-fold optimization
  - Loading strategies
- **Modern Loading Techniques:**
  - CSS containment
  - `content-visibility` property

#### **27. 📝 [[27. Form Styling|Form Styling]]**
- **Input Elements:**
  - Text inputs styling
  - Focus states and accessibility
  - **`accent-color` for native controls (2025)**
  - **`field-sizing` property (2025)**
- **Advanced Form Styling:**
  - Custom checkboxes and radio buttons
  - File upload styling
  - Range slider customization
- **Form Validation Styling:**
  - `:valid` and `:invalid` pseudo-classes
  - Error state design patterns

#### **28. ♿ [[28. CSS Accessibility (A11y)|CSS Accessibility (A11y)]]**
- **Focus Management:**
  - Visible focus indicators
  - Skip links
  - Focus trapping
- **Screen Reader Support:**
  - `.sr-only` utility classes
  - Semantic color usage
- **Color Contrast:**
  - WCAG compliance
  - High contrast mode support
- **Motion Accessibility:**
  - `prefers-reduced-motion`
  - Respecting user preferences

#### **29. 🖨️ [[29. CSS for Print & Multi-Media|CSS for Print & Multi-Media]]**
- **Print Styles:**
  - `@media print` queries
  - Page break control
  - Print-specific typography
- **Dark Mode Support:**
  - `prefers-color-scheme`
  - Theme switching patterns
  - Variable-based theming

#### **30. 🐞 [[30. CSS Debugging & Development Tools|CSS Debugging & Development Tools]]**
- **Browser Developer Tools:**
  - CSS inspection techniques
  - Live editing capabilities
  - Performance profiling
- **CSS Debugging Strategies:**
  - Visual debugging techniques
  - Common issues and solutions
- **CSS Linting:**
  - Code quality tools
  - Style consistency

### **Part VII: 🔮 The Future & The Ecosystem**

#### **31. 🧪 [[31. Experimental CSS Features (2025+)|Experimental CSS Features (2025+)]]**
- **CSS Houdini:**
  - Custom properties API
  - Paint worklets
  - Layout API
- **View Transitions API:**
  - Smooth page transitions
  - Animation coordination
- **CSS Scope (`@scope`)**
  - Style isolation
  - Component encapsulation
- **Interpolate Size**
  - Responsive sizing animations

#### **32. 🕺 [[32. CSS Animation Libraries & Frameworks|CSS Animation Libraries & Frameworks]]**
- **Animation Libraries:**
  - CSS animation frameworks
  - Integration strategies
- **Motion Design Principles:**
  - Easing and timing
  - Choreography in web design

#### **33. 👨‍💻 [[33. CSS-in-JS & Modern Workflows|CSS-in-JS & Modern Workflows]]**
- **CSS-in-JS Approaches:**
  - Styled-components
  - Emotion
  - CSS Modules
- **Build Tools Integration:**
  - Webpack CSS handling
  - PostCSS plugins
  - CSS optimization tools

### **Part VIII: 🏗️ Practical Application**

#### **34. 💡 [[34. Project-Based Learning|Project-Based Learning]]**
- **Card Design Systems:**
  - Component variations
  - State management
- **Responsive Navigation:**
  - Mobile-first menus
  - Progressive enhancement
- **Grid Gallery Layouts:**
  - Masonry-style layouts
  - Image optimization
- **Form Design Patterns:**
  - Multi-step forms
  - Validation UX

#### **35. 📂 [[35. CSS Code Organization|CSS Code Organization]]**
- **File Structure:**
  - Modular CSS architecture
  - Import strategies
- **Documentation:**
  - CSS commenting standards
  - Style guide creation
- **Maintenance:**
  - Refactoring techniques
  - Legacy code management

### **Part IX: 📚 Resources & Reference**

#### **36. 🔖 [[36. CSS Reference & Quick Guides|CSS Reference & Quick Guides]]**
- **Property Reference:**
  - Common properties quick reference
  - Value types and syntax
- **Browser Compatibility:**
  - Feature support tables
  - Fallback strategies
- **CSS Resources:**
  - Documentation sources
  - Community resources
  - Learning platforms


---
← [[36. CSS Reference & Quick Guides.md|CSS Reference & Quick Guides]] | [[1. CSS Introduction & Setup.md|CSS Introduction & Setup]] →
