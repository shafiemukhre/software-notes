# Typescript for React

## Conventional props

```ts
function Heading({ title }: { title: string }) {
  return <h1>{title}</h1>;
}
⋮
function App() {
  return (
    <Heading title="Hello"></Heading>
  )
}

```

```ts
function HeadingWithContent({ children }: { children: string }) {
  return <h1>{children}</h1>;
}
⋮
function App() {
  return (
    <HeadingWithContent>Hello</HeadingWithContent>
  )
}
```

```ts
function HeadingWithContent({ children }: { children: ReactNode }): ReactElement | null {
  return <h1>{children}</h1>;
}
⋮
function App() {
  return (
    <HeadingWithContent>
      <strong>Hello!</strong>
    </HeadingWithContent>
  )
}
```

## Basic

```ts
// destructring props like this is more common
// the prop is an object with key of backgroundColor that has a type string
function Button({ backgroundColor }: { backgroundColor: string }) {
  return <button className="red-blue-500">click me</button>;
}

// the above is the same as

function Button(props: { backgroundColor: string; fontSize: number }) {
  const { backgroundColor } = props;

  return <button className="bg-blue-500">click me</button>;
}
```

```ts
// instead of this
function Button({
  backgroundColor,
  fontSize,
  pillShape,
}: {
  backgroundColor: string;
  fontSize: number;
  pillShape: boolean;
}) {
  return <button className="red-blue-500">click me</button>;
}

// extract it so that it will look much cleaner
type ButtonProps = {
  backgroundColor: string;
  fontSize: number;
  pillShape: boolean;
};

function Button({ backgroundColor, fontSize, pillShape }: ButtonProps) {
  return <button className="red-blue-500">click me</button>;
}
```

### Type for returned element

Specify the type of the returned element. [Tips] Hover on the functional component in your editor to see the inferred type of the returned element. For example:

```ts
function Button({
  backgroundColor,
  fontSize,
  pillShape,
}: ButtonProps): JSX.Element {
  return <button className="red-blue-500">click me</button>;
}
```

### Union

```ts
// extract the union so that you can use it for multiple types
type Color = "red" | "blue" | "green";

type ButtonProps = {
  backgroundColor: Color;
  textColor: Color;
  fontSize: number;
  pillShape?: boolean;
};

function Button({ backgroundColor, textColor fontSize, pillShape }: ButtonProps) {
  return <button className="red-blue-500">click me</button>;
}
```

### Array vs Tuple

```ts
type ButtonProps = {
  backgroundColor: "red" | "blue" | "green";
  fontSize: number;
  pillShape?: boolean;
  padding: number[]; // array of numbers
};

function Button({ backgroundColor, fontSize, pillShape }: ButtonProps) {
  return <button className="red-blue-500">click me</button>;
}

// it's better to use tuple instead because tuple's type and length is immutable

type ButtonProps = {
  backgroundColor: "red" | "blue" | "green";
  fontSize: number;
  pillShape?: boolean;
  padding: [number, number, number, number]; // tuple of numbers
};

function Button({
  backgroundColor,
  fontSize,
  pillShape,
  padding,
}: ButtonProps) {
  return <button className="red-blue-500">click me</button>;
}
```

### Object prop vs multiple props

Instead of this

```tsx
// Page.tsx
function Home() {
  return (
    <main>
      <Button backgroundColor="red" fontSize={30} padding={[5, 10, 20, 50]} />
    </main>
  );
}

// Button.tsx
type ButtonProps = {
  backgroundColor: "red" | "blue" | "green";

  fontSize: number;
  padding: [number, number, number, number]; // tuple of numbers
};

function Button({ backgroundColor, fontSize, padding }: ButtonProps) {
  return (
    <button
      style={{
        backgroundColor: backgroundColor,
        fontSize: fontSize,
        padding: `${padding[0]}px ${padding[1]}px ${padding[2]}px ${padding[3]}px`,
      }}
    >
      click me
    </button>
  );
}
```

do this

```tsx
// Page.tsx
function Home() {
  return (
    <main>
      <Button
        style={{
          backgroundColor: "blue",
          fontSize: 24,
          padding: [5, 10, 15, 20],
        }}
      />
    </main>
  );
}

// Button.tsx
type ButtonProps = {
  style: {
    backgroundColor: "red" | "blue" | "green";
    fontSize: number;
    padding: [number, number, number, number]; // tuple of numbers
  };
};

function Button({ style }: ButtonProps) {
  return <button style={style}>click me</button>;
}
```

### React.CSSProperties

Or even better in this case since it is a style, you can use `React.CSSProperties`

```tsx
// Page.tsx
function Home() {
  return (
    <main>
      <Button
        style={{
          backgroundColor: "blue",
          fontSize: 24,
          padding: "1rem, 2rem, 1rem, 3rem",
          borderRadius: 8,
          borderColor: "transparent",
        }}
      />
    </main>
  );
}

// Button.tsx
type ButtonProps = {
  style: React.CSSProperties;
};

function Button({ style }: ButtonProps) {
  return <button style={style}>click me</button>;
}
```

### Record

### Interface vs Type

## React Hooks with Typescript

to learn

## Tips

- use `ctrl` + `space` to activate intellissence so that you can know what are the props that the component is expecting
