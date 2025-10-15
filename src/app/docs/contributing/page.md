---
title: Contributing
nextjs:
  metadata:
    title: Contributing
    description: Guidelines for contributing to Walker's documentation.
---

# To Walker Documentation

Thank you for your interest in improving Walker's documentation!

## Documentation Structure

The documentation is organized into the following files:

- `page.md` - Documentation overview and index
- `docs/installation/page.md` - Installation instructions for all platforms
- `docs/getting-started/page.md` - Basic usage and first steps
- `docs/configuration/page.md` - Complete configuration reference
- `docs/providers/page.md` - Available providers and their features
- `docs/provider-actions/page.md` - Detailed action reference
- `docs/keybindings/page.md` - Keyboard shortcuts and customization
- `docs/theming/page.md` - Theming guide with CSS and layouts
- `docs/advanced-usage/page.md` - Advanced features and use cases

## How to Contribute

### Reporting Issues

If you find errors, outdated information, or missing content:

1. Check if an issue already exists
2. Open a new issue describing the problem
3. Include:
   - Which document has the issue
   - What's incorrect or missing
   - Suggestions for improvement (if any)

### Improving Documentation

1. Fork the repository
2. Edit the relevant `.md` file in `src/app/docs/`
3. Follow the style guide below
4. Test that links work
5. Submit a pull request

## Style Guide

### Formatting

- Use clear, concise language
- Write in second person ("you can", not "one can")
- Use present tense
- Break up long paragraphs
- Use code blocks for commands and config examples
- Use tables for structured information

### Code Examples

Use fenced code blocks with language hints:

````markdown
```bash
walker --gapplication-service
```

```toml
theme = "default"
```

```css
.item-box {
  padding: 10px;
}
```
````

### Headings

- Use ATX-style headings (`#`, `##`, etc.)
- One H1 per document (title)
- Logical hierarchy (don't skip levels)
- Capitalize first word only (except proper nouns)

### Links

- Use relative links for internal docs: `[Configuration](/docs/configuration)`
- Use full URLs for external links
- Check that all links work

### Examples

- Provide practical, real-world examples
- Show both basic and advanced usage
- Include expected output when relevant
- Use comments to explain complex examples

## Testing Changes

Before submitting:

1. **Check formatting:** Ensure markdown renders correctly
2. **Test links:** All internal and external links work
3. **Verify accuracy:** Information matches current Walker version
4. **Check consistency:** Terminology matches other docs

## Documentation Standards

### Accuracy

- Test all commands and configurations
- Reference the latest Walker version
- Note if features are version-specific
- Update screenshots if UI changed

### Completeness

- Cover common use cases
- Include troubleshooting tips
- Provide examples for each feature
- Link to related documentation

### Clarity

- Define technical terms
- Explain the "why" not just the "how"
- Use consistent terminology
- Add visual aids (tables, lists) where helpful

## Versioning

Documentation should match the latest stable Walker release. If documenting unreleased features:

- Clearly mark as "development version"
- Note the target version
- Consider a separate branch

## Contact

- GitHub Issues: [https://github.com/abenz1267/walker/issues](https://github.com/abenz1267/walker/issues)
- Discord: [https://discord.gg/mGQWBQHASt](https://github.com/abenz1267/walker/issues)

## License

By contributing to this documentation, you agree that your contributions will be licensed under the same license as Walker (GNU General Public License v3.0).
