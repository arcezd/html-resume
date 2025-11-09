# GitHub Copilot Instructions for html-resume

## Project Overview

This is a single-page résumé template built purely with HTML and CSS that can be rendered into PDF through web browsers' print-to-PDF functionality. The project creates professional, ready-to-print résumés without requiring proprietary software.

**Key Characteristics:**
- Static HTML/CSS template with Handlebars templating syntax
- No build system, bundler, or compilation required
- No test infrastructure
- No package manager or dependencies to install
- Browser-based PDF generation workflow

## Repository Structure

```
.
├── .github/                    # GitHub configuration (you're here!)
├── default/                    # Main template directory
│   ├── lang/                  # Internationalization files
│   │   ├── en-US.json        # English translations
│   │   └── es-CR.json        # Spanish translations
│   ├── resume.html           # Main HTML template with Handlebars syntax
│   └── style.css             # All styling for the resume
├── demo.json                  # Example resume data structure
├── firefox_result.pdf         # Example output PDF
├── README.md                  # Project documentation
├── LICENSE                    # Apache License
└── .gitignore                # Git ignore patterns

```

## Technology Stack

### Core Technologies
- **HTML5**: Structure and content
- **CSS3**: Styling and layout (using modern features like CSS variables, flexbox, calc())
- **Handlebars**: Templating syntax (note: template is NOT compiled, used as reference/pattern)

### External Dependencies (CDN-loaded)
- **Normalize.css** (v8.0.1): CSS reset via CDN
- **Font Awesome** (v6.6.0): Icon fonts via CDN
- **Google Fonts**: Open Sans, Source Code Pro, Source Sans Pro

### Browser Targets
- Firefox (56+) on macOS
- Google Chrome (61+) on macOS
- Potentially other modern browsers supporting CSS calc(), var(), and flexbox

## How to Work with This Project

### Understanding the Template System

The `resume.html` file uses **Handlebars-like template syntax** but is NOT actually compiled. The syntax serves as a pattern/reference showing how data should be structured. Key patterns:

```handlebars
{{#with info}}                    # Access nested object
  {{firstname}} {{lastname}}      # Simple variable interpolation
{{/with}}

{{#each experience}}              # Loop over arrays
  {{position}}                    # Access array item properties
{{/each}}

{{#if projects}}                  # Conditional rendering
  <section>...</section>
{{/if}}

{{ i18n 'experience_title' }}     # i18n function (references lang/*.json)
{{ monthYearDate since }}         # Date formatting helper
{{ onlyYearDate issueDate }}      # Year-only date helper
{{ shortDate expirationDate }}    # Short date format helper
```

### Editing the Resume

1. **Modify Content**: Edit `default/resume.html` to change structure and content
2. **Style Changes**: Edit `default/style.css` to adjust appearance
3. **Data Structure**: Use `demo.json` as reference for data schema
4. **Translations**: Modify `default/lang/en-US.json` or `default/lang/es-CR.json` for labels

### Key CSS Variables (in style.css)

The template uses CSS custom properties for easy customization:

```css
--page-width: 8.5in;              # Letter size width
--page-height: 11in;              # Letter size height
--main-width: 6.5in;              # Main content area
--sidebar-width: calc(...)        # Sidebar (calculated)
--decorator-border-width: 1px;    # Timeline decorator
--row-blocks-padding-top: 6pt;    # Spacing
```

### Testing Changes

**No automated tests exist.** All testing is manual and visual.

