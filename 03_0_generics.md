# Generics

<!--
  Definition
  Why to use
-->

---

* [Generic constraints](#generic-constraints)

---

Let's say that we have a `Queue` class that implements a Queue data Structure.

```ts
class Queue {
  messages: any[] = []

  push(message: any): void {
    this.messages.push(message);
  }

  pop() {
    return this.messages.shift();
  }
}

const q = new Queue();

q.push('Hello');
q.push('Hi');
q.push(1);
q.push('Hola');

console.log(q);
// Queue: {
//   "messages": [
//     "Hello",
//     "Heo",
//     1,
//     "Hi"
//   ]
// } 

console.log(q.pop().toUpperCase()); // HELLO
console.log(q.pop().toUpperCase()); // HE
console.log(q.pop().toUpperCase()); // Error: q.pop(...).toUpperCase is not a function 
```

This `Queue` accepts any message data type. You can pass a string, number, object...

However, this flexibility can end in `runtime errors`.

In the previous example we first push a `string` and then a `number`.
Then, we assume the `Queue` is an array of `strings` and decide to uppercase each message. 

Once we reach the element `1` we receive the following error:

```
[ERR]: q.pop(...).toUpperCase is not a function
```

As you know, there is no toUpperCase method for the Number object.

We could fix this creating a `subclass` for just `strings`, example: `QueueString`

```ts
class Queue {
  messages: any[] = []

  push(message: any): void {
    this.messages.push(message);
  }

  pop() {
    return this.messages.shift();
  }
}

class QueueString extends Queue {
  constructor() {
    super();
  }

  push(message: string): void {
    this.messages.push(message);
  }

  pop() {
    return this.messages.shift();
  }  
}

const q = new QueueString();

q.push('Hello');
q.push('Hi');
q.push(1); // Argument of type 'number' is not assignable to parameter of type 'string'.
```

If we try to push anything else but a `string` we will receive the following error:

```
Argument of type 'number' is not assignable to parameter of type 'string'.
```

But what happened if we need to support multiple data types. We'd probably end creating different subclasses for each data type: `QueueNumber`, `QueueObject`...

To avoid specific classes we can use `Generics`

We can add a generic type parameter as an argument to the Queue class. 
Then, we specify the type of `message` and the return type of `pop()`.
Lastly, we use `!` (non-null assertion operator), to tell TS that the message is always going to be a `string` (in this case) and it **will not** be undefined or null.

When we initialize a new `Queue`, we pass in the generic type argument. In this case, `string`

```ts
class Queue<T> {
  messages: Array<T> = []

  push(message: T): void {
    this.messages.push(message);
  }

  pop(): T {
    return this.messages.shift()!;
  }
}

const q = new Queue<string>();

q.push('Hello');
q.push('Hi');
q.push(1); // Argument of type 'number' is not assignable to parameter of type 'string'.
```

Now if we try to push a number, we will see the expected error:

```
Argument of type 'number' is not assignable to parameter of type 'string'.
```

## Generic constraints

<!-- 
  TODO:
    What is?
-->

Example: `<T extends Order>`

In the following example, we have the function `processOrder()` that...
1. Takes an `order` (object) of type `T`
3. The object that takes (`T`) conforms to the type Order (`<T extends Order>` without this, we would nolt be able to access the order properties like `order.shopper`)
2. Returns a `new object` containing:
  * The order (object of type T)
  * orderId
  * name

```ts
type Products = {
  [k: string]: object
}

type Order = {
  products: Products,
  shopper: string
}

function processOrder<T extends Order>(order: T, orderId: number): T & { orderId: number } & { name: string } {
  return {
    ...order,
    orderId,
    name: `${order.shopper}`
  }
}

const order = {
  products: {
    candies: {
      quantity: 10
    }
  },
  shopper: 'Peter Pan'
}


const processedOrder = processOrder(order, 1000);

console.log(processedOrder);
// {
//   "products": {
//     "candies": {
//       "quantity": 10
//     }
//   },
//   "shopper": "Peter Pan",
//   "orderId": 1000,
//   "name": "Peter Pan"
// } 
```