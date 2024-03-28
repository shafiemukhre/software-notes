# Tips and tricks

## Use spread operator to add an element to an array 

```js
// wrong ❌
const [bars, setBars] = useState([true, false]);

const addProgressBar = () => {
    setBars(bars.push(false));
};
```

The `push` method modifies the original array and returns the new length of the array, not the array itself. This means that `setBars(bars.push(false))` is setting `bars` to a number (the new length of the array), not an array, which is why you're seeing the error when trying to call `.map()` on `bars`.

To fix this issue, you should use the spread operator (`...`) to create a new array that includes all the existing elements of `bars` plus the new element you want to add.

```js
// correct ✅
const [bars, setBars] = useState([true, false]);

const addProgressBar = () => {
    setBars([...bars, false]);
};
```

This approach aligns with React's requirement to treat the state as immutable and to use non-mutating methods when updating the state.

## Use standard DOM props

Besides common event handlers like `onClick` and others, there are many more common event handlers that you can consider using when building a feature such as `onBlur` and `onTransitionEnd` and more. You can refer to the [common props](https://react.dev/reference/react-dom/components/common#common-props) on React docs.

## Conditional inline styling

This is useful in React/UI interviews because you'd normally work with only JS and CSS.

**Conditional inline styling using css property**

```javascript
<div style={{backgroundColor: selected ? 'red':'green'}}></div>
```

**Conditional inline styling using classname**

```javascript
// in js
<div className={`section ${selected && 'section_selected'}`}></div>
```

```javascript
// in css
.section {
  display: flex;
  align-items: center;
} 
.section_selected{
  background-color: whitesmoke;
  border-width: 3px !important;
}
```