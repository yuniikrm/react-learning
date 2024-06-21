# Styling with Tailwind

Tailwind adalah library utility classes untuk styling, yang memungkinkan untuk menuliskan style langsung di dalam elemen HTML . Langkah-langkah untuk menggunakan Tailwind CSS

## Installation

```
pnpm add tailwindcss
```

## Configuration

Setelah menginstal, Anda perlu mengonfigurasi Tailwind. Jika Anda belum memiliki file konfigurasi, Anda bisa menghasilkannya dengan menjalankan:

```
npx tailwindcss init
```

Ini akan membuat file `tailwind.config.js` di direktori proyek Anda.

## Import

Buka file CSS utama proyek Anda (biasanya `src/index.css` atau `src/App.css`) dan impor Tailwind CSS:

```css
/* src/index.css atau src/App.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
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
