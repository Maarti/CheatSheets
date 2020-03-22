# Typescript 

[Clean Code concepts adapted for TypeScript](https://github.com/labs42io/clean-code-typescript)
  
 
## [Set default objects with Object.assign or destructuring](https://github.com/labs42io/clean-code-typescript#set-default-objects-with-objectassign-or-destructuring)

```typescript
type MenuConfig = { title?: string, body?: string, buttonText?: string, cancellable?: boolean };

function createMenu(config: MenuConfig) {
  const menuConfig = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // ...
}

createMenu({ body: 'Bar' });
```

## [Use generator](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/function*)
```typescript
function* generator(i) {
  while(true){  
  yield i++;
  }
}
// Use next()...
const gen = generator(10);
console.log(gen.next().value);
console.log(gen.next().value);

// ... or "for ... of"
function print(n) {
  let i = 0;
  for (const g of generator(1)) {
    if (i++ === n) break;  
    console.log(g);
  }  
}
print(10);

```