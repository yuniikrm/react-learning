# useState

## Definition

Hooks useState digunakan untuk mendefine sebuah state di dalam sebuah component. State Management paling sederhana yang bisa digunakan di dalam sebuah aplikasi react adalah menggunakan useState ini.

Pemanggilan useState akan terlihat seperti ini:

```typescript
const [ name, setName ] = useState<string>('')
```

Atau secara semantic akan terlihat seperti ini:

```typescript
const [ state, setState ] = useState<type>(defaultValue)
```

Jabaran dari kode di atas antara lain:

* `state`: Variabel yang digunakan untuk menyimpan data.
* `setState`: Fungsi setter yang digunakan untuk mengubah state.
* `type`: Karena kita menggunakan typescript, maka kita perlu mendefine tipe dari tiap state.
* `defaultValue`: Value awal dari state tersebut sebelum diassign.

## Penggunaan useState

```typescript
// example.tsx
/* eslint-disable @typescript-eslint/no-explicit-any */
import { Button } from 'baseui/button';
import { useState } from 'react';

function ExamplePage() {
  const [count, setCount] = useState<number>(0)

  const incrementCount = () => {
    setCount(count + 1)
  }

  return (
    <div>
      <p>Count: {count}</p>
      <Button onClick={incrementCount}>
        Increment
      </Button>
    </div>
  )
}

export default ExamplePage
```

## Passing Melalui Props

State bisa diperlakukan seperti variabel/value biasa yang dapat dipassing melalui props. Di dalam penggunaan component yang memiliki nesting yang lumayan dalam, passing props ke dalam component di nest terdalam menjadi tidak efektif. Hal ini dapat diatasi dengan menggunakan global state management seperti **Context**, **Redux**, ataupun **Zustand**
