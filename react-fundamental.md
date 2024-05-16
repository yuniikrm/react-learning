# React Fundamental

Berikut adalah beberapa aspek penting dari pemrograman React:

## Component-Based Architectiure&#x20;

React menggunakan arsitektur berbasis komponen, di mana UI dibangun dengan menyusun komponen kecil yang dapat digunakan kembali. Setiap komponen terdiri dari logika dan UI-nya sendiri.

```jsx
function Car() {
  return <h2>Hi, I am a Car!</h2>;
}
```

## Virtual DOM

React menggunakan DOM virtual (Document Object Model) untuk mengoptimalkan pembaruan UI. Daripada memanipulasi DOM browser secara langsung, React memperbarui representasi DOM dalam memori yang ringan yang disebut DOM virtual. React kemudian membandingkan DOM virtual dengan DOM sebenarnya dan hanya memperbarui bagian DOM yang telah diubah, meminimalkan manipulasi DOM dan meningkatkan kinerja.

## JSX React

JSX adalah singkatan dari JavaScript XML. Ini adalah ekstensi sintaks untuk JavaScript yang memungkinkan Anda menulis kode HTML dalam file JavaScript tanpa perlu menggabungkan string atau membuat objek DOM secara manual. Dengan JSX, Anda dapat mendefinisikan struktur tampilan komponen menggunakan sintaks yang mirip dengan HTML, membuatnya lebih mudah dipahami daripada metode tradisional seperti manipulasi DOM secara langsung menggunakan JavaScript.

Contoh sederhana penggunaan JSX dalam React: &#x20;

```jsx
import React from 'react';

// Definisikan komponen dengan JSX
function App() {
  return (
    <div>
      <h1>Hello, World!</h1>
      <p>This is a React component with JSX.</p>
    </div>
  );
}

export default App;

```

## React ES6

React menggunakan ECMAScript 6 untuk penulisan code, beberapa yang perlu diperhatikan

#### Arrow Functions

Memungkinkan untuk menulis syntax lebih singkat jika dalam fungsi hanya terdapat 1 statement dan mengembalikan nilai value, maka tanda kurung _brackets_ dan _return_ tidak diperlukan

```jsx
const hello = () => {
  return "Hello World!";
}

const hello = () => "Hello World!";
const hello = (val) => "Hello " + val;
```

#### Variables

Ada 3 cara untuk mendefinisikan variables, `var`, `let`, and `const`.

Var:&#x20;

Jika menggunakan var di luar suatu fungsi, maka var termasuk dalam cakupan global.&#x20;

Jika var di dalam suatu fungsi, maka var hanya menjadi milik fungsi tersebut.&#x20;

Jika menggunakan var di dalam blok, seperti perulangan for atau if else, variabel masih bisa terbaca di luar blok itu.

```jsx
var x = 5.6;
```

Let:  sama seperti var hanya saja terbatas pada blok (atau ekspresi) di mana ia didefinisikan. Jika Anda menggunakan let di dalam sebuah blok, yaitu perulangan for, variabel hanya tersedia di dalam perulangan itu saja.

```jsx
let x = 5.6;
```

Const: adalah variabel yang setelah dibuat, nilainya tidak akan pernah berubah. Const tidak dapat di-reassign, tetapi property nya bisa diubah untuk const yang berupa array dan object

```jsx
const x = 5.6;
```

#### Array Methods

Salah satu yang paling sering digunakan di React adalah metode array .map(). Metode .map() memungkinkan Anda menjalankan fungsi pada setiap item dalam array, dan mengembalikan array baru sebagai hasilnya.

```jsx
const myArray = ['apple', 'banana', 'orange'];
const myList = myArray.map((item) => <p>{item}</p>)

const myObjArray = [{ name: "user", id: 1 }, { name: "user 2", id: 2 }]
const myObjList = myObjArray.map((item) => <p>{item.name}</p>)

// example return new object array
const newArray = myArray.map((a) => ({ fruitName: a })) 
console.log(newArray) // [{ fruitName: 'apple' }, { fruitName: 'banana' }, { fruitName: 'orange' }]
```

#### Destructuring

Destrukturisasi adalah cara untuk mengekstrak atau mengambil hanya beberapa item yang dibutuhkan dari sebuah array atau object.

```jsx
// Destrukturing Array
const vehicles = ['mustang', 'f-150', 'expedition'];
const [car, truck, suv] = vehicles;

// Destrukturing Object
const vehicleOne = {
  brand: 'Ford',
  model: 'Mustang',
  type: 'car',
  year: 2021, 
  color: 'red'
}
const { brand, model } = vehicleOne;

myVehicle(vehicleOne);

function myVehicle({type, color, brand, model}) {
  const message = 'My ' + type + ' is a ' + color + ' ' + brand + ' ' + model + '.';
}
```

#### Spread Operator

Operator spread JavaScript (...) memungkinkan kita dengan cepat menyalin semua atau sebagian dari array atau objek yang ada ke dalam array atau objek lain.

