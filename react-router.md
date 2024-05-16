# React Router

## Installation

```sh
pnpm add react-router-dom
```

## Create Router

```typescript
// router.tsx

import { BrowserRouter, Route, Routes } from "react-router-dom";

function Router() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<div>Home</div>} />
        <Route path="/order-management" element={<div>Order Management</div>} />
        <Route path="/trip-tracking/:orderId" element={<div>Trip Tracking</div>} />
      </Routes>
    </BrowserRouter>
  );
}

export default Router;
```

```typescript
// App.tsx
// Import & use router
import Router from './router'

export default function App() {
  return <Router />
}
```

## Navigation

Pada react router kita dapat menggunakan 2 cara navigasi, secara explisit dan implisit. secara implisit kita menggunakan `NavLink` dan secara explisit kita bisa menggunakan `useNavigation`

<pre class="language-typescript"><code class="lang-typescript">// Home.tsx
// Implisit Navigation
<strong>import { NavLink } from 'react-router-dom';
</strong>
export default function Home() {
  return (
    &#x3C;div>
        &#x3C;h1>Home&#x3C;/h1>
<strong>        &#x3C;NavLink to='/order-management'>Ke Halaman Order Management&#x3C;/NavLink>
</strong>    &#x3C;/div>
  )
}
</code></pre>

<pre class="language-typescript"><code class="lang-typescript">// Home.tsx
// Explisit Navigation
<strong>import { useNavigate } from 'react-router-dom';
</strong>
export default function Home() {
  const navigate = useNavigate();

    const handleClickButton = () => {
<strong>        navigate('/order-management', {
</strong><strong>            replace: true // Optional, jika ingin replace dan menghapus history route sebelumnya
</strong><strong>        })
</strong>    }

  return (
    &#x3C;div>
        &#x3C;h1>Home&#x3C;/h1>
        &#x3C;button onClick={handleClickButton}>Ke Halaman Order Management&#x3C;/button>
    &#x3C;/div>
  )
}
</code></pre>

## useParams

useParams adalah hooks function yang digunakan untuk mendapatkan key/value pada sebuah dynamic route yang match dengan path yang telah dibuat. pada contoh sebelumnya terdapat route berikut

```typescript
<Route path="/trip-tracking/:orderId" element={<div>Trip Tracking</div>} />
```

useParams digunakan untuk mendapatkan value dari _**orderId.**_ sebagai contoh sebagai berikut

<pre class="language-typescript"><code class="lang-typescript">// pages/trip-tracking.tsx
<strong>import { useParams } from "react-router-dom";
</strong>
export default function TripTracking() {
<strong>  const { orderId } = useParams&#x3C;{ orderId?: string }>();
</strong>
  return &#x3C;div>TripTracking with order id : {orderId}&#x3C;/div>;
}
</code></pre>

<pre class="language-typescript"><code class="lang-typescript">// route.tsx
// Modify Route path trip tracking
import { BrowserRouter, Route, Routes } from "react-router-dom";
<strong>import TripTracking from "./pages/trip-tracking";
</strong>
function Router() {
  return (
    &#x3C;BrowserRouter>
      &#x3C;Routes>
         ...
<strong>        &#x3C;Route path="/trip-tracking/:orderId" element={&#x3C;TripTracking />} />
</strong>         ...
      &#x3C;/Routes>
    &#x3C;/BrowserRouter>
  );
}

export default Router;
</code></pre>

## useSearchParams

`useSearchParams` adalah hooks function yang digunakan untuk mendapatkan value dari search param pada url, selain itu kita dapat modify dan juga menghapus search params tersebut.

```typescript
// pages/order-management.tsx
import { useSearchParams } from "react-router-dom";

export default function OrderManagement() {
  const [searchParams, setSearchParams] = useSearchParams();

  // Get data search params
  const currentPage = searchParams.get('page') ;
  const currentLimit = searchParams.get('limit');

  const handleClickModify = () => {
    // Update value params & set into url
    searchParams.set('page', '2')
    setSearchParams(searchParams)
  }

  const handleClickDelete = () => {
    // Delete value params & set into url
    searchParams.delete('page')
    setSearchParams(searchParams)
  }

  return (
    <div>
        <h1>Order Management</h1>
        <button onClick={handleClickModify}>modify params url</button>
        <button onClick={handleClickDelete}>hapus params page</button>
        <p>Current Page : {currentPage}, Current Limit : {currentLimit}</p>
    </div>
  )
}
```
