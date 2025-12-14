# Polytech Git Configuration - Slidev Presentation

Slidev presentation about Git configuration for Polytech.

## 🚀 Quick Start

### Prerequisites

- [Bun](https://bun.sh/) installed on your machine

### Installation

```bash
# Install dependencies
bun install
```

### Development

```bash
# Start the development server (automatically opens in browser)
bun run dev
```

### Build and Export

```bash
# Build for production (generates a static SPA)
bun run build

# Export slides
bun run export              # Default export (PDF)
bun run export --format pdf  # Export PDF
bun run export --format png  # Export PNG
bun run export --format pptx # Export PowerPoint
```

## 📁 Project Structure

```
.
├── slides.md              # Main presentation file
├── pages/                 # Slides imported from other files
│   └── imported-slides.md
├── components/            # Reusable Vue components
│   └── Counter.vue
├── snippets/              # Code snippets for inclusion in slides
│   └── external.ts
├── AGENTS.md              # Instructions for coding agents
├── netlify.toml          # Netlify deployment configuration
├── vercel.json           # Vercel deployment configuration
└── package.json          # Dependencies and scripts
```

## 🎨 Themes

This project uses the **seriph** theme by default. The following themes are available:

- `@slidev/theme-default`
- `@slidev/theme-seriph` (current)

To change the theme, modify the `theme` property in the frontmatter of `slides.md`.

## 📝 Documentation

- [Slidev Documentation](https://sli.dev/guide)
- [Slidev Syntax Guide](https://sli.dev/guide/syntax)
- [Built-in Components](https://sli.dev/builtin/components)
- [Theme Gallery](https://sli.dev/resources/theme-gallery)

## 🤖 For Coding Agents

This project includes an `AGENTS.md` file that contains detailed instructions for coding agents working on this project. Check it out for:

- Setup commands
- Code conventions
- Slidev best practices
- Deployment instructions

## 🚢 Deployment

This project is configured to be deployed on:

- **Netlify**: Configuration in `netlify.toml`
- **Vercel**: Configuration in `vercel.json`
- **GitHub Pages**: Use `bun run build` and deploy the `dist/` folder

## 📄 License

This project is private.

## 🔗 Useful Links

- [Slidev GitHub](https://github.com/slidevjs/slidev)
- [Slidev Documentation](https://sli.dev)
- [AGENTS.md Standard](https://agents.md/)
