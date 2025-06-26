# `ansi-terminal`

`ansi-terminal` is a thin wrapper over ANSI escape sequences.

This is a library for the [Neut](https://vekatze.github.io/neut/) programming language.

## Installation

```sh
neut get ansi https://github.com/vekatze/ansi-terminal/raw/main/archive/0-5-5.tar.zst
```

## Types

```neut
data ansi-kit

define make-ansi-kit(sink: descriptor, capacity: int): ansi-kit

define make-ansi-kit-unbuffered(sink: descriptor): ansi-kit

// writes text
define write<r := rho>(k: &ansi-kit, t: &text): system(unit)

// writes text + "\n"
define write-line<r := rho>(k: &ansi-kit, t: &text): system(unit)

// writes the ANSI escape code of a command `c` (see below)
inline write-code<r := rho>(k: &ansi-kit, c: command): system(unit)

// flush the buffer of `k` (if any)
define flush<r := rho>(k: &ansi-kit): system(unit)

data command {
| Set-Style(style)
| Move-Cursor(cursor-movement)
| Erase(space, span)
}

data style {
| Normal
| Bold
| Faint
| Italic
| Underline
| Color(color-layer, color)
}

data color-layer {
| Foreground
| Background
}

data color {
| Color-16(color-intensity, color-ansi)
| Color-256(int8)
| Color-RGB(int8, int8, int8)
}

data color-intensity {
| Dull
| Vivid
}

data color-ansi {
| Black
| Red
| Green
| Yellow
| Blue
| Magenta
| Cyan
| White
}

data cursor-movement {
| Up(int)
| Down(int)
| Forward(int)
| Backward(int)
| Up-Start(int)
| Down-Start(int)
| To-Column(int)
| To(int, int)
}

data space {
| Line
| Screen
}

data span {
| From-Cursor
| To-Cursor
| Whole
}
```

## Example

```neut
define some-func(): system(unit) {
  pin k = make-ansi-kit of {sink := stdout, capacity := 100};
  // prints "error: " in bold red
  try _ = write-code(k, Set-Style(Color(Foreground, Color-16(Vivid, Red))));
  try _ = write-code(k, Set-Style(Bold));
  try _ = write(k, "error: ");
  try _ = write-code(k, Set-Style(Normal));
  // prints "Lorem.." in plain text
  try _ = write(k, "Lorem ipsum dolor sit amet, consectetur adipiscing elit.\n");
  // prints "hint: " in bold blue
  try _ = write-code(k, Set-Style(Color(Foreground, Color-16(Vivid, Blue))));
  try _ = write-code(k, Set-Style(Bold));
  try _ = write(k, "hint: ");
  // prints "くらきより.." in plain text
  try _ = write-code(k, Set-Style(Normal));
  try _ = write(k, "くらきよりくらきみちにぞいりぬべきはるかにてらせやまのはのつき\n");
  flush(k)
}
```
