# useMutation

Hooks useMutation digunakan dalam pemanggilan API untuk metode POST, PUT, dan DELETE.

Pemanggilan useMutation akan terlihat seperti ini:

```typescript
const mutationCreatePosts = useMutation(fetchFunction)
const { data, mutate, isLoading, isError} = mutationCreatePosts
```

#### Return useQuery

Hasil return dari useQuery yang biasa digunakan antara lain:

* `data`: Data yang didapat dari pemanggilan API
* `mutate`: Function yang digunakan untuk melakukan pemanggilan API
* `isLoading`: State isLoading dari pemanggilan API
* `isError`: State yang menunjukkan bahwa pemanggilan API mengembalikan error

Function mutate

## Usage API Call

Di dalam contoh ini, kita akan membuat sebuah user baru dengan memasukkan `name` di dalam component `Input`, dan API Create User akan dipanggil ketika kita menekan tombol submit.

```typescript
// example.tsx
/* eslint-disable @typescript-eslint/no-explicit-any */
import axios from 'axios';
import { Button } from 'baseui/button';
import { Input } from 'baseui/input';
import { useState } from 'react';
import { useMutation } from 'react-query';

const baseURL = "https://jsonplaceholder.typicode.com/users";

function ExamplePage() {
  const [name, setName] = useState<string>('')

  const fetchFunction = (params: any) => {
    return axios.post(baseURL, { params }).then((response) => {
      return response?.data
    }).catch(error => {
      console.error(error)
    });
  }

  const { mutate } = useMutation(fetchFunction)

  const handleSubmit = async () => {
    try {
      const payload = { name }
      await mutate(payload, {
        onSuccess: (data) => {
          alert(`Success creating with id ${data?.id}`)
        },
        onError: (error) => {
          alert(`Error: ${error}`)
        }
      })
    } catch (error) {
      alert(`Error: ${error}`)
    }
  }

  return (
    <div style={{ padding: '64px' }}>
      <div style={{ marginBottom: '24px' }}>
        <Input
          value={name}
          onChange={(e) => setName(e.target.value)}
          placeholder="Name"
        />
      </div>
      <Button onClick={handleSubmit}>Submit</Button>
    </div>
  )
}

export default ExamplePage
```
