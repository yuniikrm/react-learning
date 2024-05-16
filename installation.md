# Installation

1. Install [nodeJs](https://nodejs.org/en/download), jika sudah terinstall jalankan `node --version` pada terminal untuk memastikan node sudah terinstall
2.  Install pnpm&#x20;

    ```bash
    npm install -g pnpm
    ```


3.  Perintah ini akan menginstal `pnpm` secara global pada sistem, sehingga dapat digunakan dari teriminal mana saja. Setelah instalasi selesai, jalankan perintah berikut untuk memastikan sudah terinstall dengan benar

    ```bash
    pnpm --version
    ```



## Generate React App dengan Vite

Jalankan perintah berikut pada terminal untuk membuat app baru

```
pnpm create vite my-react-app --template react-ts
```

Jika aplikasi selesai di-generate, install library dependencies dengan membuka terminal pada root folder app, lalu jalankan perintah `pnpm install`\


Setelah instalasi dependencies selesai, run aplikasi dengan command `pnpm dev` untuk running mode development, dan `pnpm build` untuk running mode build.
