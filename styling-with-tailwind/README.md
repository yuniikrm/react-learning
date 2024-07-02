# Styling with Tailwind

Tailwind adalah library utility classes untuk styling, yang memungkinkan untuk menuliskan style langsung di dalam elemen HTML . Langkah-langkah untuk menggunakan Tailwind CSS

## Installation

```
pnpm install -D tailwindcss postcss autoprefixer
```

## Configuration

Setelah menginstal, Anda perlu mengonfigurasi Tailwind. Jika Anda belum memiliki file konfigurasi, Anda bisa menghasilkannya dengan menjalankan:

```
npx tailwindcss init -p
```

Ini akan membuat file `tailwind.config.js` di direktori proyek Anda.

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

## Import

Buka file CSS utama proyek Anda (biasanya `src/index.css` atau `src/App.css`) dan impor Tailwind CSS:

```css
/* src/index.css atau src/App.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Modify vite.config.js

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from "tailwindcss";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  css: {
    postcss: {
      plugins: [tailwindcss()],
    },
  },
})
```

## Usage

Anda sekarang dapat menggunakan Tailwind CSS langsung di komponen React Anda. Misalnya, jika Anda memiliki komponen `Button`:

```tsx
import React from 'react';

const Button = () => {
  return (
    <button className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Button
    </button>
  );
};

export default Button;
```
