---
description: Guidelines for structuring FAQ pages in Secured Finance documentation
---

# 📋 FAQ Page Structure Guidelines

## Overview

This document establishes consistent guidelines for creating and maintaining FAQ pages across Secured Finance documentation. These guidelines ensure optimal user experience across desktop and mobile devices while maintaining content quality and accessibility.

## Template Structure

### Required Frontmatter
```yaml
---
description: Brief description of the FAQ scope and purpose
---
```

### Page Structure Template
```markdown
# ❓ [Product Name] FAQs

## Overview
Brief introduction to the FAQ scope (2-3 sentences)

## What You'll Learn
- Key concept 1
- Key concept 2  
- Key concept 3

## Quick Navigation
- [Section 1](#section-1)
- [Section 2](#section-2)
- [Section 3](#section-3)

## Section 1
<details>
<summary>Question goes here?</summary>
Answer content with proper formatting and links.
</details>

## Related Resources
- [Link to related documentation 1](../path/to/doc1.md)
- [Link to related documentation 2](../path/to/doc2.md)
```

## Navigation Principles

### Mobile-First Design
- **Use collapsible sections** (`<details>` tags) instead of tabs for better mobile UX
- **Include Quick Navigation** with anchor links for easy jumping between sections
- **Keep section titles concise** for mobile screen constraints

### Content Organization
1. **Getting Started** - Basic concepts and introductory questions
2. **Core Operations** - Main functionality and common use cases  
3. **Risk Management** - Safety, liquidation, and risk-related topics
4. **Advanced Topics** - Complex features and edge cases
5. **Troubleshooting** - Common issues and solutions

### Question Formatting
- Use `####` headers for questions when not using collapsible sections
- Use `<summary>` tags for questions within collapsible sections
- Keep questions concise and user-focused
- Use natural language that users would actually search for

## Content Guidelines

### Answer Quality
- **Self-contained answers** - Each answer should be complete without requiring other FAQ entries
- **Include concrete examples** where applicable
- **Cross-reference related documentation** using proper relative links
- **Use consistent terminology** aligned with the main documentation

### Avoiding Duplication
- **Single source of truth** - Avoid repeating the same information across multiple FAQ pages
- **Cross-reference instead of duplicate** - Link to detailed explanations in main documentation
- **Unified answers** - Create shared answers for questions that apply to multiple products

### Link Management
- Use **relative paths** for internal documentation links
- **Test all links** before publishing
- **Avoid self-referencing links** within the same FAQ page
- **Update links** when documentation structure changes

## Mathematical Formulas

Use block-style formatting for mathematical expressions:

```markdown
$$
\text{Collateral Ratio} = \frac{\text{Collateral Value}}{\text{Debt Amount}} \times 100\%
$$
```

## Examples Section

Each FAQ answer should include practical examples when applicable:

```markdown
<details>
<summary>How do I calculate my collateral ratio?</summary>

Your collateral ratio determines your liquidation risk. Here's how to calculate it:

$$
\text{Collateral Ratio} = \frac{\text{FIL Value}}{\text{USDFC Debt}} \times 100\%
$$

**Example:**
- You deposit 100 FIL worth $500
- You mint 400 USDFC
- Your collateral ratio = ($500 ÷ $400) × 100% = 125%

Since this is above the 110% minimum, your position is safe from liquidation.

**Related:** [Managing Collateral Effectively](../getting-started/managing-collateral-effectively.md)
</details>
```

## Maintenance Guidelines

### Regular Updates
- **Review quarterly** for accuracy and relevance
- **Update links** when documentation structure changes
- **Add new questions** based on community feedback and support tickets
- **Archive outdated questions** that no longer apply

### Version Control
- **Document changes** in commit messages
- **Test GitBook preview** before merging
- **Coordinate with related documentation** updates

## Implementation Checklist

When creating or updating FAQ pages:

- [ ] Frontmatter includes proper description
- [ ] Overview section introduces the scope
- [ ] "What You'll Learn" section lists key concepts
- [ ] Quick Navigation provides section links
- [ ] Questions organized by user journey complexity
- [ ] All answers include examples where applicable
- [ ] Related Resources section includes relevant links
- [ ] All internal links use relative paths and work correctly
- [ ] Mathematical formulas use proper block formatting
- [ ] Content tested on both desktop and mobile GitBook preview

## Related Resources

- [Documentation Structure Guidelines](../introduction/documentation-structure-guidelines.md)
- [GitBook Style Guide](../introduction/gitbook-style-guide.md)
- [Content Writing Guidelines](../introduction/content-writing-guidelines.md)
