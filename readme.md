# Getting Started with NodeJS

As we know in nodejs we can build everything in only one file wish is index.js but that's not great for future development so here I am gonna represent an easy structure and explain everything for you to start organizing your project architecture.

**If its the first time using nodejs, please install nodejs before following me**

First, we will start by creating a new folder, Init nodejs, and opening our node project with vscode like the screenshot below.

![Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled.png](Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled.png)

when you open vscode you will find only one file wish is package.json

first, we need to install express wish is a nodejs framework that makes a lot of things easier for us
so let us open vscode terminal or any other one and install the dependencies we need now!

```bash
npm install express
```

---

so lets create our first file wish is **app.js**

```bash
touch app.js
```

and lets add this code

```jsx
const express = require("express");

const app = express();

app.use(express.json());
app.use("/", (req, res) => res.send("Hello world!"));

module.exports = app;
```

Here we are creating our express app, first, we imported express initialized express in a const named app and used express.json to handle JSON parsing, sent a Hello world text when requesting the "/" route and finally we exported it!

---

Now lets create our **server.js**

```bash
touch server.js
```

And lets add this code

```jsx
const app = require("./app");
const port = 8000;

app.listen(port, () => {

console.log(`App running on ${port}...`);

});
```

So as you can see we imported our app module and created our port wish the application will work on and we started or app.
let's start our server.js file!

```bash
node server.js
```

and thats the result our app is running on port 8000

![Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%201.png](Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%201.png)

Now lets visit [http://localhost:8000](http://localhost:8000/)/ you will see Hello world !

![Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%202.png](Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%202.png)

We just build our Hello world with nodeJS! Now let's make something more interesting by building a simple crud application to create, read, update, and delete Products.
So in this case we need a place to store data! we gonna use a simple variable to do that but in the next chapter we will use a database

---

Lets add the following code in app.js file to create , and retrieve products data .

```bash
app.get("/products", (req, res) => {
  res.json(products);
});

app.post("/products", (req, res) => {
  const body = req.body;
  products.push(body);
  res.json(body);
});
```

As you can see we just returned the products array in JSON format when we make a get request to /products endpoint
the second function let us push a new product to the product array and return the data we added
Now let's do the update and delete part :

```jsx
app.delete("/products/:id", (req, res) => {
  const id = req.params.id;
  const filtredProducts = products.filter((value, index) => index != id);
  products = filtredProducts;
  res.json(filtredProducts);
});
app.patch("/products/:id", (req, res) => {
  const id = req.params.id;
  const body = req.body;
  products[id] = body;
  res.json(products);
});
```

In these lines of code, we just made two routes the first to delete a product and the second to update one.
firstly we took the id and we filtered the array to take the products that don't match our id and updated them with the filtered ones.
Secondly, we updated the product that got the same index as our id and updated the data with the one in the body.

---

Our final App.js code : 

```jsx
const express = require("express");

let products = [];
const app = express();

app.use(express.json());
app.get("/products", (req, res) => {
  res.json(products);
});

app.post("/products", (req, res) => {
  const body = req.body;
  products.push(body);
  res.json(body);
});
app.delete("/products/:id", (req, res) => {
  const id = req.params.id;
  const filtredProducts = products.filter((value, index) => index != id);
  products = filtredProducts;
  res.json(filtredProducts);
});
app.patch("/products/:id", (req, res) => {
  const id = req.params.id;
  const body = req.body;
  products[id] = body;
  res.json(products);
});
app.use("/", (req, res) => res.send("Hello world!"));

module.exports = app;
```

To test our api we gonna use a tool named Postman

![Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%203.png](Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%203.png)

**Sending post request to add product**

![Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%204.png](Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%204.png)

Sending get request to retrieve products

![Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%205.png](Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%205.png)

Sending delete request to delete a product

![Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%206.png](Getting%20Started%20with%20NodeJS%20e7b75e7e24aa40fbaaa0c98bb2596d0f/Untitled%206.png)

Sending patch request to update a product

This was a brief introduction to Express and nodejs in the next chapters we will do more interesting things like Using MongoDB, creating our structure, and splitting our code