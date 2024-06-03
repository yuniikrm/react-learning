# useQuery

Hooks useQuery digunakan dalam pemanggilan API untuk metode GET.

Pemanggilan useQuery akan terlihat seperti ini:

```typescript
const queryKey = 'get-posts'
const queryGetPosts = useQuery(queryKey, fetchFunction, options)
const { data, isLoading, isError, refetch } = queryGetPosts
```

#### Return useQuery

Hasil return dari useQuery yang biasa digunakan antara lain:

* `data`: Data yang didapat dari pemanggilan API
* `isLoading`: State isLoading dari pemanggilan API
* `isError`: State yang menunjukkan bahwa pemanggilan API mengembalikan error
* `refetch`: Function yang dapat digunakan untuk melakukan pemanggilan API kembali

#### Query Key

Query Key digunakan sebagai identifier dari API yang akan dipanggil oleh useQuery. Identifier ini dimanfaatkan di dalam sistem caching yang digunakan oleh useQuery. Untuk menghilangkan cache yang ada, bisa digunakan metode Query Invalidation yang memanfaat Query Key.

Query Key akan masuk menjadi paramter ke-1 di dalaam hooks useQuery.

#### Fetch Function

Di dalam pemanggilan API menggunakan useQuery, fungsi API yang biasa digunakan (dalam hal ini axios) akan menjadi parameter ke-2 yang masuk ke dalam hooks useQuery.

#### useQuery Options

Hooks useQuery memiliki parameter ke-3 yaitu options. Parameter ini berisikan object / method yang akan dilakukan sebelum/sesudah pemanggilan API berakhir.

Beberapa method yang ada di dalamnya yaitu:

* `enabled`: Digunakan untuk mengaktifkan / menonaktifkan pemanggilan API. Jika false, maka API tidak akan dipanggil.
* `onSuccess`: Di dalam onSuccess kita bisa memasukkan statement yang ingin dijalankan setelah pemanggilan API dan fetchFunction melakukan return hasil / resolve Promise.
* `onError`: Di dalam onError kita bisa memasukkan statement yang ingin dijalankan setelah pemanggilan API dan fetchFunction melakukan return error / reject Promise.

## Usage API Call

```typescript
// example.tsx
/* eslint-disable @typescript-eslint/no-explicit-any */
import axios from 'axios';
import { useQuery } from 'react-query';

const baseURL = "https://jsonplaceholder.typicode.com/posts";

function ExamplePage() {
  const fetchFunction = () => {
    return axios.get(baseURL).then((response) => {
      return response?.data
    }).catch(error => {
      console.error(error)
    });
  }

  const queryKey = 'get-posts'
  const { data: resultData } = useQuery(queryKey, fetchFunction)

  return (
    <div>
      {resultData?.map((el) => (
        <div style={{ border: '1px solid black', margin: '16px', padding: '16px' }}>
          <b>{el.title}</b>
          <p>{el.body}</p>
          <p>Created By: User Id {el.userId}</p>
          <p>Id: {el.id}</p>
        </div>
      ))}
    </div>
  )
}

export default ExamplePage
```

Di dalam contoh code di atas, fetchFunction akan dipanggil ketika component `ExamplePage` dirender. Hal ini dilakukan karena useQuery masuk ke dalam life cycle dari component `ExamplePage`.

## Lazy Fetching

Secara default, pemanggilan API akan dilakukan ketika component dirender (useQuery mengikuti life cycle component). Tetapi dalam penggunaannya, terkadang pemanggilan API ingin dilakukan pada waktu-waktu tertentu. Pemanggilan API yang ditrigger oleh event tertentu disebut `Lazy Fetching / Lazy Loading`.

Dengan menggunakan useQuery, lazy loading dapat diterapkan dengan beberapa metode antara lain:

* refetch()
* Query Invalidation

### Lazy Fetching with refetch()

Dalam contoh di bawah ini, kita akan mengimplementasikan fungsi search kepada list `Users`. API Get Users akan dipanggil kembali berdasarkan input yang dimasukkan.

```typescript
// example.tsx
/* eslint-disable @typescript-eslint/no-explicit-any */
import { useDebounce } from '@navi-app/utils';
import axios from 'axios';
import { Input } from 'baseui/input';
import { useEffect, useState } from 'react';
import { useQuery } from 'react-query';

const baseURL = "https://jsonplaceholder.typicode.com/users";

function ExamplePage() {
  const [name, setName] = useState<string>('')
  const debounceName = useDebounce(name, 300)

  const fetchFunction = () => {
    const params = {
      name: name || null
    }
    return axios.get(baseURL, { params }).then((response) => {
      return response?.data
    }).catch(error => {
      console.error(error)
    });
  }

  const queryKey = 'get-users'
  const { data: resultData, refetch } = useQuery(queryKey, fetchFunction, { enabled: false })

  useEffect(() => { refetch() }, [debounceName])

  return (
    <div style={{ padding: '64px' }}>
      <div style={{ marginBottom: '24px' }}>
        <Input
          value={name}
          onChange={(e) => setName(e.target.value)}
          placeholder="Search by name (exact)"
        />
      </div>
      {resultData?.map((el) => (
        <div style={{ padding: '16px', margin: '16px 0 16px', border: '1px solid black', borderRadius: '8px' }}>
          <b>Name: {el.name}</b>
          <p>Username: {el.username}</p>
          <p>E-mail: {el.email}</p>
        </div>
      ))}
    </div>
  )
}

export default ExamplePage
```

Dalam penggunaan fungsi `refetch()`, pastikan options `enabled` di-set menjadi `false` agar API tidak dipanggil sebelum kondisi tertentu ditrigger (dalam hal ini, sebelum search dilakukan)

```typescript
  const queryKey = 'get-users'
  const { data: resultData, refetch } = useQuery(queryKey, fetchFunction, { enabled: false })

  useEffect(() => { refetch() }, [debounceName])
```

### Lazy Fetching with Query Invalidation

Query Invalidation adalah menghapus cache yang disimpan di dalam useQuery. Cache ini disimpan sebagai key-value pair dengan Query Key sebagai key dan data return sebagai valuenya.

Untuk menghapus cache dari suatu Query Key, dapat menggunakan hooks useQueryClient yang menyediakan fungsi `removeQueries`.

Perbandingan penggunaan `refetch` dengan `removeQueries`:

```typescript
  // refetch
  import { useQuery } from 'react-query';

  const queryKey = 'get-users'
  const { data: resultData, refetch } = useQuery(queryKey, fetchFunction, { enabled: false })

  useEffect(() => { refetch() }, [debounceName])
```

```typescript
  // removeQueries
  import { useQuery, useQueryClient } from 'react-query';

  const queryKey = 'get-users'
  const { data: resultData, refetch } = useQuery(queryKey, fetchFunction, { enabled: false })
  const queryClient = useQueryClient()

  useEffect(() => {
    queryClient.removeQueries(queryKey, { exact: true })
    }, [debounceName])
```
