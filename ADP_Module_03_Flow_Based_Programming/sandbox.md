

{[{}]}

[{"name":"Alice","age":25},
 {"name":"Sophie","age":30},
 {"name":"Julie","age":19}]

 [{"name":"Alice","age":25},  {"name":"Sophie","age":30},  {"name":"Julie","age":19}]

 ["Alice", "Sophie", "Julie"]


 ## Have a look on that:

 In JavaScript, the operator you're seeing is actually `||` (two vertical bars), called the **logical OR operator**.

In your code:

```javascript
msg.payload = {
    type: msg.payload.type || "ALARM",
    source: msg.payload.source || msg.topic || "System",
    message: msg.payload.message || msg.payload.toString()
};
```

it is used to provide **default values** when the value on the left is "falsy".

Falsy values in JavaScript are:

```javascript
false
0
""
null
undefined
NaN
```

### Example 1

```javascript
msg.payload.type = "WARNING";

type = msg.payload.type || "ALARM";
```

Result:

```javascript
type = "WARNING";
```

because `"WARNING"` is truthy.

---

### Example 2

```javascript
msg.payload.type = undefined;

type = msg.payload.type || "ALARM";
```

Result:

```javascript
type = "ALARM";
```

because `undefined` is falsy.

---

### Chained ORs

This line:

```javascript
source: msg.payload.source || msg.topic || "System",
```

means:

1. Use `msg.payload.source` if it exists and is truthy.
2. Otherwise use `msg.topic`.
3. Otherwise use `"System"`.

Equivalent code:

```javascript
let source;

if (msg.payload.source) {
    source = msg.payload.source;
} else if (msg.topic) {
    source = msg.topic;
} else {
    source = "System";
}
```

---

### Modern alternative: `??`

Be careful: `||` treats **0**, **false**, and **""** as missing values.

Sometimes you only want to replace **null** or **undefined**. In that case use the **nullish coalescing operator** `??`:

```javascript
const value = msg.payload.count ?? 10;
```

Examples:

```javascript
0 ?? 10      // 0
false ?? 10  // false
"" ?? 10     // ""
null ?? 10   // 10
undefined ?? 10 // 10
```

For Node-RED flows, `||` is very common for setting defaults, but `??` is often safer when `0`, `false`, or an empty string are valid values.
