# vite-aloha

A Vite template for developing Aloha plugins with TypeScript support, optimized build configuration, and testing setup.

## Overview

The `vite-aloha` template provides a streamlined development environment for creating plugins for the Aloha desktop agent. It includes:

- **TypeScript support** with strict type checking
- **Vite build system** optimized for Node.js libraries
- **Aloha SDK integration** with proper plugin structure
- **Testing setup** with Node.js test runner - feel free to replace with your favourite test runner
- **ESM module format** for modern JavaScript compatibility

## Quick Start

### Requirements

- Node.js 20+ 
- npm or yarn
- prefix the plugin name with `aloha-`
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
│   └── index.esm.ts          # Main plugin entry point
├── public/
│   └── manifest.json         # Plugin manifest file
│   └── icon.svg              # Plugin icon
├── tests/
│   └── validate-export.test.mts  # Example tests
├── package.json              # Project configuration
├── vite.config.ts           # Vite build configuration
├── tsconfig.json            # TypeScript configuration
└── README.md               # This file
```

## Plugin Development

### Basic Plugin Structure

The template provides a basic plugin structure that extends the Aloha SDK's `Plugin` class:

```typescript
import { Plugin, PluginContext } from 'aloha-sdk'

export default class AlohaSamplePlugin extends Plugin {
  constructor(context: PluginContext) {
    super(context)
  }

  async toolCall(toolName: string, args: any): Promise<string> {
    return "Your `Markdown` response"
  }
}
```

## Building and Testing

### Build Command

```bash
npm run build
```

The built files will be in `dist/`:
  - `icon.svg` - Static Asset from public folder
  - `manifest.json` - Your plugin manifest file from public folder
  - `index.esm.js` - Main plugin file
  - `index.esm.js.map` - Source map for debugging

### Testing

```bash
# Run tests
npm test

# Run tests in watch mode
npm run test:watch
```

## Plugin Manifest

The `public/manifest.json` file describe the plugin capabilities to Aloha Desktop agent:

```json
{
  "manifestVersion": 1,
  "name": "Your Plugin Name",
  "version": "1.0.0",
  "description": "Description of what your plugin does",
  "author": "Your Name",
  "icon": "dist/icon.svg",
  "main": "dist/index.esm.js",
  "tools": [
    {
      "name": "toolName",
      "displayName": "Tool Display Name",
      "description": "Description of the tool",
      "parameters": {
        "type": "object",
        "required": ["paramName"],
        "properties": {
          "paramName": {
            "type": "string",
            "description": "Parameter description"
          }
        }
      }
    }
  ]
}
```

## Publishing

### Automatic

The template includes a GitHub release workflow that is triggered on new `v#.#.#` tags.

The workflow is creating a `plugin.tgz` artifact with `dist` folder and adding it to a new release.

### Manual

```bash
# Test your code
npm run test 

# build code bundle
npm run build

# pack dist folder and manifest.json into tarball
tar czf plugin.tgz dist manifest.json
```

Finally publish the `plugin.tgz` on a new GitHub release.

## License

MIT
