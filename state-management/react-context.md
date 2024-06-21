# React Context

React Context dalah salah satu cara untuk melakukan State Management secara global di dalam sebuah aplikasi.

React Context terdiri dari 3 langkah utama:

* Membuat Context (createContext)
* Menyediakan Context (Context Provider)
* Menggunakan Context (Context Consumer)

Dengan menggunakan React Context, kita tidak perlu passing state dari

## Membuat Context

Pertama-tama, context perlu dibuat. Di dalam contoh kali ini, akan dibuat context yang akan menyimpan state untuk theme dari aplikasi kita (mode terang & gelap).

```typescript
import React, { createContext, useState, useContext } from 'react';

const ThemeContext = createContext();
```

## Menyediakan Context

Context yang sudah dibuat, perlu diisi dan didefinisikan seperti layaknya hooks dan state di dalam react.

```typescript
const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

`ThemeProvider` ini nantinya akan membungkus setiap component di dalam aplikasi kita yang ingin dipengaruhi oleh context ini.

```typescript
const App = () => (
  <ThemeProvider>
    <ThemeToggle />
  </ThemeProvider>
);

export default App;
```

## Penggunaan Context

Context bisa langsung dipanggil di dalam component yang sudah dibungkus oleh `ThemeProvider`.

```typescript
const ThemeToggle = () => {
  const { theme, setTheme } = useContext(ThemeContext);

  const toggleTheme = () => {
    setTheme((prevTheme) => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <div>
      <p>Tema Saat Ini: {theme}</p>
      <button onClick={toggleTheme}>Ubah Tema</button>
    </div>
  );
};
```

Ketika value berubah dari `dark` menjadi `light` ataupun sebaliknya, semua component yang dibungkus di dalam `ThemeProvider` dan memakai value dari context tersebut akan terpengaruh.
