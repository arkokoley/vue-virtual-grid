# Vue Virtual Grid

_Virtual Scrolling Grid made for VueJS based on CSS grids._

[NPM Package](https://www.npmjs.com/package/vue-virtual-grid) | [Demo Website](https://vue-virtual-grid.netlify.app/)

---

-   Render any Vue Component (images, iframes, content) of a known width/height inside.
-   Variable height items in the same row.
-   Variable width items (based on columns).
-   Rendering is done with virtual scrolling (aka windowing).
-   Supports infinite scroll!

---

## Install

```bash
npm install --save vue-virtual-grid
```

### Usage

Import VirtualGrid from the package:

```ts
import VirtualGrid from 'vue-virtual-grid';
```

Register it as on of your components:

```js
components: {
    VirtualGrid,
},
```

In your template you can add:

```html
<VirtualGrid :updateFunction="yourGetDataFunction" />
```

The `VirtualGrid` takes multiple custom function as properties

-   **updateFunction**:
    A function that will populate the grid, constructor is the following `updateFunction(params: { offset: number }) => VirtualGrid.Item[]`.
    The offset will be incremented (+1) each time the function is called.
-   **getGridGap**:
    A function that will define the gap between elements of the grid, constructor is the following `getGridGap(elementWidth: number, windowHeight: number) => number`.
-   **getColumnCount**:
    A function that set the width of columns in the grid, constructor is the following `getColumnCount(elementWidth: number) => number;`.
-   **getWindowMargin**:
    A function that set the margin size used for windowing (virtualization), constructor is the following `getWindowMargin(windowHeight: number) => number;`.
-   **getWindowMargin**:
    A function that provides a way to compute ratio height/width depending on the display (by default it preserves ratio), constructor is the following `getItemRatioHeight(height: number, width: number, columnWidth: number) => number;`.

Properties are provided with default functions that you can use or get inspired from in `src/utils.ts`.

The function `updateFunction` should return a list of items that will be rendered, each item should look like this object:

```js
{
    id: string, // binding id (must be unique)
    injected?: string, // custom param, pass an object with what you want inside (optional)
    width: number, // original width of the item
    height: number, // original height of the item
    columnSpan: number, // how many columns will use your item (put 0 if you want the full width)
    newRow?: boolean, // if the item should appear on the next row (optional)
    renderComponent: Component // A VueJS component (custom template of your choice) to render the item (passed as prop `item`)
}
```

The property `injected` does not impact the computation, it is here to pass custom data to the final component.

In the returned object to your `renderComponent` the height and width properties will be recomputed depending on the column size. It will always keep the original ratio.

### Typescript support

If you're using Typescript you can import typing for `Item` and provide custom typing for injected data:

```ts
import { Item } from 'vue-virtual-grid';

interface Image {
    alt: string;
    url: string;
}

const item: Item<Image>;
```

### Live example

If you want a live example, you can take a look at the demo (link at the top) and check the corresponding code in `example/`.

## Contribute

Anyone is welcome to contribute (this project is not perfect obviously).

### Install current dependencies

```bash
npm ci
```

### Build and try the example

```bash
npm run serve:example
```

### Compiles lib for production

```bash
npm run build
```

### Lints and fixes files

```bash
npm run lint
```

## Inspiration

This is based on React work here: https://github.com/jamiebuilds/react-gridlist

**Kudos to Jamie!**

## Maintainer

| [![twitter/mikescops](https://avatars0.githubusercontent.com/u/4266283?s=100&v=4)](https://pixelswap.fr 'Personal Website') |
| --------------------------------------------------------------------------------------------------------------------------- |
| [Corentin Mors](https://pixelswap.fr/)                                                                                      |
