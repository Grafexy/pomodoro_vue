# 🍅 Pomodoro Vue

A modern Pomodoro Timer built with Vue 3, TypeScript, and Vite.

![Pomodoro Timer](https://github.com/user-attachments/assets/e468987e-1698-456a-befd-7b47e60ff0c0)

## Features

- ⏱️ 25-minute focus sessions with 5-minute breaks
- 🎯 Visual progress indicator with circular progress bar
- 🔊 Audio notification when sessions complete
- 📱 Responsive design for mobile and desktop
- 🎨 Clean, modern UI with Vue 3 composition API
- 🔄 Automatic session counting and break management

## Tech Stack

- **Vue 3** - Progressive JavaScript framework
- **TypeScript** - Type-safe JavaScript
- **Vite** - Fast build tool and dev server
- **Vue Router** - Client-side routing
- **ESLint** - Code linting
- **Prettier** - Code formatting

## Development

### Prerequisites

- Node.js 20.19.0 or higher
- npm

### Setup

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Type checking
npm run type-check

# Lint code
npm run lint

# Format code
npm run format
```

## CI/CD

This project includes GitHub Actions workflow for:

- ✅ Type checking with TypeScript
- ✅ Code linting with ESLint
- ✅ Automated building
- 🚀 Deployment to GitHub Pages

The app is automatically deployed to GitHub Pages when changes are pushed to the main branch.

## About the Pomodoro Technique

The Pomodoro Technique is a time management method developed by Francesco Cirillo in the late 1980s:

1. **Focus**: Work for 25 minutes with complete focus
2. **Break**: Take a 5-minute break
3. **Repeat**: Continue this cycle
4. **Long Break**: After 4 cycles, take a longer break (15-30 minutes)

### Benefits
- Improved focus and concentration
- Better time management
- Reduced mental fatigue
- Increased productivity

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.
