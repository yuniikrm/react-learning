# Responsive Design

Untuk membuat desain responsif  dengan Tailwind CSS dapat dilakukan dengan beberapa langkah dasar berikut:

## Penggunaan Utility Classes Tailwind CSS

Tailwind CSS menggunakan utility classes untuk styling, yang memudahkan dalam membuat desain responsif. Pendekatan mobile-first dalam Tailwind CSS berarti Anda mulai dengan desain untuk perangkat seluler (mobile) dan kemudian menambahkan perubahan untuk layar yang lebih besar.

## Menentukan Breakpoints

Tailwind CSS memiliki breakpoint bawaan yang bisa Anda gunakan, seperti `sm` (640px), `md` (768px), `lg` (1024px), `xl` (1280px), dan `2xl` (1536px). Anda dapat menggunakan breakpoint ini untuk mengatur perubahan gaya pada layar yang lebih besar.

## Implementasi

```html
<div class="bg-gray-200 p-4 sm:w-full md:w-1/2 lg:w-1/3 xl:w-1/4">
    <p class="text-center text-lg">Ini adalah teks responsif dengan Tailwind CSS</p>
</div>
```

## Menggunakan `@screen` directive (opsional)

Jika Anda perlu menyesuaikan lebih lanjut atau menambahkan breakpoint kustom, Anda dapat menggunakan `@screen` directive dalam konfigurasi Tailwind CSS:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@screen sm {
  /* Styles for small screens */
}

@screen md {
  /* Styles for medium screens */
}
```