#### Manual Testing Process:
1. Edit the HTML/CSS files
2. Open `default/resume.html` directly in browser (file:/// protocol works)
3. Visually inspect the layout and styling
4. Test print-to-PDF functionality

#### Print-to-PDF Instructions:

**Firefox:**
- Remove page margins in about:config
- Uncheck "Ignore Scaling and Shrink To Fit Page Width"
- Check "Print Background Colors"
- Clear headers and footers
- Save as PDF

**Chrome:**
- Set Margin to "None"
- Enable "Print Background Graphics"
- Disable headers and footers
- Save as PDF

**Important Notes:**
- No hyperlinks work in rendered PDFs (limitation of print-to-PDF)
- Sidebar may not reach page edge due to printer no-print areas
- Test that text isn't clipped and items haven't unexpectedly shrunk

## Common Tasks

### Adding a New Section

1. Copy an existing section structure from `resume.html`
2. Modify the Handlebars template syntax to match your data
3. Add corresponding CSS styling in `style.css` if needed
4. Test in browser

### Changing Paper Size

Currently supports letter portrait only. To add A4:
- Modify CSS `@page` rule in `style.css`
- Adjust `--page-width` and `--page-height` variables
- Test print output

### Adding Icons

Use Font Awesome icon classes (loaded via CDN):
```html
<i class="fas fa-suitcase"></i>     <!-- Solid style -->
<i class="fab fa-github"></i>       <!-- Brands style -->
```

Browse available icons at: https://fontawesome.com/icons

### Internationalization

To add a new language:
1. Create `default/lang/[locale].json` (e.g., `fr-FR.json`)
2. Copy structure from `en-US.json`
3. Translate all label values
4. Reference in template using `{{ i18n 'key_name' }}`

## Important Constraints and Limitations

### What You CANNOT Do:
- **No JavaScript execution**: Template is pure HTML/CSS, no JS processing
- **No dynamic functionality**: All content must be hardcoded or use static template syntax
- **No hyperlinks in PDF**: Browser print-to-PDF flattens everything
- **No build process**: Don't add webpack, npm scripts, or compilation steps
- **No automated testing**: Don't add test frameworks

### Browser Compatibility Hacks

Check `default/resume.html` and `default/style.css` for browser-specific comments. Some CSS features require specific browser support:
- CSS `calc()` function
- CSS custom properties (`var()`)
- Flexbox layout

## Making Changes

### Best Practices:
1. **Preserve simplicity**: This is intentionally a no-build project
2. **Test in multiple browsers**: Firefox and Chrome at minimum
3. **Check print output**: Always test print-to-PDF after changes
4. **Maintain accessibility**: Keep semantic HTML structure
5. **Keep file:// compatibility**: No features requiring a web server

### Style Guide:
- CSS: Use existing CSS variable naming convention
- HTML: Maintain semantic structure with proper heading hierarchy
- Indentation: Consistent 2-space indentation
- Comments: Inline comments for browser-specific hacks

## Troubleshooting

### Common Issues:

**Text clipped in PDF:**
- Check CSS padding/margins
- Verify `@page` size matches paper size
- Test with different browser print settings

**Fonts not displaying:**
- Verify Google Fonts CDN links are working
- Check internet connection (CDN dependencies)

**Icons not showing:**
- Verify Font Awesome CDN link is current version
- Check icon class names against FA documentation

**Layout broken:**
- Validate CSS syntax
- Check CSS variable dependencies
- Test in different browsers for compatibility

### No Errors to Document
As of initial exploration, no errors were encountered. The repository is in a working state with:
- Clean file structure
- Valid HTML/CSS
- Working example (firefox_result.pdf demonstrates successful output)

## Quick Start for Copilot Agents

When working on this repository:

1. **Understand**: This is a static template, no build/compile needed
2. **Edit carefully**: Direct HTML/CSS changes, test in browser
3. **Don't add complexity**: No npm, webpack, or build tools
4. **Test manually**: Open file in browser and use print-to-PDF
5. **Preserve simplicity**: The no-build nature is a feature, not a bug

## Additional Resources

- **Project Blog Post**: https://blogs.purincess.tw/matrixblog/2016/04/typesetting-resume-with-html-and-css/
- **Author's Example**: https://mnjul.net/cv/resume.pdf
- **Font Awesome Icons**: https://fontawesome.com/icons
- **Google Fonts**: https://fonts.google.com/

## License

Apache License - Feel free to create derivative templates and share with others.
