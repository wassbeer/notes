# Code Styling JavaScript

_This document displays my personal picks from the rules of code styling as mentioned in the idiomatic.js github repository on "Principles of Writing Consistent, Idiomatic JavaScript"_

## 1. White space

Rules:
+ Never mix spaces and tabs
+ Set indent size to 2 (for readability)<details><summary>[?]</summary>
_In Sublime Text 3: Preferences --> Settings --> User --> Insert: '"tab_size" : 2'_</details>
+ Show invisibles/spaces (for consistency & end of of line white spacing issues)<details><summary>[?]</summary>
_In Sublime Text 3: Preferences --> Settings --> User --> Insert: '"draw_white_space": "all"'_</details>
+ Use Editorconfig when possible <details><summary>[?]</summary>
Editorconfig helps developers define and maintain consistent coding styles between different editors and IDEs. The .editorconfig files are created locally and stored in the root directory. For more information on Editorconfig please consult the [documentation](http://editorconfig.org/). 
</details>

My preferences.Sublime-settings | One of my .editorconfig files
:------------------------------:|:-----------------------------:
![](/images/preferences.JPG)    | ![](/images/editorconfig.JPG)

## 2. Beautiful Syntax

Rules:
+ Use white space for readability
+ "" vs. '': never mix quotes on the same project
+ Declare variables always in the beginning of their respective scope
+ Use the var/let/const keyword once per var/let/const or one var/let/const for each matching var/let/const
+ Named function declarations should be descriptive and verbose

Consistency always wins!

## 3. Conditional Evaluation

Keep It Simple, Stupid(KISS). Do not overdo the conditional evaluation.

``` JavaScript

// 4.1.1
// When only evaluating that an array has length,
// instead of this:
if ( array.length > 0 ) ...

// ...evaluate truthiness, like this:
if ( array.length ) ...


// 4.1.2
// When only evaluating that an array is empty,
// instead of this:
if ( array.length === 0 ) ...

// ...evaluate truthiness, like this:
if ( !array.length ) ...


// 4.1.3
// When only evaluating that a string is not empty,
// instead of this:
if ( string !== "" ) ...

// ...evaluate truthiness, like this:
if ( string ) ...


// 4.1.4
// When only evaluating that a string _is_ empty,
// instead of this:
if ( string === "" ) ...

// ...evaluate falsy-ness, like this:
if ( !string ) ...


// 4.1.5
// When only evaluating that a reference is true,
// instead of this:
if ( foo === true ) ...

// ...evaluate like you mean it, take advantage of built in capabilities:
if ( foo ) ...


// 4.1.6
// When evaluating that a reference is false,
// instead of this:
if ( foo === false ) ...

// ...use negation to coerce a true evaluation
if ( !foo ) ...

// ...Be careful, this will also match: 0, "", null, undefined, NaN
// If you _MUST_ test for a Boolean false, then use
if ( foo === false ) ...


// 4.1.7
// When only evaluating a ref that might be null or undefined, but NOT false, "" or 0,
// instead of this:
if ( foo === null || foo === undefined ) ...

// ...take advantage of == type coercion, like this:
if ( foo == null ) ...

// Remember, using == will match a `null` to BOTH `null` and `undefined`
// but not `false`, "" or 0
null == undefined

```

## 4. Inspiration

Cool ideas:
+ turn switch statement into an object with a function
+ return earlier to promote code readability