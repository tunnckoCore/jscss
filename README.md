JsCSS
========

Embed CSS in your JavaScript.

It's like React's JSX, but for CSS.

## Usage

```bash
npm install -g jscss

jscss [--pretty] [filename]
```

## Syntax

JsCSS can magically differentiate JavaScript and CSS (hopefully, using one big Regex).

This makes it possible to mix both languages in an intuitive way.
A special preprocessor like Sass and LESS is not needed.
JavaScript is the preprocessor.

Within CSS expressions, `|` can be used to create JavaScript zones. They will be eval'd (literally)
like JavaScript.

## Example

```CSS
var cool_colour = "rgb(39, 192, 129)";

* {
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
}

p {
  color: rgb(238 , 23, 12);
}

for (var i = 0; i < 5; i++) {

  div .hello:nth-child(|i|) {
    color: rgb(| i * 10 |, 20, |i * 20|);
  }

}

var i = 0;

p > li {
  background-color: |cool_colour|;
}

while (i < 4) {
  
  p > li.number-|i| {
    width: |i * 10|;
  }

  i++;
}
```
This will compile to plain CSS:
`jscss example.jscss --pretty`

```CSS
* {
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
}

p {
  color: rgb(238 , 23, 12);
}

div .hello:nth-child(0) {
  color: rgb(0, 20, 0);
}

div .hello:nth-child(1) {
  color: rgb(10, 20, 20);
}

div .hello:nth-child(2) {
  color: rgb(20, 20, 40);
}

div .hello:nth-child(3) {
  color: rgb(30, 20, 60);
}

div .hello:nth-child(4) {
  color: rgb(40, 20, 80);
}

p > li {
  background-color: rgb(39, 192, 129);
}

p > li.number-0 {
  width: 0;
}

p > li.number-1 {
  width: 10;
}

p > li.number-2 {
  width: 20;
}

p > li.number-3 {
  width: 30;
}

```

## Aims

This isn't done yet. Things will change.

* Use a VM to execute JavaScript more safely.
* Attach a "standard library", which can do common colour-calculations
* Test against even more complex selectors.

## License

MIT - `LICENSE`
