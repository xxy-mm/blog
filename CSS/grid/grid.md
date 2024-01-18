# CSS Grid

> references: [https://css-tricks.com/snippets/css/complete-guide-grid/](https://css-tricks.com/snippets/css/complete-guide-grid/)

## terminology

- grid container: Element with `display: grid`.
- grid item: Direct descendants (children) of the container.
- grid line: Dividing lines of the items.
- grid cell: The space between two adjacent row and two adjacent columns. A single `unit` of the grid.
- grid track: The space between two adjacent grid lines. (row/col)
- grid area: The total space surrounded by four grid lines.

> Question: What's the difference between `item` and `cell`?

## container properties

- display: grid/inline-grid
- grid-template-columns
- grid-template-rows

```css
/* the [first] represents the name of the line. The name of the first column line is identified as 'first' below. */
grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
```

- grid-template-areas

- column-gap
- row-gap
- gap: row-gap/column-gap

### alignment

- justify-items: start|end|center|stretch
- align-items: start|end|center|stretch
- place-items: align-items/justify-items

### content

- justify-content: start|end|center|stretch|space-around|space-between|space-evenly
- align-content: the same as justify-content
- place-content: align-content/justify-content

### auto

- grid-auto-columns
- grid-auto-rows
- grid-auto-flow: row | column | row dense | column dense;

## grid item properties

- grid-column
  - grid-column-start: `<number> | <name> | span <number> | span <name> | auto;`
  - grid-column-end: the same as above
- grid-row
  - grid-row-start: the same as above
  - grid-row-end: the same as above

```css
.item-a {
  grid-column-start: 2;
  grid-column-end: five;
  grid-row-start: row1-start;
  grid-row-end: 3;
}
```

- grid-area: `<name> | <row-start> / <column-start> / <row-end> / <column-end>`

```css
grid-area: 1 / col4-start / last-line / 6;
grid-area: header;
```

- place-self: auto| `<align-self> / <justify-self>`
  - justify-self: start | end | center | stretch
  - align-self: start | end | center | stretch

```css
.item {
  justify-self: end;
  align-self: center;
}
/* the above is equal to below */
.item {
  place-self: center end;
}
```

## sizing keywords

- min-content
- max-content
- auto
- fr

## sizing functions

- fit-content()
- minmax()
- min()
- max()
- repeat()
  - auto-fill: Fit as many possible columns as possible on a row, even if they are empty.
  - auto-fit: Fit whatever columns there are into the space. Prefer expanding columns to fill space rather than empty columns.

```css
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```
