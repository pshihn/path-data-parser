# path-data-parser

I know there are a bunch of SVG path parsers out there, but here's one that I have been using for a few years now. It's small, tree-shakable and provides four simple functions.

## Install

From npm

```
npm install --save path-data-parser
```

The code is shipped as ES6 modules. 

## Methods

The module exposes 4 methods

### pasrePath(d: string): Segment[]

This is the main method that parses the SVG path data. You pass in the path string and it returns an array of `Segments`. A segment has a `key` which is the commands, e.g. `M` or `h` or `C`; and `data` which is an array of numbers used by the command

```javascript
Segment {
  key: string;
  data: number[];
}
```

example:

```javascript
import { parsePath } from 'path-data-parser';
const segments = parsePath('M10 10 h 80 v 80 h -80 C Z');
```

### serialize(segments: Segment[]): string

This is essentially the opposite of the `parsePath` command. It outputs a path string from an array of `Segment` objects.

```javascript
import { parsePath, serialize, absolutize } from 'path-data-parser';

const segments = parsePath('M10 10 h 80 v 80 h -80 Z');
const absoluteSegments = absolutize(segments); // Turns relative commands to absolute
const outputPath = serialize(absoluteSegments);
console.log(outputPath);
// Logs:
// M 10 10 H 90 V 90 H 10 Z
```

### absolutize(segments: Segment[]): Segment[]


