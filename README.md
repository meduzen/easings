# easings.scss

This package adds a set of CSS [`cubic-bezier`](https://codepen.io/seanseansean/pen/GgxrXw) [timing functions](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function) (also named _easings_) as Custom Properties.

Goals and benefits of the package:
- lighter generated CSS;
- shorter `cubic-bezier()` syntax;
- code portability: same syntax as similar libraries.

Also read: [ideas](https://github.com/meduzen/easings/issues/1) for this package.

## Summary

- [Easings list](#easings-list)
- [Installation](#installation)
- [Usage](#usage)
- [Options](#options)
  - [Partial import (`$easings`)](#partial-import-easings)
  - [Legacy browsers (`$easings-legacy`)](#legacy-browsers-easings-legacy)
- [Other easings](#other-easings)

## Easings list

If you’re familiar with [Bourbon](https://www.bourbon.io/docs/4/#timing-functions)’s easings, they are exactly the same. ([Other visualization](https://codepen.io/slavanossar/full/ERoaBx)).

| easing | in-out | in | out |
|--|--|--|--|
| Sine | `$ease-in-out-sine`  | `$ease-in-sine`  | `$ease-out-sine` |
| Quad | `$ease-in-out-quad`  | `$ease-in-quad`  | `$ease-out-quad` |
| Cubic | `$ease-in-out-cubic`  | `$ease-in-cubic`  | `$ease-out-cubic` |
| Quart | `$ease-in-out-quart`  | `$ease-in-quart`  | `$ease-out-quart` |
| Quint | `$ease-in-out-quint`  | `$ease-in-quint`  | `$ease-out-quint` |
| Expo | `$ease-in-out-expo`  | `$ease-in-expo`  | `$ease-out-expo` |
| Circ | `$ease-in-out-circ`  | `$ease-in-circ`  | `$ease-out-circ` |
| Back | `$ease-in-out-back`  | `$ease-in-back`  | `$ease-out-back` |

Aliases for a shorter syntax (not available in Bourbon):

| easing | in-out | in | out |
|--|--|--|--|
| Sine | `$in-out-sine`  | `$in-sine`  | `$out-sine` |
| Quad | `$in-out-quad`  | `$in-quad`  | `$out-quad` |
| Cubic | `$in-out-cubic`  | `$in-cubic`  | `$out-cubic` |
| Quart | `$in-out-quart`  | `$in-quart`  | `$out-quart` |
| Quint | `$in-out-quint`  | `$in-quint`  | `$out-quint` |
| Expo | `$in-out-expo`  | `$in-expo`  | `$out-expo` |
| Circ | `$in-out-circ`  | `$in-circ`  | `$out-circ` |
| Back | `$in-out-back`  | `$in-back`  | `$out-back` |

## Installation

1. `npm install easings.scss` pulls the package into your project.
2. `@import '~easings.scss';` in a SCSS file make all the easings available as SCSS variables in addition to adding them at [`:root`](https://developer.mozilla.org/en-US/docs/Web/CSS/:root) level.

This means the `@import` statement…
```scss
@import '~easings.scss';
```

… already outputs:

```css
:root {
  --in-sine: cubic-bezier(0.47, 0, 0.745, 0.715);
  --out-sine: cubic-bezier(0.39, 0.575, 0.565, 1);
  --in-out-sine: cubic-bezier(0.445, 0.05, 0.55, 0.95);
  --in-quad: cubic-bezier(0.55, 0.085, 0.68, 0.53);
  /* all 18 other easings… */
  --out-back: cubic-bezier(0.175, 0.885, 0.32, 1.275);
  --in-out-back: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}
```

## Usage

Write your timing functions powered by CSS Custom Properties the way you want:

```scss
.my-class {

  // using a custom property…
  transition: opacity 1.3s var(--in-out-circ);

  // … or a SCSS variable (Bourbon naming)
  transition: opacity 1.3s $ease-in-out-circ;

  // … or a shorter SCSS variable
  transition: opacity 1.3s $in-out-circ;
}
```

These syntaxes all lead to the same CSS output:
```css
.my-class {
  transition: opacity 1.3s var(--in-out-circ);
}
```

> 💡 If you use Bourbon, no code change is required. Make sure you `@import` _easings.scss_ **after** _Bourbon_, and you’re all set.

## Options

### Partial import (`$easings`)

If you don’t want to import everything, write an `$easings` list before the `@import` statement:

```scss
$easings: 'in-out-quad', 'out-circ', 'in-out-back';
@import '~easings.scss;
```

This will only output the needed Custom Properties, instead of the 24 available:

```css
:root {
  --in-out-quad: cubic-bezier(0.455, 0.03, 0.515, 0.955);
  --out-circ: cubic-bezier(0.075, 0.82, 0.165, 1);
  --in-out-back: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}
```

All the 24 SCSS variables (and their aliases) remain available. In addition, the 24 `cubic-bezier` coordinates are also available with the `-value` suffix:

```scss
$in-out-cubic-value: 0.645, 0.045, 0.355, 1;
```

### Legacy browsers (`$easings-legacy`)

If you don’t want to output custom properties, set `$easings-legacy` to `true` before the `@import` statement:

```scss
$easings-legacy: true;
@import '~easings.scss;
```

With this legacy flag, no CSS will be generated in `:root`. SCSS variables will output a `cubic-bezier` function instead of a Custom Property:

Example SCSS code:
```scss
.my-class {
  transition: opacity 1.3s $ease-in-out-circ;
}
```

Generated CSS:

```css
/* with `$easings-legacy: true;` */
.my-class {
  transition: opacity 1.3s cubic-bezier(0.785, 0.135, 0.15, 0.86);
}

/* without `$easings-legacy` */
.my-class {
  transition: opacity 1.3s var(--in-out-circ);
}
```

## Other easings

*easings.scss* also adds a `bezier()` function that alias the CSS `cubic-bezier()` one, allowing a shorter syntax for your custom easings.

```scss
// You can now write this…
.my-class {
  transition-timing-function: bezier(.1, .02, 1, .7);
}

// … instead of
.my-class {
  transition-timing-function: cubic-bezier(.1, .02, 1, .7);
}
```

If you want to [reverse an easing curve](https://css-tricks.com/reversing-an-easing-curve), you can use the `reverse-bezier()` function (or its alias `r-bezier()`), accepting 1 or 4 parameters.

```scss
// 4 parameters
.my-class {
  transition-timing-function: reverse-bezier(.1, .02, 1, .7);
}

// 1 parameter
$my-easing-not-yet-reversed: .1, .02, 1, .7;

.my-class {
  transition-timing-function: reverse-bezier($my-easing-not-yet-reversed);
}

// r-bezier alias
.my-class {
  transition-timing-function: r-bezier(.1, .02, 1, .7);
}
```
