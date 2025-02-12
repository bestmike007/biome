---
title: noInvalidUseBeforeDeclaration (not released)
---

**Diagnostic Category: `lint/nursery/noInvalidUseBeforeDeclaration`**

:::danger
This rule hasn't been released yet.
:::

:::caution
This rule is part of the [nursery](/linter/rules/#nursery) group.
:::

Disallow the use of variables and function parameters before their declaration

JavaScript doesn't allow the use of block-scoped variables (`let`, `const`) and function parameters before their declaration.
A `ReferenceError` will be thrown with any attempt to access the variable or the parameter before its declaration.

The rule also reports the use of variables declared with `var` before their declarations.

## Examples

### Invalid

```jsx
function f() {
    console.log(x);
    const x;
}
```

<pre class="language-text"><code class="language-text">nursery/noInvalidUseBeforeDeclaration.js:3:11 parse ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">✖</span></strong> <span style="color: Tomato;">Const declarations must have an initialized value</span>
  
    <strong>1 │ </strong>function f() {
    <strong>2 │ </strong>    console.log(x);
<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">&gt;</span></strong> <strong>3 │ </strong>    const x;
   <strong>   │ </strong>          <strong><span style="color: Tomato;">^</span></strong>
    <strong>4 │ </strong>}
    <strong>5 │ </strong>
  
<strong><span style="color: lightgreen;">  </span></strong><strong><span style="color: lightgreen;">ℹ</span></strong> <span style="color: lightgreen;">this variable needs to be initialized</span>
  
</code></pre>

```jsx
function f() {
    console.log(x);
    var x = 0;
}
```

<pre class="language-text"><code class="language-text">nursery/noInvalidUseBeforeDeclaration.js:2:17 <a href="https://biomejs.dev/linter/rules/no-invalid-use-before-declaration">lint/nursery/noInvalidUseBeforeDeclaration</a> ━━━━━━━━━━━

<strong><span style="color: Orange;">  </span></strong><strong><span style="color: Orange;">⚠</span></strong> <span style="color: Orange;">This variable is used before its declaration.</span>
  
    <strong>1 │ </strong>function f() {
<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">&gt;</span></strong> <strong>2 │ </strong>    console.log(x);
   <strong>   │ </strong>                <strong><span style="color: Tomato;">^</span></strong>
    <strong>3 │ </strong>    var x = 0;
    <strong>4 │ </strong>}
  
<strong><span style="color: lightgreen;">  </span></strong><strong><span style="color: lightgreen;">ℹ</span></strong> <span style="color: lightgreen;">The variable is declared here:</span>
  
    <strong>1 │ </strong>function f() {
    <strong>2 │ </strong>    console.log(x);
<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">&gt;</span></strong> <strong>3 │ </strong>    var x = 0;
   <strong>   │ </strong>        <strong><span style="color: Tomato;">^</span></strong>
    <strong>4 │ </strong>}
    <strong>5 │ </strong>
  
</code></pre>

```jsx
function f(a = b, b = 0) {}
```

<pre class="language-text"><code class="language-text">nursery/noInvalidUseBeforeDeclaration.js:1:16 <a href="https://biomejs.dev/linter/rules/no-invalid-use-before-declaration">lint/nursery/noInvalidUseBeforeDeclaration</a> ━━━━━━━━━━━

<strong><span style="color: Orange;">  </span></strong><strong><span style="color: Orange;">⚠</span></strong> <span style="color: Orange;">This parameter is used before its declaration.</span>
  
<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">&gt;</span></strong> <strong>1 │ </strong>function f(a = b, b = 0) {}
   <strong>   │ </strong>               <strong><span style="color: Tomato;">^</span></strong>
    <strong>2 │ </strong>
  
<strong><span style="color: lightgreen;">  </span></strong><strong><span style="color: lightgreen;">ℹ</span></strong> <span style="color: lightgreen;">The parameter is declared here:</span>
  
<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">&gt;</span></strong> <strong>1 │ </strong>function f(a = b, b = 0) {}
   <strong>   │ </strong>                  <strong><span style="color: Tomato;">^</span></strong>
    <strong>2 │ </strong>
  
</code></pre>

## Valid

```jsx
f();
function f() {}

new C();
class C {}
```

```jsx
// An export can reference a variable before its declaration.
export { CONSTANT };
const CONSTANT = 0;
```

```jsx
function f() { return CONSTANT; }
const CONSTANT = 0;
```

## Related links

- [Disable a rule](/linter/#disable-a-lint-rule)
- [Rule options](/linter/#rule-options)
