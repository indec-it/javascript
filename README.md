# INDEC JavaScript Style Guide() {

*A mostly reasonable approach to JavaScript*

> **Note**: this guide is base on airbnb guide [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/blob/master/README.md),
it reinforces the most important rules and overwrites some of them.

## Table of Contents

  1. [Functions](#functions)
  1. [Blocks](#blocks)
  1. [WhiteSpace](#whitespace)
  1. [ES7](#es7)

## Functions
 <a name="methods--naming"></a><a name="1.1"></a>
  - [1.1](#functions) **Method Naming**: Methods should be named with a verb in infinitive.

```js
// bad
function validating() {
    //...
};

// good
function validate() {
    // ...
};
```

## Blocks
  <a name="blocks--braces"></a><a name="2.1"></a>
  - [2.1](#blocks--braces) Use braces with all single-line blocks.

```js
// bad
if (test) return false;

// good
if (test) {
    return false;
}
```
**[⬆ back to top](#table-of-contents)**

## Whitespace

  <a name="whitespace--spaces"></a><a name="3.1"></a>
  - [3.1](#whitespace--spaces) Use soft tabs (space character) set to 4 spaces.

```js
// bad
function foo() {
∙let name;
}

// bad
function bar() {
∙∙let name;
}

// good
function baz() {
∙∙∙∙let name;
}
```
**[⬆ back to top](#table-of-contents)**

## ES7
   <a name="ES7--Async/Await"></a><a name="4.1"></a>
   - [4.1](#Async/Await) **Async/Await**: use `async/await` instead of `then` (promises)

```js
// bad
const fetchUser = url => getAuthHeader().then(
    authorization => fetch(url, { headers: {authorization} })
).then(
    response => response.json
).then(
    data => new User(data.user)
)catch(
    err => console.log(err);
);

// good
const fetchUser = async url => {
    try {
        const response = await fetch(url, {
            credentials: 'same-origin',
            headers: {
                authorization: await getAuthHeader()
            }
        });
        const data = await response.json();
        return new User(data.user);
    } catch (err) {
        console.log(err);
        throw err;
    }
}
```
**[⬆ back to top](#table-of-contents)**

# }
