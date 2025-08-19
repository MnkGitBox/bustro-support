# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **static HTML website** for the Bustro app support pages. The repository contains static HTML files that serve as support documentation and privacy policy for the Bustro Singapore bus timing app.

**Project Type**: Static HTML website (no build tools, frameworks, or package managers)

## Architecture & Structure

```
bustro-support/
├── index.html          # Main support page with FAQs and app information
├── privacy.html        # Privacy policy page
├── robot-banner.png    # Image asset for the site
└── CLAUDE.md          # This file
```

### Key Components

**index.html** (`/Users/malithkamburapola/Developer/Personal-apps/Bustro/Support-URLs/bustro-support/index.html:1`)
- Complete support documentation for Bustro app
- Interactive FAQ sections with JavaScript toggle functionality
- Comprehensive responsive CSS with light/dark mode support
- Covers all app features: live bus tracking, favorites, weather integration, MRT integration

**privacy.html** (`/Users/malithkamburapola/Developer/Personal-apps/Bustro/Support-URLs/bustro-support/privacy.html:1`)  
- Privacy policy documentation
- Same responsive design system as index.html
- Details data collection, usage, and user privacy controls

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