# patternmatch.js
A pattern matching library in native javascript. This library is inspired from F# and other macro pattern matching libraries with functional programming in mind.  Particularly, I wanted to take advantage of new ES6 language structures to really create precise pattern matching expressions.

# What is pattern matching?

Pattern matching is an idea from function programming to transform data using a very strict form of expression. Some languages are even pretty cool about telling you if you missed a certain case.  Sure, you could write a bunch of if statements, but programming is also part about communication. I wanted a very simple way to communicate what's going on.  Pattern matching tries to keep your code looking algebriac and less about state and variable comparison. I try to use various symbols in order to express what's going on.

#installing
```
npm install patternmatch
```
OR
```
<script src="https://npmcdn.com/patternmatch@latest/patternmatch.js"></script>
```

# Patterns

Let's look at some cool stuff we can pattern match!

##Literals
```javascript
var {pattern,match} = require("patternmatch");
//Gather pattern matching symbols
var [_$_,__,ALL,ARRAY] = [pattern.var,pattern.any,pattern.all,pattern.array];

var p = match(
  pattern(null),        ()=>"found null",
  pattern(undefined),   ()=>"found undefined",
  pattern(42),          ()=>"life",
  pattern("foo"),       ()=>"bar",
  pattern("ha","ha"),   ()=>"laugh",
  pattern(ALL),         ()=>"everything else"
);

p(null)           //"found null"
p(undefined)      //"found undefined"
p(42)             //"life"
p("foo")          //"bar"
p("ha","ha")      //"laugh"
p("jabberwocky")  //"everything else"
```

##Placeholders

Place holders let you ignore certain arguments

```javascript
var p = match(
  pattern("beginning",__,"end"), ()=>"match"
);

p("beginning","my story","end")           //"match"
p("beginning","their story story","end")  //"match"
```
##Variables

Extract variables out of a pattern

```javascript
var p = match(
  pattern("hello",_$_), (name)=>"goodbye "+name,
  pattern(1,__,_$_),    (x)=>x
);

p("hello","richard")  //"goodbye richard"
p(1,2,3)              //3
```
