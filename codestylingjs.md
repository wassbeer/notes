# Code Styling JavaScript

_This document displays my personal picks from the rules of code styling as mentioned in the idiomatic.js github repository on "Principles of Writing Consistent, Idiomatic JavaScript"_

## 1. White Space

Rules:
+ Never mix spaces and tabs
+ Set indent size to 2 (for readability)<details><summary></summary>
_In Sublime Text 3: Preferences --> Settings --> User --> Insert: '"tab_size" : 2'_</details>
``` JavaScript
// preferences.sublime-settings

{
	"color_scheme": "Packages/Babel/Monokai Phoenix.tmTheme",
	"draw_white_space": "all",
	"font_size": 11,
	"ignored_packages":
	[
		"Vintage"
	],
	"tab_size": 2
}
```
+ Show invisibles/spaces (for consistency & end of of line white spacing issues)<details><summary></summary>
_In Sublime Text 3: Preferences --> Settings --> User --> Insert: '"draw_white_space": "all"'_
``` JavaScript
// preferences.sublime-settings

{
	"color_scheme": "Packages/Babel/Monokai Phoenix.tmTheme",
	"draw_white_space": "all",
	"font_size": 11,
	"ignored_packages":
	[
		"Vintage"
	],
	"tab_size": 2
}
```
</details>

+ Use Editorconfig when possible <details><summary></summary>
Editorconfig helps developers define and maintain consistent coding styles between different editors and IDEs. The .editorconfig files are created locally and stored in the root directory. For more information on Editorconfig please consult the [documentation](http://editorconfig.org/). 

``` JavaScript 
// .editorconfig

root = true

[*]
indent_style = tab
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

</details>
```

## 2. Beautiful Syntax

Rules:
+ Use white space for readability <details>
``` JavaScript
if ( condition ) {
  // statements
}

while ( condition ) {
  // statements
}

for ( var i = 0; i < 100; i++ ) {
  // statements
}
```
</details>
+ Declare variables always in the beginning of their respective scope <details>
``` JavaScript
// Bad
function foo() {

  // some statements here

  var bar = "",
    qux;
}

// Good
function foo() {
  var bar = "",
    qux;

  // all statements after the variables declarations.
}
```
</details>
+ Use the var/let/const keyword once per var/let/const or one var/let/const for each matching var/let/const<details>
``` JavaScript
// Bad
var foo = "",
  bar = "";
var qux;

// Good
var foo = "";
var bar = "";
var qux;

// or..
var foo = "",
  bar = "",
  qux;
}
```
</details>
+ Named function declarations should be descriptive and verbose
+ "" vs. '': never mix quotes on the same project

__Consistency always wins!__

## 3. Conditional Evaluation

Keep It Simple, Stupid(__KISS__). Do not overdo the conditional evaluation.

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
+ turn switch statements into objects with functions<details>
``` JavaScript
// An example switch statement

switch( foo ) {
  case "alpha":
    alpha();
    break;
  case "beta":
    beta();
    break;
  default:
    // something to default to
    break;
}

// >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

// A alternate approach that supports composability and reusability is to
// use an object to store "cases" and a function to delegate:

var cases, delegator;

// Example returns for illustration only.
cases = {
  alpha: function() {
    // statements
    // a return
    return [ "Alpha", arguments.length ];
  },
  beta: function() {
    // statements
    // a return
    return [ "Beta", arguments.length ];
  },
  _default: function() {
    // statements
    // a return
    return [ "Default", arguments.length ];
  }
};

delegator = function() {
  var args, key, delegate;

  // Transform arguments list into an array
  args = [].slice.call( arguments );

  // shift the case key from the arguments
  key = args.shift();

  // Assign the default case handler
  delegate = cases._default;

  // Derive the method to delegate operation to
  if ( cases.hasOwnProperty( key ) ) {
    delegate = cases[ key ];
  }

  // The scope arg could be set to something specific,
  // in this case, |null| will suffice
  return delegate.apply( null, args );
};
```
</details>
+ return earlier to promote code readability<details>
``` JavaScript
// Bad:
function returnLate( foo ) {
  var ret;

  if ( foo ) {
    ret = "foo";
  } else {
    ret = "quux";
  }
  return ret;
}

// Good:

function returnEarly( foo ) {

  if ( foo ) {
    return "foo";
  }
  return "quux";
}
```
</details>