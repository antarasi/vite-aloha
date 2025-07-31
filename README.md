# vite-aloha

A Vite template for developing Aloha plugins with TypeScript support, optimized build configuration, and testing setup.

![Vite+Aloha](.github/assets/vite-aloha-64.png)

[![Open in StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/~/github.com/antarasi/vite-aloha?file=src/index.esm.ts&startScript=build)


## Overview

The `vite-aloha` template provides a streamlined development environment for creating plugins for the Aloha desktop agent. It includes:

- 🔷 **TypeScript support** with strict type checking
- ⚡ **Vite build system** optimized for Node.js libraries
- 🧩 **Aloha SDK integration** with proper plugin structure
- 🧪 **Testing setup** with Node.js test runner - feel free to replace with your favourite test runner
- 📦 **ESM module format** for modern JavaScript compatibility

## Quick Start

### Requirements

- Node.js 20+ 
- npm or yarn
- prefix the plugin repository name with `aloha-`
- include plugin `manifest.json`

### Installation

1. **Apply the template:**
   ```bash
   npx degit antarasi/vite-aloha#main aloha-awesome-plugin
   cd aloha-awesome-plugin
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start development:**
   ```bash
   npm run build
   npm test
   ```

**Note:** You can also apply the template to your existing npm project:
```bash
cd aloha-awesome-plugin

# notice the dot below indicating current directory
npx degit antarasi/vite-aloha#main . 
```

## Project Structure

```
vite-aloha/
├── src/
│   └── index.esm.ts              # Main plugin entry point
├── public/
│   └── icon.svg                  # Plugin icon
├── tests/
│   └── validate-export.test.mts  # Example tests
└── manifest.json                 # Plugin manifest file
```

## Building and Testing

### Build Command

```bash
npm run build
```

The built files will be in `dist/`:
  - `icon.svg` - Static Asset from public folder
  - `index.esm.js` - Main plugin file
  - `index.esm.js.map` - Source map for debugging

### Testing

```bash
# Run tests
npm test

# Run tests in watch mode
npm run test:watch
```

## Publishing

### Automatic

The template includes a GitHub release workflow that is triggered on new `v#.#.#` tags.

The workflow is creating a new release with `manifest.json` and `plugin.tgz` (containing the `dist` folder).

> **Note:** To make the workflow automatically publish releases of your plugin, go to your repository Settings > Actions > General > Workflow permissions > Select: Read and write permissions

### Manual

```bash
# Test your code
npm run test 

# build code bundle
npm run build

# pack dist folder into tarball
tar czf plugin.tgz dist
```

Finally publish the `manifest.json` and `plugin.tgz` on a new GitHub release.

## License

MIT