```jsx
// Spread Array
const numbersOne = [1, 2, 3];
const numbersTwo = [4, 5, 6];
const numbersCombined = [...numbersOne, ...numbersTwo];


// Spread Object
const myVehicle = {
  brand: 'Ford',
  model: 'Mustang',
  color: 'red'
}
const updateMyVehicle = {
  type: 'car',
  year: 2021, 
  color: 'yellow'
}
const myUpdatedVehicle = {...myVehicle, ...updateMyVehicle}
```

## State

Digunakan untuk menyimpan data dinamis di dalam sebuah komponen dan memungkinkan komponen tersebut untuk merender ulang saat data berubah. Dengan menggunakan state, komponen dapat merespon terhadap perubahan data, dan menampilkan secara langsung.

```jsx
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("black");
  
  return <h1>My favorite color is {color}!</h1>
}
```

## Props

Props (singkatan dari properties) adalah cara untuk mentransfer data dari parent component ke child component dalam React.&#x20;

```jsx
function Car(props) {
  return <h2>I am a { props.brand }!</h2>;
}

function Garage() {
  return (
    <>
      <h1>Who lives in my garage?</h1>
      <Car brand="Ford" />
    </>
  );
}
```

## Hooks

merupakan fungsi yang memungkinkan Anda untuk “mengaitkan” _state_ dan fitur-fitur _lifecycle_ React dari _function component_. Basic Hooks yang akan sering digunakan adalah _useState_ dan _useEffect_. Untuk info lebih detail lihat [disini](https://www.w3schools.com/react/react\_hooks.asp).

#### useState

React useState Hook memungkinkan kita melacak state dalam komponen atau fungsi, umumnya mengacu pada data atau properti yang perlu dilacak dalam suatu aplikasi.

#### useEffect

useEffect Hook memungkinkan Anda mengeksekusi efek pada komponen Anda berdasarkan variable tertentu.

```jsx
useEffect(() => {
  //Runs only on the first render
}, []);

useEffect(() => {
  //Runs on the first render
  //And any time any dependency value changes
}, [prop, state]);
```

## Events

&#x20;Sama seperti event HTML DOM, React memiliki event yang sama dengan HTML: click, change, mouseover, dll ditulis dalam sintaks camelCase:

onClick, bukan onclick. Penulisan event React ditulis di dalam kurung kurawal:

onClick={shoot}.

```jsx
function Football() {
  const shoot = () => {
    alert("Great Shot!");
  }

  return (
    <button onClick={shoot}>Take the shot!</button>
  );
}
```

```jsx
// Contoh dengan tambahan parameter dalam fungsi shoot
function Football() {
  const shoot = (a) => {
    alert(a);
  }

  return (
    <button onClick={() => shoot("Goal!")}>Take the shot!</button>
  );
}
```

## Conditional Rendering

Dalam React, Anda dapat menampilkan UI secara kondisional, ada beberapa cara yang dapat dilakukan

#### `if` Statement

```jsx
function Goal() {
  const isGoal = true;
  if (isGoal) {
    return <div>Goal!</div>;
  }
  return <div>Missed!</div>;
}
```

#### Logical `&&` Operator

```jsx
function Garage() {
  const cars = ['Ford', 'BMW', 'Audi'];
  return (
    <>
      <h1>Garage</h1>
      {cars.length > 0 &&
        <h2>
          You have {cars.length} cars in your garage.
        </h2>
      }
    </>
  );
}
```

#### Ternary Operator

```jsx
function Goal(props) {
  const isGoal = props.isGoal;
  return (
    <>
      { isGoal ? <div>Goal!</div> : <div>Missed!</div> }
    </>
  );
}
```

## Modules Export & Import

Di React, ekspor dan impor digunakan untuk berbagi kode antar file yang berbeda.

**Ekspor** digunakan ketika Anda ingin membuat fungsi, komponen, atau variabel tersedia untuk digunakan di file lain, sedangkan **Import** digunakan untuk memasukkan fungsi, komponen, atau variabel yang telah Anda ekspor dari file lain.

Terdapat 2 jenis export yaitu `export default` dan `export` biasa (named export).

&#x20;`export default` digunakan untuk mengekspor hanya satu nilai dari sebuah file, seperti komponen React. Untuk mengimpor tidak memerlukan kurung kurawal

Contoh export default:

```jsx
// File: MyComponent.js
import React from 'react';

function MyComponent() {
  return (
    <div>
      <h1>Hello, World!</h1>
    </div>
  );
};

export default MyComponent;

```

```jsx
import MyComponent from './MyComponent';
```

Sedangkan `export` biasa (atau named export) digunakan untuk mengekspor banyak nilai. Saat mengimpor, Anda harus menggunakan kurung kurawal dan nama yang tepat dari nilai yang diekspor.

```jsx
// File: MyUtilities.js
export const utility1 = ...;
export function utility2() { ... };
```

```jsx
import { utility1, utility2 } from './MyUtilities';
```
