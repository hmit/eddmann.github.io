---
layout: post
title: "Maybe in JavaScript"
meta: "Exploration of the Maybe type in JavaScript"
---

Recently I have been delving into the concepts of [Functors](http://learnyouahaskell.com/functors-applicative-functors-and-monoids) and [Monads](http://learnyouahaskell.com/a-fistful-of-monads).
There are many good [resources](https://curiosity-driven.org/monads-in-javascript) available online that will do a far better job of explaining these concepts than me, however, I do wish to document an example Maybe type I have implemented in JavaScript.
Again, there are many good external [resources](http://sean.voisen.org/blog/2013/10/intro-monads-maybe/) which highlight the characteristics and power of using such a type, so I will direct your attention to those if you wish to learn more.
<!--more-->

### Implementation

The Maybe type encapsulates the concept of Some (contains a value) and None (no value present).
With these two abstractions we are able to safety handle the event of no value being present, without NullPointerException's being thrown and null checks.

{% highlight js %}
const Maybe = (function () {
  const Some = function (x) { this.x = x; };
  Some.prototype.fmap = function (fn) { return Maybe.of(fn(this.x)); };
  Some.prototype.bind = function (fn) { return fn(this.x); };
  Some.prototype.toString = function () { return `Some(${this.x})`; };

  const None = function () {};
  None.fmap = () => None;
  None.bind = () => None;
  None.toString = () => 'None';

  return {
    of: (x) => x === null || x === undefined ? None : new Some(x),
    lift: (fn) => (...args) => Maybe.of(fn(...args)),
    Some,
    None
  };
})();
{% endhighlight %}

The implementation above uses two small prototypical class definitions to define Some and None.
We then return the ability to take a value of a plain type and put it into a Maybe container, along with the capability to lift a function into the Maybe space.

### Division by Zero Example

The first example of using the Maybe type I will demonstrate is in the case of handling division by zero errors.
In the event that the denominator is zero instead of throwing an exception or returning null (as shown in the basic `div` implementation) we will instead lift the function into the Maybe type and return a Some or None.
This may not seem like much of a win at this time but when we later look at examples of composing these expressions together you will be shown its full power.

{% highlight js %}
const div = (a, b) => b === 0 ? null : a / b;
const mdiv = Maybe.lift(div);

div(10, 0); // null
mdiv(100, 0); // None
mdiv(10, 2); // Some(5)
{% endhighlight %}

### Property Retrieval Example

Another case were `undefined` values may appear in JavaScript is whilst retrieving properties from objects that may(not) be present.
Again, we are able to highlight how the basic `get` function returns the object property or undefined if not present, were as lifting it into the Maybe type provides us with the Some and None abstractions.

{% highlight js %}
const get = curry((prop, obj) => obj[prop]);
const mget = (prop) => Maybe.lift(get(prop));

const user = {
  name: 'Joe Bloggs',
  age: 25,
  address: {
    street: 'Cinder Drive'
  }
};

get('agez')(user); // undefined
mget('agez')(user); // None
mget('age')(user); // Some(25)
{% endhighlight %}

We are then able to compose multiple `mget` functions together, handling application on the Maybe containers using `fmap` and `bind`.

{% highlight js %}
const fmap = curry((fn, functor) => functor.fmap(fn));
const bind = curry((fn, monad) => monad.bind(fn));
{% endhighlight %}

You will notice that `fmap` double wraps the resulting value, this is due to as being a Functor definition its' action is to wrap the resulting value (from our provided function) back into the given container.
However, in the case of the `bind` Monad definition, it instead does not wrap the value back into the container upon completion, but instead relies on the function itself to return the correctly typed value.

{% highlight js %}
const getStreet = compose(fmap(mget('street')), mget('address'));
getStreet({ address: {} }); // Some(None)
getStreet(user); // Some(Some(Cinder Drive))

const getStreet = compose(bind(mget('street')), mget('address'));
getStreet({ address: {} }); // None
getStreet(user); // Some(Cinder Drive)
{% endhighlight %}

### Mimicking Do Notation in JavaScript

You will notice when looking through Haskell examples how succinct the do notation is at handling the containers used.
We are able to take advantage of the ability to phase JavaScript functions as strings to rewrite a language similar to this notation into one that can be executed.
This allows us to clearly express the intent of the code as opposed to muddling it with the plumbing required to make it work with the containers.

{% highlight js %}
const doM = (function() {
  const tokenize = (exp) => exp
    .toString()
    .split(/[\n;]/)
    .slice(1, -1)
    .map((s) => s.trim())
    .filter(Boolean);

  const evaluate = (tokens) => {
    if (tokens.length === 0) return '';

    let token = tokens.shift(), match;
    if (match = token.match(/^return (.+)$/))
      return `return Maybe.of(${match[1]});` + evaluate(tokens);
    if (match = token.match(/^(.+) <= (.+)$/))
      return `return ${match[2]}.bind(function(${match[1]}) { ${evaluate(tokens)} });`;

    return evaluate(tokens);
  };

  return compose(x => x(), Function, evaluate, tokenize);
})();

doM(() => {
  address <= mget('address')(user)
  street <= mget('street')(address)
  return street
}); // Some(Cinder Drive)
{% endhighlight %}
