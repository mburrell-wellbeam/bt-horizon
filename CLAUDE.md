# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Horizon is a Shopify theme built with Liquid templates, vanilla JavaScript web components, and CSS. It's a flagship first-party theme emphasizing web-native development, server-rendered HTML, and progressive enhancement without external dependencies.

## Development Commands

### Theme Development
```bash
# Start development server (using Shopify CLI)
shopify theme dev

# Check theme for errors
shopify theme check

# Push theme to development store
shopify theme push

# Pull theme from store
shopify theme pull
```

## Architecture

### Component Framework
The theme uses a custom web component framework (`assets/component.js`) that extends `DeclarativeShadowElement`. Components:
- Use `ref` attributes for element references 
- Support declarative event handlers with `on:click="/methodName"`
- Automatically manage refs through mutation observers
- Follow strict typing with JSDoc annotations

### File Structure
- **assets/**: JavaScript components, CSS, and SVG icons (flat directory, no subdirectories)
- **blocks/**: Reusable Liquid blocks for sections
- **sections/**: Page sections with schema definitions
- **snippets/**: Reusable Liquid partials
- **templates/**: JSON templates defining page structures
- **locales/**: Internationalization JSON files

### JavaScript Standards
- **No external dependencies** - Only native browser APIs
- **Component-based architecture** - All interactive elements extend the Component class
- **Event-driven communication** - Components communicate via custom events
- **Async/await over promises** - Always use async/await syntax
- **JSDoc type annotations** - Required for all components and methods

### Liquid Patterns
- Server-side rendering with Liquid templates
- Theme blocks for customizable sections
- Settings schemas for merchant customization
- Translations via `locales/*.json` files

## Key Development Principles

1. **Web-native approach**: Use modern browser features with progressive enhancement for older browsers
2. **Performance first**: Lean, fast, reliable code - functionality defaults to "no" until justified
3. **Server-rendered**: Business logic and platform primitives stay on the server
4. **Type safety**: Use JSDoc annotations and enable checkJs in jsconfig.json
5. **Accessibility**: Follow WCAG guidelines (see `.cursor/rules/*-accessibility.mdc`)

## Testing and Validation

Run `shopify theme check` before committing changes to validate:
- Liquid syntax
- Theme best practices  
- Performance issues
- Accessibility concerns

## Component Communication

- **Parent to child**: Direct method invocation via refs
- **Child to parent**: Custom events with typed details
- **Cross-component**: Document-level event listeners

## URL and State Management

Always use URL and URLSearchParams APIs for URL manipulation. Use History API for client-side navigation without full page reloads.