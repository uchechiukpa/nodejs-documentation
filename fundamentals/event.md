# 🎣 Event

![](../.gitbook/assets/eventEmitters.png)

### _<mark style="color:blue;">**Introduction**</mark>_

A lot of Node.js core [API](https://en.wikipedia.org/wiki/API) is built around an asynchronous event-driven architecture in which certain kinds of objects called _<mark style="color:blue;">**emitters**</mark>_,  emit named events that cause _<mark style="color:blue;">**functions**</mark>_ called _<mark style="color:blue;">**listeners**</mark>_ to be called.



For Example,&#x20;

* A net.server object emits an event each time a peer connects to it,
* A fs.ReadStream emits an event when a file is opened,
* A stream emits an event whenever data is available to be read, etc.



The following example shows a simple EventEmitter instance with listeners. All objects that emit events are instances of the _<mark style="color:blue;">**EventEmitter**</mark>_ class.&#x20;

{% tabs %}
{% tab title="TS" %}
```typescript
import EventEmitter from "events"
class MyEmitter extends EventEmitter {}
const emitter = new MyEmitter();

// First listener
emitter.on('event', function firstListener() {
  console.log('Helloooo! first listener');
});

// Second listener
emitter.on('event', function secondListener() {
  console.log(`event in second listener`);
});

// Third listener
emitter.on('event', function thirdListener() {
  console.log(`event in third listener`);
});

//prints all the listerners on the eventName 'event'
console.log(myEmitter.listeners('event'));

myEmitter.emit('event', 1, 2, 3, 4, 5);


// Prints:
// [
//   [Function: firstListener],
//   [Function: secondListener],
//   [Function: thirdListener]
// ]
// Helloooo! first listener
// event with parameters 1, 2 in second listener
// event with parameters 1, 2, 3, 4, 5 in third listener
```
{% endtab %}

{% tab title="Untitled" %}

{% endtab %}
{% endtabs %}

{% hint style="info" %}
Event names are camel-cased strings but any valid JavaScript property key can be used.
{% endhint %}

The _<mark style="color:blue;">**eventEmitter.on()**</mark>_ method is used to register listeners, it adds the _<mark style="color:blue;">**listener**</mark>_ function to the end of the listener array of the name _<mark style="color:blue;">**EventName**</mark>_ ~~.~~

{% hint style="warning" %}
Note, No checks are made to see if the _<mark style="color:blue;">**listener**</mark>_ has already been added. Multiple calls passing the same combination of _<mark style="color:blue;">**eventName**</mark>_ and _<mark style="color:blue;">**listener**</mark>_ will result in the _<mark style="color:blue;">**listener**</mark>_ being added and called multiple times.
{% endhint %}

The _<mark style="color:blue;">**eventEmitter.emit()**</mark>_ method synchronously calls each of the _<mark style="color:blue;">**listener's**</mark>_ function registered, for the event named _<mark style="color:blue;">**eventName**</mark>_,  it calls them in the order they where registered and passes the supplied arguments to each. Think of it as an array, when a listener is registered it is pushed into an array, and when the _<mark style="color:blue;">**emit**</mark>_ method is called it loops through the array and calls each listener.



### _<mark style="color:blue;">**Passing argument and**</mark>** **<mark style="color:orange;">**this**</mark>** **<mark style="color:blue;">**to listeners.**</mark>_

The _<mark style="color:blue;">**eventEmitter.emit()**</mark>_ method allows an unlimited set of arguments to passed to the listener functions.&#x20;

{% hint style="info" %}
Please note,  when an ordinary listener function is called, the standard _<mark style="color:blue;">**this**</mark>_ keyword is intentionally set to reference the _<mark style="color:blue;">**EventEmitter**</mark>_ instance to which the listener is attached.
{% endhint %}

```typescript
import EventEmitter from "events"
class MyEmitter extends EventEmitter {}
const emitter = new MyEmitter();

// First listener
emitter.on('event', function firstListener() {
  console.log('Helloooo! first listener');
});

// Second listener
emitter.on('event', function secondListener(arg1, arg2) {
  console.log(`event with parameters ${arg1}, ${arg2},this, this === myEmitter in second listener`);
});

// Third listener
emitter.on('event', function thirdListener(...args) {
  const parameters = args.join(', ');
  console.log(`event with parameters ${parameters} in third listener`);
});

//prints all the listerners on the eventName 'event'
console.log(myEmitter.listeners('event'));

myEmitter.emit('event', 1, 2, 3, 4, 5);


// Prints:
// [
//   [Function: firstListener],
//   [Function: secondListener],
//   [Function: thirdListener]
// ]

// Helloooo! first listener
// event with parameters 1, 2, MyEmitter {
//     domain: null,
//     _events: { event: [Function] },
//     _eventsCount: 1,
//     _maxListeners: undefined } true in second listener
// event with parameters 1, 2, 3, 4, 5 in third listener
```

{% hint style="info" %}
you can also use ES6 Arrow Functions as listeners, however, when doing so, the _<mark style="color:blue;">**this**</mark>_ keyword will no longer reference the EventEmitter instance:
{% endhint %}

```typescript
const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  console.log(a, b, this);
  // Prints: a b {}
});
myEmitter.emit('event', 'a', 'b');
```



### _<mark style="color:blue;">**Asynchronous vs Synchronous**</mark>_&#x20;

The _<mark style="color:blue;">**EventEmitter**</mark>_ calls all listeners synchronously in the order in which they were registered. This ensures the proper sequencing of events and helps avoid race conditions and logic errors. When appropriate, listener functions can switch to an asynchronous mode of operation using the _<mark style="color:blue;">**setImmediate()**</mark>_ or  _<mark style="color:blue;">**process.nextTick()**</mark>_ process methods:



\
