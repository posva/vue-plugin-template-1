# Vue Plugin Template

A comprehensive template for creating Vue 3 plugins with TypeScript, testing, and development tools pre-configured.

## 🚀 Features

- ✅ **Vue 3** support with TypeScript
- ✅ **Local playground** for testing your plugin during development
- ✅ **Unit testing** with Vitest and Vue Test Utils
- ✅ **Linting** with ESLint and Prettier
- ✅ **GitHub Actions** CI/CD pipeline
- ✅ **Build configuration** for npm package publishing
- ✅ **Example components** and composables

## 🏁 Getting Started

### 1. Clone this template

```bash
git clone https://github.com/monterail/vue-plugin-template.git
cd vue-plugin-template
```

### 2. Install dependencies

```bash
npm install
```

### 3. Customize your plugin

Update the following files:

- `package.json` - Change name, description, author, etc.
- `src/index.ts` - Rename your plugin and customize functionality
- `src/components/` - Add or modify components
- `src/composables/` - Add or modify composables
- `README.md` - Update documentation for your plugin

### 4. Start development

```bash
# Run the playground for local development
npm run dev

# Or run tests in watch mode
npm run test:watch
```

## 🛠️ Development

### Basic Plugin Structure

```typescript
// src/index.ts
import type { App, Plugin } from 'vue'

export interface MyPluginOptions {
  // Your options here
}

const MyPlugin: Plugin = {
  install(app: App, options: MyPluginOptions = {}) {
    // Register components
    app.component('MyComponent', MyComponent)
    
    // Add global properties
    app.config.globalProperties.$myPlugin = {
      // Your global methods
    }
    
    // Provide data
    app.provide('myData', someData)
  }
}

export default MyPlugin
```

### Registering Components

```typescript
// Register globally
app.component('MyComponent', MyComponent)

// Register with prefix
const prefix = options.prefix || 'My'
app.component(`${prefix}Component`, MyComponent)
```

### Adding Global Properties

```typescript
app.config.globalProperties.$myPlugin = {
  greet: (name: string) => `Hello, ${name}!`
}

// TypeScript types
declare module 'vue' {
  export interface ComponentCustomProperties {
    $myPlugin: {
      greet: (name: string) => string
    }
  }
}
```

### Creating Composables

```typescript
// src/composables/useMyPlugin.ts
import { ref, computed } from 'vue'

export function useMyPlugin() {
  const count = ref(0)
  const double = computed(() => count.value * 2)
  
  const increment = () => count.value++
  
  return { count, double, increment }
}
```

## 🔧 Using Your Published Plugin

Once published, users can install and use your plugin:

```bash
npm install your-plugin-name
```

```typescript
// main.ts
import { createApp } from 'vue'
import App from './App.vue'
import MyPlugin from 'your-plugin-name'

const app = createApp(App)

app.use(MyPlugin, {
  // Plugin options
})

app.mount('#app')
```

```vue
<!-- Using in components -->
<template>
  <MyComponent />
</template>

<script setup>
import { useMyPlugin } from 'your-plugin-name'

const { count, increment } = useMyPlugin()
</script>
```

## 📦 Publishing to npm

Before publishing your plugin to npm, make sure you've:

1. **Updated `package.json`** with your plugin details:
   - Change `name` to your package name
   - Update `version`, `description`, `author`, and `keywords`
   - Set `repository` URL if applicable

2. **Built your plugin**:
   ```bash
   npm run build
   ```

3. **Tested thoroughly**:
   ```bash
   npm test
   ```

4. **Log in to npm** (if not already logged in):
   ```bash
   npm login
   ```

5. **Publish to npm**:
   ```bash
   npm publish
   ```

> **Note:** The `prepublishOnly` script will automatically run the build before publishing.

## 🌟 Showcase Your Plugin

After publishing your plugin, consider adding it to [vue-plugins.org](https://www.vue-plugins.org/) - a curated directory of Vue.js plugins and libraries. It's a great way to:

- 📣 **Increase visibility** - Get your plugin discovered by the Vue community
- 🎯 **Reach your audience** - Connect with developers looking for Vue plugins
- 🏆 **Build credibility** - Be part of a trusted resource for Vue developers
- 📊 **Track adoption** - See how your plugin is being used

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

MIT

## 🙏 Acknowledgments

Built with:
- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- [Vitest](https://vitest.dev/)
- [TypeScript](https://www.typescriptlang.org/)
- [Vue Test Utils](https://test-utils.vuejs.org/)

---

**Happy plugin building! 🎉**

If you find this template helpful, please give it a ⭐️ on GitHub!
