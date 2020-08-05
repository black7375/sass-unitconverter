sass-unitconverter
==============

**Convert Anything** (almost)

At the moment the following units are supported (please comment if something is wrong/missing):

````SCSS
px, pt, pc, mm, cm, in, em, rem, ex, ch, vw, vh, vmin, vmax,
deg, rad, grad, turn, dpi, dpcm, dppx, s, ms, hz, khz, number,
ratio
````

**Install**
````shell
## Yarn
yarn add sass-unitconverter

## NPM
npm install sass-unitconverter

## Github Repository
npm install @black7375/sass-unitconverter
````


**Simple Syntax**

Rather than going with the "good" old fromUnit-to-toUnit(fromUnit) syntax this function set is based on toUnit(fromUnit) making it a lot shorter and less cumbersome to maintain – as shown below :-)

````SCSS
       pt-to-px(input);
       pc-to-px(input);
       mm-to-px(input);
       cm-to-px(input);    ==>   px(input);
       in-to-px(input);
       em-to-px(input);
       rem-to-px(input);
       num-to-px(input);
`````
**Note!**

* In this library, `num` means pure numbers.(`10` => :o:, `10px` => :x:)

* To allow conversion between relative and absolute lengths `em` and `rem` are calculated as pixel values based on `$root-font-size` and `$base-font-size` (`16px` browser default). If you change the base font size of your document – remember to set the `$root-font-size` and `$base-font-size` variables accordingly.

* To ease the job of handling compounds the `em` function takes multiple arguments. Each argument is treated as an em compound and used to calculate the visual size.
Example – how to set a visual size of `18px` on a class nested in an element with a font-size of `2em`:
````SCSS
      .class {
          font-size: em(18px, 2em);  ==>   0.5625em;
      }
`````
* If you use unit conversion in relation to the font shorthand syntax be aware that line-height "/" will cause division. To prevent this from happening you can either either interpolate the value or use + to add the pieces together without calculation:
````SCSS
      h2 { 
          font:300 #{em(24px)}/3 'Lato', sans-serif;
      }
````

**Conversion Table**
| **Type**        |                       **Function** | **Input Units**                                                                                                                |
|-----------------|-----------------------------------:|:------------------------------------------------------------------------------------------------------------------------------:|
| Absolute length |                        px($input); | px, pt, pc, in, mm, cm, em, rem, number                                                                                        |
|                 |                        pt($input); | ǀǀ                                                                                                                             |
|                 |                        pc($input); | ǀǀ                                                                                                                             |
|                 |                        mm($input); | ǀǀ                                                                                                                             |
|                 |                        cm($input); | ǀǀ                                                                                                                             |
|                 |                        in($input); | ǀǀ                                                                                                                             |
| Relative length |                        em($input); | ǀǀ                                                                                                                             |
|                 |                       rem($input); | ǀǀ                                                                                                                             |
|                 |                        ex($input); | ex, num                                                                                                                        |
|                 |                        ch($input); | ch, num                                                                                                                        |
|                 |                        vw($input); | vw, num                                                                                                                        |
|                 |                        vh($input); | vh, num                                                                                                                        |
|                 |                      vmin($input); | vmin, num                                                                                                                      |
|                 |                      vmax($input); | vmax, num                                                                                                                      |
| Angle           |                        em($input); | deg, rad, grad, turn, num                                                                                                      |
|                 |                       rad($input); | ǀǀ                                                                                                                             |
|                 |                      grad($input); | ǀǀ                                                                                                                             |
|                 |                      turn($input); | ǀǀ                                                                                                                             |
| Resulution      |                       dpi($input); | dpi, dpcm, dppx, num                                                                                                           |
|                 |                      dpcm($input); | ǀǀ                                                                                                                             |
|                 |                      dppx($input); | ǀǀ                                                                                                                             |
| Time            |                        ms($input); | ms, s, num                                                                                                                     |
|                 |                         s($input); | ǀǀ                                                                                                                             |
| Frequency       |                        hz($input); | Hz, kHz, num                                                                                                                   |
|                 |                       khz($input); | ǀǀ                                                                                                                             |
| String          | str($input);  <br> string($input); | Anything not null                                                                                                              |
| Number          |  num($input); <br> number($input); | px, pt, pc, mm, cm, in,  em, rem, ex, ch,vw, vh, vmin, vmax, deg, rad, grad, turn,dpi, dpcm, dppx, s, ms, hz, khz, num, string |
|                 |                       int($input); | ǀǀ                                                                                                                             |
|                 |                      uint($input); | ǀǀ                                                                                                                             |
| Etc             |                  one-unit($input); | px, pt, pc, mm, cm, in,  em, rem, ex, ch,vw, vh, vmin, vmax, deg, rad, grad, turn,dpi, dpcm, dppx, s, ms, hz, khz, num         |
|                 |            to-unit($input, $unit); | ǀǀ                                                                                                                             |
|                 |       to-unit-list($input, $unit); | ǀǀ                                                                                                                             |
|                 |        to-unit-map($input, $unit); | ǀǀ                                                                                                                             |

**Check Unit**

* You can check unit & types with `is-[unit]($input)`

* Types: `null`, `bool`, `color`, `list`, `map`

* However, there is a strict mode for `num`, `null`.(Default value is `true`)
````SCSS
      is-px(16px);         ==> true;
      is-px(16pt);         ==> false;
      
      is-num(16,    true); ==> true;
      is-num(16px,  true); ==> false;
      is-num(16px, false); ==> true;
      
      is-null(null, true); ==> true;
      is-null((),   true); ==> false;
      is-null('',   true); ==> false;
      is-null((),  false); ==> true;
      is-null('',  false); ==> true;
`````

Cive it a try on:
[Sassmeister.com](http://www.sassmeister.com/gist/5943041498e406ff2d1d452ac2c31c9f)


<hr>


[The MIT License (MIT)](https://opensource.org/licenses/MIT)
Copyright (c) 2016 Jakob Eriksen

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
