# React Composition

Dalam React, composition mengacu pada bagaimana cara membangun komponen dengan merakit komponen-komponen yang lebih kecil dan dapat digunakan kembali. Pendekatan ini memungkinkan pembuatan UI yang kompleks dengan penyusun blok yang lebih sederhana, mendorong penggunaan kembali kode, kemudahan pemeliharaan, dan skalabilitas.&#x20;

Ada beberapa composition di React:

#### Props Composition

Meneruskan props dari parent component ke child component. Dengan meneruskan props yang berbeda, Anda dapat menyesuaikan behaviour dan tampilan dari child component

```jsx
function ParentComponent() {
  return (
    <div>
      <ChildComponent value="Component 1" />
      <ChildComponent value="Component 2" />
    </div>
  );
}

function ChildComponent(props) {
  return (
    <div>Hello! from {props.value}</div>
  )
}

function App() {
  return (
    <ParentComponent />
  );
}
```

**Children Composition**

Anda juga dapat menggunakan prop `children` untuk menyusun komponen dengan menumpuknya satu sama lain.

```jsx
function ParentComponent({ children }) {
  return (
    <div>
      {children}
    </div>
  );
}

function App() {
  return (
    <ParentComponent>
      <ChildComponent1 />
      <ChildComponent2 />
    </ParentComponent>
  );
}
```

**Higher-Order Components (HOCs)**

HOC adalah fungsi yang mengambil komponen dan mengembalikan komponen baru dengan fungsionalitas tambahan. Hal ini memungkinkan Anda menyusun komponen dengan menyempurnakannya menggunakan logika yang dapat digunakan kembali.

```jsx
function withLogger(WrappedComponent) {
  return function WithLogger(props) {
    console.log("Props:", props);
    return <WrappedComponent {...props} />;
  };
}

const EnhancedComponent = withLogger(MyComponent);
```

**Render Props**:

Render Props merupakan teknik berbagi kode antar komponen React menggunakan prop yang nilainya berupa fungsi yang mengembalikan elemen.

```jsx
function App() {
const data = 'App'
    return (
      <div>
        <h1>Hello!</h1>
        <Mouse render={() => (
          <div>hello from render {app}</div>
        )}/>
      </div>
    );
}

function CustomComponent(props) {
  return (
    <div>
      <div>Inside custom component</div>
      {props.render}
    </div>
  )
}
```
