# Setting Up Pinia and Configuring `@` Alias in a Vue 3 Project

This guide will walk you through setting up Pinia for state management and configuring the `@` alias in a Vue 3 project.

## Prerequisites

- Node.js and Yarn installed
- Vue 3 project set up with Vite

## Steps

### 1. Install Pinia

First, install Pinia using Yarn:

```sh
yarn add pinia
```

### 2. Create a Pinia Store

Create a new file `store.ts` in your store directory:

```typescript
import { defineStore } from 'pinia'

export interface State {
	count: number
	message: string
	isLoggedIn: boolean
}

export const useStore = defineStore('store', {
	state: (): State => ({
		count: 0,
		message: 'Hello, Pinia!',
		isLoggedIn: false,
	}),
	actions: {
		increment() {
			this.count++
		},
		login() {
			this.isLoggedIn = true
		},
		logout() {
			this.isLoggedIn = false
		},
		updateMessage(newMessage: string) {
			this.message = newMessage
		},
	},
})
```

### 3. Set Up Pinia in Your Main Application File

Update your `main.ts` file to include Pinia:

```typescript
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'
import './assets/scss/app.scss'
import router from './router'

const app = createApp(App)
const pinia = createPinia()

app.use(router)
app.use(pinia)
app.mount('#app')
```

### 4. Configure the `@` Alias

Update your Vite configuration file (`vite.config.ts`) to include the alias configuration:

```typescript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { resolve } from 'path'

// https://vite.dev/config/
export default defineConfig({
	plugins: [vue()],
	base: '/codestream/',
	resolve: {
		alias: {
			'@': resolve(__dirname, 'src'),
		},
	},
})
```

### 5. Update tsconfig.json

Ensure your tsconfig.json includes the correct paths:

```json
{
	"compilerOptions": {
		"baseUrl": ".",
		"paths": {
			"@/*": ["src/*"]
		}
		// other compilerOptions...
	},
	"include": ["src/**/*.ts", "src/**/*.tsx", "src/**/*.vue"]
}
```

### 6. Use the Store in Your Components

You can now use the Pinia store in your Vue components. Here is an example:

```vue
<!-- filepath: d:\AwesomeWebProjects\codestream\src\views\about\AboutIndex.vue -->
<script setup lang="ts">
import { useStore } from '@/store'
import { storeToRefs } from 'pinia'

const store = useStore()
const { count } = storeToRefs(store)

const increment = store.increment
</script>

<template>
	<div class="container mt-3">
		<h5 class="text-primary">About</h5>

		<div class="mt-3">
			<p>Count: {{ count }}</p>
			<button @click="increment" type="button" class="btn btn-primary">
				Increment
			</button>
		</div>
	</div>
</template>
```

### 7. Restart Your TypeScript Server

After making these changes, restart your TypeScript server in VS Code:

1. Open the command palette (`Ctrl+Shift+P`).
2. Type "TypeScript: Restart TS Server" and select it.

## Conclusion

You have successfully set up Pinia for state management and configured the `@` alias in your Vue 3 project. You can now use Pinia to manage your application's state and use the `@` alias for cleaner imports.
