# The JS Event Loop

![how-the-event-loop-works.png](how-the-event-loop-works.png)

![event-loop.png](event-loop.png)

* Your JavaScript code runs single threaded. There is just one thing happening at a time.
    * Pay attention to how you write your code and avoid anything that could block the thread, like synchronous network calls or long loops.
    * In most browsers there is an event loop for every browser tab, to avoid a web page with heavy processing to block your entire browser.
    * Web Workers run in their own event loop as well

## Web Workers

### /local/src/uai/uai2015/simple-web-worker

* [Repo de ejemplo](https://github.com/SYTW/simple-web-worker)

## Race Condition

### /local/src/uai/uai2015/race-condition/index.html

* [Repo de Ejemplo](https://github.com/ULL-MII-SYTWS-1920/js-race)


## Promises

### local/src/uai/uai2015/promise-ejemplo

* [A Gist with a very Simple Example of How to make and use a Promise](https://gist.github.com/crguezl/f5c52c8b72b4722e374a8af10e9d2b5d)

## Códigos Ilustrando el Bucle de Eventos


### tema1-introduccion/practicas/p2-t1-c3-file-system/event-loop/callstack.js 

* Tutorial [Concurrency model and Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop) at https://developer.mozilla.org

```js
function multiply(x,y) {
  // console.trace imprime una traza de la pila
  console.trace("-----------At multiply-----------");
  return x * y;
}

function squared(n) {
  console.trace("-----------At squared-----------");
  return multiply(n,n)
}

function printSquare(n) {
   return squared(n)
}

let numberSquared = printSquare(5);
console.log(numberSquared);
```

### tema1-introduccion/practicas/p2-t1-c3-file-system/event-loop/settimeout-does-not-run-inmediately.js 

* Tutorial [Concurrency model and Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop) at https://developer.mozilla.org


```js
const s = new Date().getSeconds();

setTimeout(function() {
  console.log("Ran after " + (new Date().getSeconds() - s) + " seconds");
}, 500);

while(true) {
  if(new Date().getSeconds() - s >= 2) {
    console.log("Good, looped for 2 seconds");
    break;
  }
}
```

### tema1-introduccion/practicas/p2-t1-c3-file-system/event-loop/order.js 

* Tutorial [Concurrency model and Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop) at https://developer.mozilla.org


```js
(function() {

  console.log('this is the start');

  setTimeout(function cb() {
    console.log('Callback 1: this is a msg from call back');
  }); // has a default time value of 0

  console.log('this is just a message');

  setTimeout(function cb1() {
    console.log('Callback 2: this is a msg from call back');
  }, 0);

  console.log('this is the end');

})();
```

## References

* Tutorial [Concurrency model and Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop) at https://developer.mozilla.org
* [The JavaScript Event Loop](https://flaviocopes.com/javascript-event-loop/) by Flavio
* [Philip Roberts: ¿Que diablos es el "event loop" (bucle de eventos) de todos modos? (JSConf EU)](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
* [loupe](http://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D) a tool in the cloud to see the event loop working