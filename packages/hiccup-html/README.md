<!-- This file is generated - DO NOT EDIT! -->

# ![hiccup-html](https://media.thi.ng/umbrella/banners/thing-hiccup-html.svg?cec1e8d8)

[![npm version](https://img.shields.io/npm/v/@thi.ng/hiccup-html.svg)](https://www.npmjs.com/package/@thi.ng/hiccup-html)
![npm downloads](https://img.shields.io/npm/dm/@thi.ng/hiccup-html.svg)
[![Twitter Follow](https://img.shields.io/twitter/follow/thing_umbrella.svg?style=flat-square&label=twitter)](https://twitter.com/thing_umbrella)

This project is part of the
[@thi.ng/umbrella](https://github.com/thi-ng/umbrella/) monorepo.

- [About](#about)
  - [Supported elements](#supported-elements)
    - [Head / metadata](#head---metadata)
    - [Sections](#sections)
    - [Text content](#text-content)
    - [Lists](#lists)
    - [Inline](#inline)
    - [Forms / inputs](#forms---inputs)
    - [Media](#media)
  - [Compatibility](#compatibility)
  - [Status](#status)
  - [Related packages](#related-packages)
- [Installation](#installation)
- [Dependencies](#dependencies)
- [API](#api)
  - [defElement](#defelement)
    - [Element creation](#element-creation)
- [Authors](#authors)
- [License](#license)

## About

Type-checked HTML5 element functions for [@thi.ng/hiccup](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup) related infrastructure.

The following type-checked factory functions are provided **so far** and
in many cases include specialized type definitions for element-specific
attributes. See [`defElement()`](#defelement) below for more details.

### Supported elements

#### Head / metadata

[Source](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/head.ts)

`base`, `head`, `link`, `meta`, `style`, `title`

#### Sections

[Source](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/sections.ts)

`address`, `article`, `aside`, `body`, `footer`, `header`, `hgroup`,
`main`, `nav`, `section`

#### Text content

[Source](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/blocks.ts)

`blockquote`, `div`, `figure`, `figcaption`, `hr`, `para`, `pre`, `span`

#### Lists

[Source](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/lists.ts)

`datalist`, `dd`, `dl`, `dt`, `li`, `ol`, `ul`

#### Inline

[Source](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/inline.ts)

`abbr`, `anchor`, `br`, `cite`, `code`, `data`, `del`, `em`, `i`, `ins`,
`kbd`, `mark`, `quote`, `small`, `span`, `strong`, `sub`, `sup`, `time`

#### Forms / inputs

[Source](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/forms.ts)

`button`, `checkbox`, `fieldset`, `form`, `inputColor`, `inputFile`,
`inputNumber`, `inputPass`, `inputRange`, `inputSearch`, `inputText`,
`label`, `legend`, `meter`, `option`, `optGroup`, `progress`, `radio`,
`select`

#### Media

[Source](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/media.ts)

`img`, `picture`, `source`

### Compatibility

The hiccup syntax is (by design) merely a convention and specific
feature support and interpretation is down to the actual tooling used.

The type definitions for element attributes used by this package allow
certain constructs which are only supported by some hiccup consumers
(however, there're compatible alternative ways of expressing the same
data).

The table below provides an overview of the _current_ syntax feature
support by the relevant packages consuming hiccup:

- [@thi.ng/hiccup](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup)
- [@thi.ng/hdom](https://github.com/thi-ng/umbrella/tree/develop/packages/hdom)
- [@thi.ng/hdom2020](https://github.com/thi-ng/umbrella/tree/feature/hdom2020/packages/hdom2020)

| Feature                    | Example and HTML equivalent/result                   | hiccup | hdom | hdom2020 |
|----------------------------|------------------------------------------------------|--------|------|----------|
| Emmet style tags           | `["div#id.foo", {}]`                                 | ✅      | ✅    | ✅        |
|                            | `<div id="id" class="foo">`                          |        |      |          |
| `class` attrib as object   | `["a.bar.baz", { class: { foo: true, bar: false }}]` | ❌      | ❌    | ✅        |
|                            | `<a class="baz foo">`                                |        |      |          |
| `style` attrib as object   | `["div", { style: { color: "red" }}]`                | ✅      | ✅    | ✅        |
|                            | `<div style="color:red;">`                           |        |      |          |
| Attrib array values        | `["img", { srcset: ["1.jpg", "2.jpg"] }]`            | ✅      | ❌    | ✅        |
|                            | `<img srcset="1.jpg, 2.jpg">`                        |        |      |          |
| Data attribs as object     | `["a", { data: { foo: 42 }}]`                        | ❌      | ❌    | ✅        |
|                            | `<a data-foo="42">`                                  |        |      |          |
| Function attrib values (1) | `["a", { id: () => "epoch-" + Date.now() }]`         | ✅      | ✅    | ✅        |
|                            | `<a id="epoch-1593024083666">`                       |        |      |          |
| `IDeref` attrib values (2) | `["div", { id: { deref() { return "foo"; }}}]`       | ❌      | ❌    | ✅        |
|                            | `<div id="foo">`                                     |        |      |          |

All other features not explicitly mentioned are supported by all three
packages.

(1) Excluding event listener attribs, these are always function values
of course, but will NOT be evaluated to obtain final attrib value

(2) The
[`IDeref`](https://github.com/thi-ng/umbrella/tree/develop/packages/api/src/api/deref.ts)
interface is implemented by various data structures in the
thi.ng/umbrella eco system (most relevant:
[@thi.ng/rstream](https://github.com/thi-ng/umbrella/tree/develop/packages/rstream),
[@thi.ng/atom](https://github.com/thi-ng/umbrella/tree/develop/packages/atom)).

### Status

**ALPHA** - bleeding edge / work-in-progress

The current aim is not necessarily to have wrappers for *each* possible
HTML5 element, but certainly to support the most commonly used ones. PRs
welcome!

### Related packages

- [@thi.ng/hdom](https://github.com/thi-ng/umbrella/tree/develop/packages/hdom) - Lightweight vanilla ES6 UI component trees with customizable branch-local behaviors
- [@thi.ng/hiccup-svg](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-svg) - SVG element functions for [@thi.ng/hiccup](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup) & [@thi.ng/hdom](https://github.com/thi-ng/umbrella/tree/develop/packages/hdom)

## Installation

```bash
yarn add @thi.ng/hiccup-html
```

```html
// ES module
<script type="module" src="https://unpkg.com/@thi.ng/hiccup-html?module" crossorigin></script>

// UMD
<script src="https://unpkg.com/@thi.ng/hiccup-html/lib/index.umd.js" crossorigin></script>
```

Package sizes (gzipped, pre-treeshake): ESM: 943 bytes / CJS: 1.23 KB / UMD: 1.19 KB

## Dependencies

- [@thi.ng/api](https://github.com/thi-ng/umbrella/tree/develop/packages/api)

## API

[Generated API docs](https://docs.thi.ng/umbrella/hiccup-html/)

```ts
import { $compile } from "@thi.ng/hdom2020";
import { div, label, option, select } from "@thi.ng/hiccup-html";

const choices = [
    ["#f00", "Red"],
    ["#ff0", "Yellow"],
    ["#0f0", "Green"],
    ["#0ff", "Cyan"],
    ["#00f", "Blue"],
    ["#f0f", "Magenta"],
];

$compile(
    div(
        null,
        label({ for: "colors" }, "Fave color: "),
        select(
            {
                id: "colors",
                onchange: (e) => alert((<HTMLSelectElement>e.target).value),
            },
            option(null, "Please choose..."),
            ...choices.map((x) => option({ value: x[0] }, x[1]))
        )
    )
).mount(document.body);
```

### defElement

All element functions are created via the higher-order function
`defElement` which produces the typed, variadic factories. `defElement`
takes an element name and optional set of default attributes. It also
uses generics to enforce types for the element's attributes (default:
[`Attribs`](https://github.com/thi-ng/umbrella/blob/develop/packages/hiccup-html/src/api.ts#L119)
and/or children/body (default: `any`).

Define element with defaults:

```ts
import { defElement } from "@thi.ng/hiccup-html";

const el = defElement("tag")
```

Define with custom attribs & no children allowed:

```ts
import { Attribs, AttribVal, defElement } from "@thi.ng/hiccup-html";

// extend global HTML default attribs
interface MyAttribs extends Attribs {
    class: AttribVal<string>;
    width: AttribVal<number>;
    height: AttribVal<number>;
}

// provide type constraints and default attribs
const el = defElement<Partial<MyAttribs>, never>(
    "tag",
    { width: 100, height: 100 }
);
```

The `Attribs` interface provides a common, fully typed base definition
of HTML attributes (incl. event listeners) and can be found in
[api.ts](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup-html/src/api.ts#L119).

The `AttribVal` type wrapper is used to allow for reactive attribute
values (in
[@thi.ng/hdom2020](https://github.com/thi-ng/umbrella/tree/feature/hdom2020/packages/hdom2020))
and [`IDeref`
instances](https://github.com/thi-ng/umbrella/tree/develop/packages/api/src/api/deref.ts)
when later providing attribute values to an element.

#### Element creation

The function returned by `defElement` has the following signatures:

```ts
(attribs?: Nullable<T>, ...body: B[]) => [string, Nullable<T>, ...B[]];

(emmet: string, attribs?: Nullable<T>, ...body: B[]) => [string, Nullable<T>, ...B[]];
```

The result of either form is a simple tuple, defining an HTML element in
[@thi.ng/hiccup](https://github.com/thi-ng/umbrella/tree/develop/packages/hiccup)
syntax.

If the second call signature is used, the initial `emmet`-style string
will be appended to the tag name and merely acts as syntax sugar for
providing an element ID and/or CSS classes.

```ts
const el = defElement<any>("a");
```

| Call                              | Result                           |
|-----------------------------------|----------------------------------|
| `el()`                            | `["a", null]`                    |
| `el(null)`                        | `["a", null]`                    |
| `el(null, "body")`                | `["a", null, "body"]`            |
| `el({ c: 2 })`                    | `["a", { c: 2 }]`                |
| `el({ c: 2 }, "body")`            | `["a", { c: 2 }, "body"]`        |
| `el("#id.foo")`                   | `["a#id.foo", null]`             |
| `el("#id.foo", { c: 2 })`         | `["a#id.foo", { c: 2 }]`         |
| `el("#id.foo", { c: 2 }, "body")` | `["a#id.foo", { c: 2 }, "body"]` |
| `el("#id.foo", null, "body")`     | `["a#id.foo", null, "body"]`     |

```ts
// with default attribs
const el = defElement<any>("a", { b: 1 });
```

| Call                              | Result                                 |
|-----------------------------------|----------------------------------------|
| `el()`                            | `["a", { b: 1 }]`                      |
| `el(null)`                        | `["a", { b: 1 }]`                      |
| `el(null, "body")`                | `["a", { b: 1 }, "body"]`              |
| `el({ c: 2 })`                    | `["a", { b: 1, c: 2 }]`                |
| `el({ c: 2 }, "body")`            | `["a", { b: 1, c: 2 }, "body"]`        |
| `el("#id.foo")`                   | `["a#id.foo", { b: 1 }]`               |
| `el("#id.foo", { c: 2 })`         | `["a#id.foo", { b: 1, c: 2 }]`         |
| `el("#id.foo", { c: 2 }, "body")` | `["a#id.foo", { b: 1, c: 2 }, "body"]` |
| `el("#id.foo", null, "body")`     | `["a#id.foo", { b: 1 }, "body"]`       |

## Authors

Karsten Schmidt

## License

&copy; 2020 Karsten Schmidt // Apache Software License 2.0
