# INDEC Functional Programming Guide() {

*A mostly reasonable approach to functional programing using lodash*

## Table of Contents

1. [Map](#map)
1. [Some & Every](#some-every)
1. [Sorting & Filtering](#sorting-filtering)
1. [Immutability](#immutability)
1. [Functional IF](#functional-if)
1. [Functional FOR](#functional-for)

## Map

<a name="map--usage"></a><a name="1.1"></a>
- [1.1](#map--usage) **Map Usage**: Map should only be used when a transformation of the data is intended.

```js
// bad
map(users, (user, index) => {
    user.order = index + 1;
});
```

```js
// good
forEach(users, (user, index) => {
    user.order = index + 1;
});
```

**[⬆ back to top](#table-of-contents)**

## Some & Every

<a name="some-every"></a><a name="2.1"></a>
- [2.1](#some-every) **Some and Every Usage**:  Functions `some` and `every` can be used without `predicate` if the list is composed by booleans.

```js
const arr = [true, false, true];

// bad
every(arr, e => e);

// good
every(arr);

// good predicate usage
some(users, user => user.disabled)
```

## Sorting & Filtering

<a name="sorting-filtering"></a><a name="3.1"></a>
- [3.1](#sorting-filtering) **Filtering**: Do not use `Array#splice` instead `filter` o `reject` should be used.

 > Why? Splice mutates the original array.

```js
// bad
let arr1 = ['a', 'b', 'c', 'd', 'e'];
const result = array.splice(0, 2);
// array mutates into ['c', 'd', 'e']
// result = ['a', 'b']

const arr1 = ['a', 'b', 'c', 'd', 'e'];
// good
const result = arr1.filter(a => a !== 'e');

// result = ['a', 'b', 'c', 'd']
```

<a name="sorting--lodash"></a><a name="3.2"></a>
- [3.2](#sorting--lodash) **Sorting**: Use a better way to sort arrays with correct lodash libraries.

```js
// bad
map(
    uniqBy(
        sortBy(
            dwellings,
            dwelling => dwelling.area
        ),
        dwelling => dwelling.area
    ),
    dwelling => dwelling.area
);
```

```js
// good
sortedUniqBy(sortBy(map(
    dwellings,
    dwelling => dwelling.area
)));
```

**[⬆ back to top](#table-of-contents)**

## Immutability

<a name="immutability--methods"></a><a name="3.2"></a>
- [4.1](#immutability--methods) **Immutable Methods**: Methods that does not mutate the arguments are prefered.

```js
// bad
_.pull(arr, value)
// bad
const a = _.remove(arr, fn);
```

```js
// good
const a = _.without(arr, value)
// good
const a = _.filter(arr, fn);
```

**[⬆ back to top](#table-of-contents)**

## Functional IF

<a name="functional-if"></a><a name="5.1"></a>
- [5.1](#functional-if) **Functional `if`**: Functional replacement for `IF` statement.

```js
// imperative
function formatUserName(user) {
    if (user.disabled) {
        return user.name + ' [disabled]';
    } else {
        return user.name;
    }
};
```

```js
// functional
const formatUserName = user => user.disabled ? user.name + ' [disabled]' : user.name;
```

**[⬆ back to top](#table-of-contents)**

## Functional FOR

<a name="functional-for"></a><a name="6.1"></a>
- [6.1](#functional-for) **Functional `for`**: Functional replacement for `FOR` statement

```js
const users = [
    { name: 'John', age: 84 },
    { name: 'Mark', age: 34 },
    { name: 'Michael', age: 4 },
    { name: 'James', age: 6 }
]
```

```js
// imperative
var underAge = [];
for (var i = 0; i < users.length; i++) {
    if (users[i].age < 18) {
        underAge.push(users[i].name)
    }
}
```

```js
// functional
const isUnderAge = user => user.age < 7;
const getName = user => user.name;
const getUnderAge = users.filter(isUnderAge).map(getName);
const underAge = getUnderAge(users);
```

**[⬆ back to top](#table-of-contents)**

# }
