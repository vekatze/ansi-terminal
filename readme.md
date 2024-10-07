# `ansi-terminal`

`ansi-terminal` is a thin wrapper over ANSI escape sequences.

This is a library for the [Neut](https://vekatze.github.io/neut/) programming language.

## Installation

```sh
neut get ansi https://github.com/vekatze/ansi-terminal/raw/main/archive/0-4-17.tar.zst
```

## Types

```neut
// Applies `c` as the foreground color to all text printed after this call.
define set-foreground-color(c: color): unit

// Applies `c` as the background color to all text printed after this call.
define set-background-color(c: color): unit

// Applies the style `s` to all text printed after this call.
// You can call `set-style(Normal)` to reset colors and styles.
define set-style(s: style): unit
```

## Example

```neut
import {
  ansi.color {Blue, Red, set-foreground-color},
  ansi.style {Bold, Normal, set-style},
}

define some-func(): unit {
  // prints "error: " in bold red
  set-foreground-color(Red);
  set-style(Bold);
  print("error: ");
  set-style(Normal);
  // prints "Lorem.." in plain text
  print("Lorem ipsum dolor sit amet, consectetur adipiscing elit.\n");
  // prints "hint: " in bold blue
  set-foreground-color(Blue);
  set-style(Bold);
  print("hint: ");
  // prints "くらきより.." in plain text
  set-style(Normal);
  print("くらきよりくらきみちにぞいりぬべきはるかにてらせやまのはのつき。\n")
}
```
