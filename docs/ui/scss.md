# SCSS

- use BEM for naming convention, for example: `.block-name__element-name--blue-modifier`

## SCSS modules in react

### How to have make nested scss work in jsx/tsx

```scss
.test {
  // name of module
  color: pink;
  [class~="test2"] {
    // target child class
    color: blue;
  }
}
```

```html
<div className="{styles.test}">
  <div className="test2"></div>
</div>
```
