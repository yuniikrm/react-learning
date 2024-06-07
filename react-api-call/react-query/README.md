# React Query

## Installation

```sh
pnpm add react-query
```

## Definition

React Query adalah sebuah library yang digunakan untuk memudahkan proses pemanggilan API dengan beberapa fitur utama yaitu:

* Data Fetching: Mempermudah pemanggilan API, menyediakan hooks & state yang mempermudah proses (refetch, isLoading).
* Caching: Melakukan cahe dengan otomatis, mengurangi pemanggilan API yang tidak perlu untuk meningkatkan performa.
* Pagination & Infinite Scroll: Menyediakan fungsi untuk pagination & infinite scroll yang bisa langsung digunakan.
* Mutation Management: Mempermudah proses Create, Update, Delete di dalam server (POST, PUT, DELETE).
* Query Invalidation: Pemanggilan API dapat di-invalidate / di-refetch ketika ada data yang berubah. Hal ini memastikan konsistensi dalam pemanggilan API tersebut

## Usage

Inisialisasi Query Client biasanya dilakukan di level tertinggi aplikasi Anda, seperti di file index atau app

<pre class="language-tsx"><code class="lang-tsx">// File App.tsx
<strong>
</strong>import { QueryClient, QueryClientProvider } from 'react-query';

// membuat instance dari QueryClient dengan default value 
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      refetchOnReconnect: false,
      refetchOnWindowFocus: false,
    },
  },
});

function App() {
  return (
    &#x3C;QueryClientProvider client={queryClient}>
      &#x3C;Router />
    &#x3C;/QueryClientProvider>
  )
}

export default App

</code></pre>

```
```
