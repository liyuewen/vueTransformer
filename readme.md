# VueTransformer

## Installation

## Usage

```ts
export default {
  // ...
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: [
          {
            loader: "ts-loader",
            options: {
              transpileOnly: true,
              getCustomTransformers: () => ({
                before: [
                  VueTsxTransformer({
                    // options
                  }),
                ],
              }),
            },
          },
        ],
      },
    ],
  },
};
```
## Syntax

### Content

- Automatic `h` injection syntactic sugar
- `vModel` syntactic sugar

```tsx
render() {
  return <p>hello</p>
}
```

with dynamic content:

```tsx
render() {
  return <p>hello { this.message }</p>
}
```

when self-closing:

```tsx
render() {
  return <input />
}
```

with a component:

```tsx
import MyComponent from "./my-component";

export default {
  render() {
    return <MyComponent>hello</MyComponent>;
  },
};
```

### Attributes/Props

```tsx
render() {
  return <input type="email" />
}
```

with a dynamic binding:

```tsx
render() {
  return <input
    type="email"
    placeholder={this.placeholderText}
  />
}
```

```tsx
// not supported > v1.2.4
render() {
  const inputAttrs = {
    type: 'email',
    placeholder: 'Enter your email'
  }
  return <input {...{ attrs: inputAttrs }} />
}
```



```tsx

### Slots

named slots:

```tsx
render() {
  return (
    <MyComponent>
      <header slot="header">header</header>
      <footer slot="footer">footer</footer>
    </MyComponent>
  )
}
```

scoped slots:

```tsx
render() {
  const scopedSlots = {
    header: () => <header>header</header>,
    footer: () => <footer>footer</footer>
  }

  return <MyComponent scopedSlots={scopedSlots} />
}
```

### Directives

```tsx
<input vModel={this.newTodoText} />
```

with a modifier: Not Supported, Follow the type validation of TSX

v-html:

```tsx
<p domPropsInnerHTML={html} />
```
