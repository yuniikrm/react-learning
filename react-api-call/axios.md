# Axios

Axios adalah sebuah pustaka JavaScript yang digunakan untuk membuat permintaan HTTP dari sisi klien di lingkungan Node.js atau di browser. Ini adalah alat yang populer dan sering digunakan untuk berkomunikasi dengan API dari aplikasi web atau server.

## Installation

```sh
pnpm add axios
```

## GET Request

<pre class="language-typescript"><code class="lang-typescript">// App.tsx
<strong>import axios from "axios";
</strong>import { useEffect, useState } from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts/1";

export default function App() {
  const [post, setPost] = useState&#x3C;{ title: string; body: string } | null>(
    null
  );

  useEffect(() => {
<strong>    axios.get(baseURL).then((response) => {
</strong><strong>      setPost(response.data);
</strong>    });
  }, []);

  if (!post) return null;

  return (
    &#x3C;div>
      &#x3C;h1>{post.title}&#x3C;/h1>
      &#x3C;p>{post.body}&#x3C;/p>
    &#x3C;/div>
  );
}
</code></pre>

## POST Request

<pre class="language-typescript"><code class="lang-typescript">// App.tsx
import axios from "axios";
import { useEffect, useState } from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts";

export default function App() {
  const [post, setPost] = useState&#x3C;{ title: string; body: string } | null>(null);

  useEffect(() => {
    axios.get(`${baseURL}/1`).then((response) => {
      setPost(response.data);
    });
  }, []);

<strong>  function createPost() {
</strong><strong>    axios
</strong><strong>      .post(baseURL, {
</strong><strong>        title: "Hello World!",
</strong><strong>        body: "This is a new post."
</strong><strong>      })
</strong><strong>      .then((response) => {
</strong><strong>        setPost(response.data);
</strong><strong>      });
</strong><strong>  }
</strong>
  if (!post) return "No post!"

  return (
    &#x3C;div>
      &#x3C;h1>{post.title}&#x3C;/h1>
      &#x3C;p>{post.body}&#x3C;/p>
<strong>      &#x3C;button onClick={createPost}>Create Post&#x3C;/button>
</strong>    &#x3C;/div>
  );
}

