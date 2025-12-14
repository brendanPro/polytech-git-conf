# AGENTS.md

Instructions pour les agents de codage travaillant sur ce projet Slidev.

## Setup commands

- Install dependencies: `bun install`
- Start dev server: `bun run dev` (ouvre automatiquement dans le navigateur)
- Build for production: `bun run build`
- Export slides: `bun run export` (génère PDF, PNG, ou PPTX)

## Project structure

```
.
├── slides.md              # Fichier principal de présentation
├── pages/                 # Slides importées depuis d'autres fichiers
│   └── imported-slides.md
├── components/            # Composants Vue réutilisables
│   └── Counter.vue
├── snippets/              # Extraits de code pour inclusion dans les slides
│   └── external.ts
├── netlify.toml          # Configuration Netlify pour le déploiement
├── vercel.json           # Configuration Vercel pour le déploiement
└── package.json          # Dépendances et scripts
```

## Code style

- **Markdown**: Utilisez le format Markdown étendu de Slidev
- **Frontmatter YAML**: Chaque slide commence par `---` avec des métadonnées optionnelles
- **Séparateurs**: Utilisez `---` pour séparer chaque slide
- **Composants Vue**: Les composants dans `components/` sont automatiquement importés
- **UnoCSS**: Utilisez les classes UnoCSS pour le styling (syntaxe Tailwind-like)

## Slidev best practices

### Frontmatter

Chaque fichier de slides doit commencer par un frontmatter YAML:

```yaml
---
theme: seriph
background: https://cover.sli.dev
title: Titre de la présentation
info: |
  Description de la présentation
class: text-center
transition: slide-left
mdc: true
duration: 20min
---
```

### Slide structure

- Utilisez `---` pour séparer chaque slide
- Les métadonnées de slide peuvent être définies entre les séparateurs
- Les commentaires HTML `<!-- -->` sont utilisés pour les notes du présentateur

### Importing slides

Pour organiser de grandes présentations, importez des slides externes:

```markdown
---
src: ./pages/imported-slides.md
hide: false
---
```

### Code blocks

- Utilisez Shiki pour le syntax highlighting: ` ```ts `
- Line highlighting: ` ```ts {1|2-3|all} `
- TwoSlash pour TypeScript: ` ```ts twoslash `
- Monaco Editor: ` ```ts {monaco} `
- External snippets: `<<< @/snippets/external.ts#snippet`

### Components

- Les composants Vue dans `components/` sont auto-importés
- Utilisez les composants intégrés: `<Toc />`, `<Tweet />`, `<Youtube />`
- Les props peuvent être passées directement: `<Counter :count="10" />`

### Animations

- `v-click` pour révéler progressivement: `<div v-click>`
- `v-motion` pour les animations: `<div v-motion :initial="{ x: -80 }" :enter="{ x: 0 }">`
- `v-mark` pour marquer du texte: `<span v-mark.red>`

### Layouts

Layouts disponibles: `default`, `center`, `two-cols`, `image-right`, `image-left`, `quote`, `section`

```markdown
---
layout: two-cols
---

# Colonne gauche

::right::

# Colonne droite
```

## Testing instructions

- Vérifiez que les slides s'affichent correctement: `bun run dev`
- Testez l'export: `bun run export`
- Vérifiez que les composants Vue fonctionnent
- Assurez-vous que les imports de slides externes fonctionnent
- Testez les animations et interactions

## Common tasks

### Adding a new slide

1. Ajoutez le contenu Markdown dans `slides.md` ou un fichier dans `pages/`
2. Séparez avec `---`
3. Ajoutez des métadonnées optionnelles (layout, transition, etc.)

### Creating a component

1. Créez un fichier `.vue` dans `components/`
2. Le composant sera automatiquement disponible dans toutes les slides
3. Utilisez la syntaxe Vue 3 Composition API

### Adding code snippets

1. Créez un fichier dans `snippets/`
2. Utilisez `#region snippet` et `#endregion snippet` pour délimiter
3. Référencez avec `<<< @/snippets/filename.ts#snippet`

### Exporting slides

- PDF: `bun run export --format pdf`
- PNG: `bun run export --format png`
- PPTX: `bun run export --format pptx`
- SPA: `bun run build` (génère une application web statique)

## Deployment

- **Netlify**: Configuration dans `netlify.toml`, déploiement automatique depuis `dist/`
- **Vercel**: Configuration dans `vercel.json`, déploiement automatique depuis `dist/`
- **GitHub Pages**: Utilisez `bun run build` et déployez le dossier `dist/`

## Documentation references

- [Slidev Documentation](https://sli.dev/guide)
- [Slidev Syntax Guide](https://sli.dev/guide/syntax)
- [Slidev Components](https://sli.dev/builtin/components)
- [Slidev Themes](https://sli.dev/resources/theme-gallery)

## Important notes

- Ce projet utilise **Bun** au lieu de npm/pnpm pour les commandes
- Le thème par défaut est `seriph` (défini dans `slides.md`)
- Les composants Vue utilisent la Composition API
- UnoCSS est utilisé pour le styling (pas de CSS traditionnel)
- Les slides sont basées sur Markdown avec des extensions Slidev

