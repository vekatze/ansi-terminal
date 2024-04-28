# `ansi-terminal`

`ansi-terminal` is a thin wrapper over ANSI escape sequences.

This is a library for the [Neut](https://vekatze.github.io/neut/) programming language.

## Installation

```sh
neut get ansi https://github.com/vekatze/ansi-terminal/raw/main/archive/0-2-0.tar.zst
```

## Example

```neut
import {
  ansi.color {Blue, Red, set-foreground-color},
  ansi.style {Bold, Normal, set-style},
}

define some-func(): unit {
  set-foreground-color(Red);
  set-style(Bold);
  print("error: ");
  set-style(Normal);
  print("Lorem ipsum dolor sit amet, consectetur adipiscing elit.\n");
  set-foreground-color(Blue);
  set-style(Bold);
  print("hint: ");
  set-style(Normal);
  print("くらきよりくらきみちにぞいりぬべきはるかにてらせやまのはのつき。\n")
}
```
