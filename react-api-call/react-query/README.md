# React Query

## Installation

```sh
pnpm add @tanstack/react-query
```

## Definition

React Query adalah sebuah library yang digunakan untuk memudahkan proses pemanggilan API dengan beberapa fitur utama yaitu:

* Data Fetching: Mempermudah pemanggilan API, menyediakan hooks & state yang mempermudah proses (refetch, isLoading).
* Caching: Melakukan cahe dengan otomatis, mengurangi pemanggilan API yang tidak perlu untuk meningkatkan performa.
* Pagination & Infinite Scroll: Menyediakan fungsi untuk pagination & infinite scroll yang bisa langsung digunakan.
* Mutation Management: Mempermudah proses Create, Update, Delete di dalam server (POST, PUT, DELETE).
* Query Invalidation: Pemanggilan API dapat di-invalidate / di-refetch ketika ada data yang berubah. Hal ini memastikan konsistensi dalam pemanggilan API tersebut
