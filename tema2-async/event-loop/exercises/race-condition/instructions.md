---
title: Race Conditions
---

## Loading an image with some delay

Consider this file `index.html`: 

```html
{% include_relative index.html %}
```

### Experiment

Copy and serve this file [index.html](index.html) with:

```
http-server -p 9000 -o
```

with this line uncommented 
```js
let waitFor = 1000;
```

Can you see the infinite loop image?

Now  comment the line where `waitFor` is initialized and uncomment the other:

```js
let waitFor = 0;
```

and run:

```
http-server -p 8000 -o
```

(Change the port to avoid cache problems)

What do you think it will happen? Can you explain it?

Where is it:

```
➜  race-condition git:(curso2021) ✗ ls ~/campus-virtual/2021/sytws2021/apuntes/tema2-async/event-loop/exercises/race-condition
index.html          infinity-loop.png   instructions.md     not-race-example.js race-example.js
```

{% include image.html url="/assets/images/event-loop.png" description="<i>There’s an endless loop, when JavaScript engine waits for tasks, executes them and then sleeps waiting for more tasks</i>" %}

### Comentarios

* [Comentarios](comments)

### References 

* [Meta repo de la Charla UAI2015](https://github.com/ULL-MII-SYTWS-1920/uai2015)
  * [Repo de Ejemplo ULL-MII-SYTWS-1920/js-race](https://github.com/ULL-MII-SYTWS-1920/js-race)
* Charla en InfoQ: [https://www.infoq.com/presentations/javascript-concurrency-parallelism/](https://www.infoq.com/presentations/javascript-concurrency-parallelism/)
* Folders:

  ```
  ~/campus-virtual/2021/sytws2021/apuntes/tema2-async/event-loop/exercises/race-condition
  ~/local/src/uai/uai2015/race-condition/index.html
  ```
* [Abstract de la charla UAI2015](https://crguezl.github.io/_book/uai2015/)
* [Race Condition in JavaScript](https://youtu.be/wNwBzgDm0BI) YouTube Video

## Manually Interleaving Promises

This other example (using promises instead of callbacks) is taken from this blog:

* [Yes, there are race conditions in JavaScript](https://medium.com/@ubershmekel/yes-there-are-race-conditions-in-javascript-ba044571a914) by [Yuval Greenfield](https://medium.com/@ubershmekel)

Promises are a (relatively) new way to handle asynchronous programming in JS. For an introduction to Promises see this section:

* [Callbacks Problems]({{site.baseurl}}/tema2-async/promises#callbacks-problems) and Promise Introduction


**File race-example.js**

```js
{% include_relative race-example.js %}
```

An example of race condition in JavaScript.
When you run this script using Node or in a browser, it
does not print "Ended with 0", but a random number.

```
➜  race-condition git:(curso2021) ✗ node race-example.js 
Started with 0
Ended with 3
All done
➜  race-condition git:(curso2021) ✗ node race-example.js
Started with 0
Ended with 20
```

Even though the functions running
simply loop 100 iterations of adding and subtracting.

The reason the end result is random is because the
sleeps are of random duration and the time between the read
of the variable causes the eventual write to be incorrect
when `adder` and `subber` interleave.

This problem is similar to:

[Time-of-check to time-of-use](https://en.wikipedia.org/wiki/Time-of-check_to_time-of-use)