```
</code></pre>

## PUT Request

<pre class="language-typescript"><code class="lang-typescript">// App.tsx
import axios from "axios";
import { useEffect, useState } from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts";

export default function App() {
  const [post, setPost] = useState&#x3C;{ title: string; body: string } | null>(null);

  useEffect(() => {
    axios.get(`${baseURL}/1`).then((response) => {
      setPost(response.data);
    });
  }, []);

<strong>  function updatePost() {
</strong><strong>    axios
</strong><strong>      .put(`${baseURL}/1`, {
</strong><strong>        title: "Hello World!",
</strong><strong>        body: "This is an updated post."
</strong><strong>      })
</strong><strong>      .then((response) => {
</strong><strong>        setPost(response.data);
</strong><strong>      });
</strong><strong>  }
</strong>
  if (!post) return "No post!"

  return (
    &#x3C;div>
      &#x3C;h1>{post.title}&#x3C;/h1>
      &#x3C;p>{post.body}&#x3C;/p>
<strong>      &#x3C;button onClick={updatePost}>Update Post&#x3C;/button>
</strong>    &#x3C;/div>
  );
}
</code></pre>

## DELETE Request

<pre class="language-typescript"><code class="lang-typescript">// App.tsx
import axios from "axios";
import { useEffect, useState } from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts";

export default function App() {
  const [post, setPost] = useState&#x3C;{ title: string; body: string } | null>(null);

  useEffect(() => {
    axios.get(`${baseURL}/1`).then((response) => {
      setPost(response.data);
    });
  }, []);

<strong>  function deletePost() {
</strong><strong>    axios
</strong><strong>      .delete(`${baseURL}/1`)
</strong><strong>      .then(() => {
</strong><strong>        alert("Post deleted!");
</strong><strong>        setPost(null)
</strong><strong>      });
</strong><strong>  }
</strong>
  if (!post) return "No post!"

  return (
    &#x3C;div>
      &#x3C;h1>{post.title}&#x3C;/h1>
      &#x3C;p>{post.body}&#x3C;/p>
<strong>      &#x3C;button onClick={deletePost}>Delete Post&#x3C;/button>
</strong>    &#x3C;/div>
  );
}
</code></pre>

## Error Handling

<pre class="language-typescript"><code class="lang-typescript">// App.tsx
import axios from "axios";
import { useEffect, useState } from "react";

const baseURL = "https://jsonplaceholder.typicode.com/posts";

export default function App() {
  const [post, setPost] = useState&#x3C;{ title: string; body: string } | null>(null);
<strong>  const [error, setError] = useState&#x3C;{message: string} | null>(null);
</strong>
  useEffect(() => {
<strong>    // invalid url will trigger an 404 error
</strong>    axios.get(`${baseURL}/asdf`).then((response) => {
      setPost(response.data);
<strong>    }).catch(error => {
</strong><strong>      setError(error);
</strong><strong>    });
</strong>  }, []);
  
<strong>  if (error) return `Error: ${error.message}`;
</strong>  if (!post) return "No post!"

  return (
    &#x3C;div>
      &#x3C;h1>{post.title}&#x3C;/h1>
      &#x3C;p>{post.body}&#x3C;/p>
    &#x3C;/div>
  );
}
</code></pre>

## Create Instance

Kita dapat membuat instance baru dengan custom config.

<pre class="language-typescript"><code class="lang-typescript">// src/axios-helper.ts
import axios from "axios";

<strong>export const client = axios.create({
</strong><strong>    baseURL: "https://jsonplaceholder.typicode.com/posts",
</strong><strong>    headers: {
</strong>        'X-auth': 'navi',
        'X-key': 'xxxxxxx'
    }
});
</code></pre>

<pre class="language-typescript"><code class="lang-typescript">// App.tsx
import { useEffect, useState } from "react";
<strong>import { client } from "./axios-helper";
</strong>
export default function App() {
  const [post, setPost] = useState&#x3C;{ title: string; body: string } | null>(null);

  useEffect(() => {
<strong>    client.get("/1").then((response) => {
</strong>      setPost(response.data);
    });
  }, []);

  function deletePost() {
<strong>    client
</strong><strong>      .delete("/1")
</strong>      .then(() => {
        alert("Post deleted!");
        setPost(null)
      });
  }

  if (!post) return "No post!"

  return (
    &#x3C;div>
      &#x3C;h1>{post.title}&#x3C;/h1>
      &#x3C;p>{post.body}&#x3C;/p>
      &#x3C;button onClick={deletePost}>Delete Post&#x3C;/button>
    &#x3C;/div>
  );
}
</code></pre>

## Async Await

Kita bisa melakukan pemanggilan api request dengan async await, ini memungkinkan kita bisa menulis code yang lebih clean tanpa `then` dan `catch` callback function sehingga lebih mudah dipahami.

<pre class="language-typescript"><code class="lang-typescript">// App.tsx
import { useEffect, useState } from "react";
import { client } from "./axios-helper";

export default function App() {
  const [post, setPost] = useState&#x3C;{ title: string; body: string } | null>(
    null
  );

  useEffect(() => {
<strong>    async function getPost() {
</strong><strong>      const response = await client.get("/1");
</strong>      setPost(response.data);
    }
<strong>    getPost();
</strong>  }, []);

<strong>  async function deletePost() {
</strong><strong>    await client.delete("/1");
</strong>    alert("Post deleted!");
    setPost(null);
  }

  if (!post) return "No post!";

  return (
    &#x3C;div>
      &#x3C;h1>{post.title}&#x3C;/h1>
      &#x3C;p>{post.body}&#x3C;/p>
      &#x3C;button onClick={deletePost}>Delete Post&#x3C;/button>
    &#x3C;/div>
  );
}
</code></pre>

## Interceptors

Kita bisa melakukan intercept terhadap request dan response sebelum dilakukannya request api atau sebelum dihandle oleh then dan catch.

<pre class="language-typescript"><code class="lang-typescript">// src/axios-helper.ts
import axios, {
<strong>  AxiosRequestConfig,
</strong><strong>  AxiosError,
</strong><strong>  InternalAxiosRequestConfig,
</strong><strong>  AxiosResponse,
</strong>} from "axios";

export const client = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com/posts",
  headers: {
    "X-auth": "navi",
    "X-key": "xxxxxxx",
  },
});

<strong>// Interceptors
</strong><strong>const onRequestError = (error: AxiosError): Promise&#x3C;AxiosError> => {
</strong><strong>  console.error(`[request error] [${JSON.stringify(error)}]`);
</strong><strong>  return Promise.reject(error);
</strong><strong>};
</strong>
<strong>const onRequest = (config: AxiosRequestConfig): InternalAxiosRequestConfig => {
</strong><strong>  console.info(`[request] [${JSON.stringify(config)}]`);
</strong><strong>  config.headers = {
</strong><strong>    ...config.headers,
</strong><strong>    "X-Authorization": `Bearer xxxxxxx`,
</strong><strong>  };
</strong><strong>  return config as InternalAxiosRequestConfig;
</strong><strong>};
</strong>
<strong>const onResponseError = (error: AxiosError): Promise&#x3C;AxiosError> => {
</strong><strong>  console.error(`[response error] [${JSON.stringify(error)}]`);
</strong><strong>  return Promise.reject(error);
</strong><strong>};
</strong>
<strong>const onResponse = (response: AxiosResponse): AxiosResponse => {
</strong><strong>  console.info(`[response] [${JSON.stringify(response)}]`);
</strong><strong>  return response;
</strong><strong>};
</strong>
<strong>const interceptors = () => {
</strong><strong>  client.interceptors.request.use(onRequest, onRequestError);
</strong><strong>  client.interceptors.response.use(onResponse, onResponseError);
</strong><strong>};
</strong>
<strong>interceptors()
</strong></code></pre>
