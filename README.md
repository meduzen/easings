# easings.scss

_easings.scss_ adds a set of CSS [`cubic-bezier`](https://codepen.io/seanseansean/pen/GgxrXw) [timing functions](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function) (also named _easings_) as [Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties).

This library brings:
- a set of easings (and their reversed version!) as CSS custom properties and SASS variables;
- lighter generated CSS;
- a [shorter `cubic-bezier()`](#custom-easings) syntax;
- reversed bezier curves with [`reverse-bezier()`](#reverse-easings);
- code portability: same syntax as similar libraries.

⚠️ **`easings.scss` version `1.x` is compatible with Dart SASS while version `0.x` sticks to `node-sass`. If you’re not sure about your environment, start with the [installation section](#installation).** The installation step is the only usage difference between both versions, but if you prefer to only read the documentation for `0.x`, see [v0.3.1 documentation](https://github.com/meduzen/easings/tree/v0.3.1#contents).

## Summary

- [Easings list](#easings-list)
  - [Reversed easings curves](#reversed-easings-curves)
- [Usage](#usage)
  - [Custom easings](#custom-easings)
  - [Reverse easings](#reverse-easings)
- [Installation](#installation)
- [Options](#options)
  - [Partial import (`$easings`)](#partial-import-easings)
  - [Legacy browsers (`$easings-legacy`)](#legacy-browsers-easings-legacy)

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

### Reversed easings curves

For each of these variables, a [reversed curve](https://css-tricks.com/reversing-an-easing-curve) is available by adding the `-r` suffix to the variable name (or its alias). Examples:

- `$ease-in-out-quart-r` is the reversed curve of `$ease-in-out-quart`;
- `$out-expo-r` is the reversed curve of `$out-expo`.

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

### Custom easings

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

#### Reverse easings

If you want to reverse a custom easing curve, you can use the `reverse-bezier()` function (or its alias `r-bezier()`), accepting 1 or 4 parameters.

```scss
// 4 parameters

.my-class {
  transition-timing-function: reverse-bezier(.1, .02, 1, .7);
}

// 1 parameter

$my-curve-not-reversed-yet: .1, .02, 1, .7;

.my-class {
  transition-timing-function: reverse-bezier($my-curve-not-reversed-yet);
}

// r-bezier alias

.my-class {
  transition-timing-function: r-bezier(.1, .02, 1, .7);
}
```

## Installation

💡 `easings.scss` supports both the old and the new (2020) SASS specification, but aside from the installation step, the usage of the library remains the same in both spec.

<details>

<summary>If you’re not sure which one your project uses, this might help.</summary>

- If the project uses `node-sass` **or** if you import SCSS files using `@import`, there’s a high chance you are using **the old spec**.
- If the project uses Dart SASS (`sass`) **and** if you import SCSS files using `@use` or `@forward`, you are using **the new spec**.
- In the new spec, `@import` is deprecated and variables are not global. This is why `easings.scss` usage isn’t the same changes depending on the spec.

</details>

### Projects using Dart SASS

**Dart SASS support starts at version 1.0.**

- `npm install easings.scss` pulls the package into your project;
- `@use 'easings.scss' as *;` in a SCSS file make all the easings available as SCSS variables in addition to adding them at [`:root`](https://developer.mozilla.org/en-US/docs/Web/CSS/:root) level.

### Projects using `node-sass`

1. `npm install easings.scss@node-sass` pulls the package into your project.
2. `@import '~easings.scss';` in a SCSS file make all the easings available as SCSS variables in addition to adding them at [`:root`](https://developer.mozilla.org/en-US/docs/Web/CSS/:root) level.

### Full import

The sole `@import` or `@use` statement…

```scss
@use 'easings.scss'; // easings.scss 1.x
@import 'easings.scss'; // easings.scss 0.x
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

## Options

### Partial import (`$easings`)

If you don’t want to import everything, write an `$easings` list before the `@use` (or `@import`) statement:

```scss
// your minimal list of easings
$easings: 'in-out-quad', 'in-out-quad-r', 'out-circ', 'in-out-back';

@use 'easings.scss' with($easings: $easings); // easings.scss 1.x
@import 'easings.scss'; // easings.scss 0.x
```

This will only output the needed Custom Properties, instead of the 24 available:

```css
:root {
  --in-out-quad: cubic-bezier(0.455, 0.03, 0.515, 0.955);
  --in-out-quad-r: cubic-bezier(0.485, 0.045, 0.545, 0.97);
  --out-circ: cubic-bezier(0.075, 0.82, 0.165, 1);
  --in-out-back: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}
```

> 💡Partial import is only impacting the generated custom properties, but all the 48 SCSS variables (and their aliases) remain available. In addition, the 48 `cubic-bezier` coordinates are also available with the `-value` suffix:
>
> ```scss
> $in-out-cubic-value: 0.645, 0.045, 0.355, 1;
> $in-out-cubic-r-value: 0.645, 0, 0.355, 0.955;
> ```

### Legacy browsers (`$easings-legacy`)

If you don’t want to output custom properties, set `$easings-legacy` to `true`:

```scss
// easings.scss 1.x
@use 'easings.scss' with($easings-legacy: true);

// easings.scss 0.x
$easings-legacy: true;
@import 'easings.scss';
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
