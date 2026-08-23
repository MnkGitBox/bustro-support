# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **static HTML website** for the Bustro app support pages. The repository contains static HTML files that serve as support documentation and privacy policy for the Bustro Singapore bus timing app.

**Project Type**: Static HTML website (no build tools, frameworks, or package managers)

## Architecture & Structure

```
bustro-support/                 # served at https://bustro.app
├── index.html          # Landing page: download the app, carries the Open Graph tags
├── help.html           # Help centre, English
├── help.ms.html        # Help centre, Malay
├── help.ta.html        # Help centre, Tamil
├── help.zh-Hans.html   # Help centre, Simplified Chinese
├── index.ms.html       # Redirect stub -> help.ms.html (see below)
├── index.ta.html       # Redirect stub -> help.ta.html
├── index.zh-Hans.html  # Redirect stub -> help.zh-Hans.html
├── privacy.html        # Privacy policy
├── terms.html          # Terms & conditions
├── privacy-v2.html     # Redirect stub -> privacy.html
├── terms-v2.html       # Redirect stub -> terms.html
├── 404.html            # Serves every unmatched path, including shared /stop/* and /service/* links
├── CNAME               # bustro.app
├── .nojekyll           # Without it Jekyll skips .well-known/ and Universal Links break
├── .well-known/apple-app-site-association
├── assets/
└── CLAUDE.md           # This file
```

### Filenames are an API — rename only behind a redirect

The iOS app hardcodes these paths in `AppMenuFeature/Sources/LinkDestination.swift`, and every
build already installed keeps pointing at whatever it shipped with. Deleting or renaming a page
outright breaks Help for users who have not updated, permanently for anyone who never does.

The help centre was `index*.html` until the bare domain became the download page. The three
`index.<lang>.html` files that remain are redirect stubs, not content — they exist solely so older
builds still land on the right page, and they carry `noindex` so search engines follow the
canonical. Do not delete them, and do not add content to them.

`privacy-v2.html` and `terms-v2.html` are stubs of the same kind, left behind when those pages
dropped the suffix.

### Key Components

**index.html** — landing page. The only page with Open Graph tags, since it is the URL people paste
and the one that returns HTTP 200. Links to the help centre near the top: builds shipped before it
existed open `/` when the user taps Help.

**help.html**, **help.ms.html**, **help.ta.html**, **help.zh-Hans.html**
- Complete support documentation for the Bustro app
- Interactive FAQ sections with JavaScript toggle functionality
- Responsive CSS with light/dark mode support

**privacy.html**, **terms.html**
- Legal pages, same design system as the help centre

## Development Approach

### CSS Architecture
Both HTML files use:
- **CSS custom properties** with `light-dark()` function for theme support
- **Mobile-first responsive design** with multiple breakpoint ranges:
  - Very small phones: 0-480px
  - Standard mobile: 481-768px  
  - Tablets: 769-1024px
  - Large screens: 1025px+
- **Fallback dark mode** using `@media (prefers-color-scheme: dark)`

### JavaScript Functionality
- Simple vanilla JavaScript for FAQ accordion behavior in index.html
- No external libraries or frameworks
- Progressive enhancement approach

## Content Management

### FAQ Structure
FAQs in index.html follow this pattern:
```html
<div class="faq-item">
    <h3 class="faq-question" onclick="toggleFAQ(this)">Question text?</h3>
    <div class="faq-answer">
        <p>Answer content...</p>
    </div>
</div>
```

### App Information
The support content is comprehensive and covers:
- Live bus tracking features
- Location services and permissions
- iCloud sync functionality
- MRT integration
- Weather integration via Apple WeatherKit
- Singapore-specific transport information

## Maintenance Notes

- **No build process**: Files can be edited directly
- **Static hosting ready**: Designed for simple web hosting
- **Self-contained**: No external dependencies beyond standard web technologies
- **Singapore-focused**: Content specifically tailored for Singapore users and transport system

## Git Workflow

Current branch: `chore/localize`
Main branch: `main`

Recent changes focused on:
- Mobile responsiveness improvements
- Content updates for app version 1.1.0
- Addition of robot banner asset