![Alexandrovich Stroganoff](http://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/A_Portrait_of_Count_Paul_Alexandrovich_Stroganoff%2C_Aged_15_by_Jean_Voille.jpg/500px-A_Portrait_of_Count_Paul_Alexandrovich_Stroganoff%2C_Aged_15_by_Jean_Voille.jpg "totally random picture of Alexandrovich Stroganoff, age 15")

This is a simple, extremely lightweight, zero-dependency simple event/pubsub system for node or the browser.

It gives your objects these really basic functions:

- `emit` - publish an event
- `on` - subscribe to an event
- `off` - unsubscribe an event

It's pronounced like ["stroganoff"](http://dictionary.cambridge.org/us/pronunciation/british/stroganoff), but "emit" instead of "stroge".

## usage

```javascript
var kitty = {
    purr: function(){
        this.emit('purr');
    },
    
    eat: function(food){
        this.emit('ate', food);
    } 
};

emitonoff(kitty);

function showAte(food){
    console.log('The kitty was hungry, so it ate', food);
}

function showPurred(){
    console.log('the kitty purred.')
}

kitty.on('ate', showAte);
kitty.on('purr', showPurred);

kitty.eat('kibble');
kitty.eat('mouse');
kitty.off('ate', showAte);
kitty.eat('tail');
kitty.purr();
```

You can also use it without an object, like this:

```javascript
var kitty = emitonoff();

function showAte(food){
    console.log('The kitty was hungry, so it ate', food);
}

function showPurred(){
    console.log('the kitty purred.')
}

kitty.on('ate', showAte);
kitty.on('purr', showPurred);

kitty.emit('ate', 'kibbles');
kitty.emit('ate', 'bits');
kitty.emit('purr');
```

## install

### nodejs/browserify

```
npm install --save emitonoff
```

then, in your code:

```javascript
var emitonoff = require('emitonoff');
```

### requirejs

Put it in your require path, then you can do this:

```javascript
define(['emitonoff'], function(emitonoff){
    // do stuff
});
```

### plain browser global

```html
<script src="https://rawgit.com/konsumer/emitonoff/master/dist/emitonoff.min.js"></script>
```

## browser support

I haven't done too much browser-testing, but it should work on any browser that can `Array.slice` (all of them in the last 15 years.) If you need it to work on a browser, file a bug and I will add support (or tell you t find a `Array.slice` polyfill.)

It works in IE5.5.