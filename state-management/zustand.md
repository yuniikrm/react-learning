# Zustand

Zustand adalah sebuah library yang dapat digunakan untuk melakukan state management secara global. Jika data biasa disimpan di dalam sebuah `state` atau sebuah `context`, di dalam **Zustand** dikenal dengan istilah `store`.

Sama seperti **Context**, penggunaan **Zustand** dilakukan saat kita melakukan state management secara global, di mana kita ingin tetap memanage sebuah state tanpa perlu melakukan passing melalui props yang terlalu dalam. State dari parent component ter-atas bisa langsung diakses dengan memanggil hooks store dari **Zustand**.

Penggunaan **Zustand** lebih sederhana dibandingkan dengan penggunaan **Context** karena tidak memerlukan pembungkusan dengan `ContextProvider`.

## Store

Store di dalam **Zustand** digunakan untuk menyimpan state / function yang dapat digunakan untuk memodifikasi state yang ada.

### Pembuatan Store

Di dalam contoh kali ini, kita akan membuat sebuah store yang akan mengatur state dari `Tab` yang akan kita pilih.

```typescript
// tab.store.ts
import create from 'zustand';

type TTabStore = {
  tab: 'all' | 'waiting' | 'ongoing' | 'done';
  setTab: (tab: 'all' | 'waiting' | 'ongoing' | 'done') => void;
};

const useTabStore = create<TTabStore>()((set) => ({
  tab: 'all',
  setTab: (value) => set(() => ({ tab: value })),
}));

export default useTabStore;
```

Kode di atas jika ditulis menggunakan useState maka akan menjadi seperti ini.

```typescript
// index.tsx
import { useState } from 'react';

const [tab, setTab] = useState<'all' | 'waiting' | 'ongoing' | 'done'>('all');
```

### Penggunaan Store

Store yang telah dibuat dapat digunakan dengan melakukan pemanggilan seperti ini.

```typescript
// index.tsx
const { tab, setTab } = useTabStore()
```

## Shallow

Jika kita tidak ingin menggunakan semua state/function yang berada di dalam store, kita dapat melakukan pemanggilan dengan cara yang lebih efisien yaitu menggunakan `shallow`.

Contoh penggunaan store dengan shallow:

```typescript
// index.tsx
import { useShallow } from 'zustand/react/shallow';

// Hanya ingin memanggil setTab dari useTabStore
const { setTab } = useTabStore(
    useShallow((state) => ({
        setTab: state.setTab,
    }))
);
```

## Persist

State dari `store` ini akan menempel dengan lifecycle di mana hooks `store` ini dipanggil. Ketika lifecycle dari component tersebut sudah mengulang / terjadi re-render, maka value dari `store` ini akan kembali menjadi default value (sama seperti useState).

Untuk mempertahankan value dari state yang ada di dalam `store` ini, kita bisa menggunakan `persist` ketika melakukan pembuatan store.

```typescript
// tab.store.ts
import create from 'zustand';
import { persist } from 'zustand/middleware';

type TTabStore = {
  tab: 'all' | 'waiting' | 'ongoing' | 'done';
  setTab: (tab: 'all' | 'waiting' | 'ongoing' | 'done') => void;
};

const useTabStore = create<TTabStore>()(
  persist(
    (set) => ({
      tab: 'all',
      setTab: (value) => set(() => ({ tab: value })),
    }),
    {
      name: 'tabStore',
    }
  )
);

export default useTabStore;
```
