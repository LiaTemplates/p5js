<!--
author:   André Dietrich

email:    LiaScript@web.de

version:  0.0.2

language: en

narrator: US English Female

comment:  Just a simple p5js template for LiaScript.

logo:     https://p5js.org/assets/img/p5js.svg

script:   https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.2.0/p5.min.js

@P5.eval: @P5.eval_(@uid)

@P5.eval_
<script>

let div = window.document.getElementById('p5-@0')

div.innerHTML = ""

let sketch = function(p5) {
    // looks strange, but this is required to use backtics within your input-macro
    try {
      eval(`@'input`)
    } catch (e) {
      console.error(e, "- line: ", getLineNumber(e) + 15)
    }

    // react to try to eval console inputs, like `p5.line(0,0,500,500)`
    send.handle("input", input => {
      try{
        let rslt = eval(input)

        if (rslt != undefined)
          console.log(rslt)
      } catch (e) {
        console.error(e);
      }
    })
};

let env = new p5(sketch, div);

// handle stop-button events
send.handle("stop", e => { env.remove() })

// Tell LiaScript if the shell should wait, stop, or open a terminal
// * "LIA: wait"
// * "LIA: stop"
"LIA: terminal"
</script>

<div id="p5-@0"></div>

@end


@P5.project: @P5.project_(@uid)

@P5.project_
<script>

let div = window.document.getElementById('p5-@0')

div.innerHTML = ""

let sketch = function(p5) {

    try {
      let input = [
        `@'input(0)`,
        `@'input(1)`,
        `@'input(2)`,
        `@'input(3)`,
        `@'input(4)`,
        `@'input(5)`,
        `@'input(6)`,
        `@'input(7)`,
        `@'input(8)`,
        `@'input(9)`,
      ]

      for(let i=1; i<input.length; i++) {
        if (input[i].startsWith(input[0])) {
          input[i] = ""
        }
      }

      eval(input.join("\n"))
    } catch (e) {
      console.error(e)
    }

    // react to try to eval console inputs, like `p5.line(0,0,500,500)`
    send.handle("input", input => {
      try{
        let rslt = eval(input)

        if (rslt != undefined)
          console.log(rslt)
      } catch (e) {
        console.error(e);
      }
    })
};

let env = new p5(sketch, div);

// handle stop-button events
send.handle("stop", e => { env.remove() })

"LIA: terminal"
</script>

<div id="p5-@0"></div>

@end

-->

# p5js - Template

                         --{{0}}--
A simple template for executing [p5.js](https://p5js.org) in
[LiaScript](https://LiaScript.github.io). You can use it to build more
sophisticated Tutorials ... Just check out, how this File gets rendered by
LiaScript:

__Try it on LiaScript:__

https://liascript.github.io/course/?https://raw.githubusercontent.com/liaTemplates/p5js/0.0.2/README.md

__See the project on Github:__

https://github.com/liaTemplates/p5js

                         --{{1}}--
There are three ways to use this template. The easiest way is to use the
`import` statement and the url of the raw text-file of the master branch or any
other branch or version. But you can also copy the required functionionality
directly into the header of your Markdown document, see therefor the
[Implementation](#Implementation). And of course, you could also clone this
project and change it, as you wish.

                           {{1}}
1. Load the macros via

   `import: https://raw.githubusercontent.com/LiaTemplates/p5js/0.0.2/README.md`

2. Copy the definitions into your Project

3. Clone this repository on GitHub


## `@P5.eval`

                         --{{0}}--
Simply add `@P5.eval` to the end of your Processing code-block to make it
executable. This will even cover a basic error handling with a line number, if
the execution somehow fails.

``` js
p5.setup = function () {
  p5.createCanvas(720, 400);
  p5.background(230);
  p5.strokeWeight(2);

  console.log("setup")
  console.warn("geht hoffentlich...")
}

p5.draw = function () {
  if (p5.mouseIsPressed) {
    p5.stroke(255);
  } else {
    p5.stroke(237, 34, 93);
  }
  p5.line(p5.mouseX - 66, p5.mouseY, p5.mouseX + 66, p5.mouseY);
  p5.line(p5.mouseX, p5.mouseY - 66, p5.mouseX, p5.mouseY + 66);
}
```
@P5.eval

## `@P5.project`

                         --{{0}}--
If you have a more sophisticated project and you want to split it into multiple
files, you can use the LiaScript project notation. The `+` or the `-` in front
of the filenames define if the code should be shown or hidden. The user can
still open it to inspect it. Add the `@P5.project` to the end of
your Processing project to make it executable. You can split your code into max
10 files.

``` js +setup.js
p5.setup = function () {
  p5.createCanvas(720, 400);
  p5.background(230);
  p5.strokeWeight(2);

  console.log("setup")
  console.warn("geht hoffentlich...")
}
```
``` js -draw.js
p5.draw = function () {
  if (p5.mouseIsPressed) {
    p5.stroke(255);
  } else {
    p5.stroke(237, 34, 93);
  }
  p5.line(p5.mouseX - 66, p5.mouseY, p5.mouseX + 66, p5.mouseY);
  p5.line(p5.mouseX, p5.mouseY - 66, p5.mouseX, p5.mouseY + 66);
}
```
@P5.project


## Implementation

                         --{{0}}--
There are two macros, `@P5.eval` and `@P5.project`, as well as the hidden
ones, which actually defines all code required.

```html
script:   https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.2.0/p5.min.js


@P5.eval: @P5.eval_(@uid)

@P5.eval_
<script>

let div = window.document.getElementById('p5-@0')

div.innerHTML = ""

let sketch = function(p5) {
    // looks strange, but this is required to use backtics within your input-macro
    try {
      eval(`@'input`)
    } catch (e) {
      console.error(e, "- line: ", getLineNumber(e) + 15)
    }

    // react to try to eval console inputs, like `p5.line(0,0,500,500)`
    send.handle("input", input => {
      try{
        let rslt = eval(input)

        if (rslt != undefined)
          console.log(rslt)
      } catch (e) {
        console.error(e);
      }
    })
};

let env = new p5(sketch, div);

// handle stop-button events
send.handle("stop", e => { env.remove() })

// Tell LiaScript if the shell should wait, stop, or open a terminal
// * "LIA: wait"
// * "LIA: stop"
"LIA: terminal"
</script>

<div id="p5-@0"></div>

@end


@P5.project: @P5.project_(@uid)

@P5.project_
<script>

let div = window.document.getElementById('p5-@0')

div.innerHTML = ""

let sketch = function(p5) {

    try {
      let input = [
        `@'input(0)`,
        `@'input(1)`,
        `@'input(2)`,
        `@'input(3)`,
        `@'input(4)`,
        `@'input(5)`,
        `@'input(6)`,
        `@'input(7)`,
        `@'input(8)`,
        `@'input(9)`,
      ]

      for(let i=1; i<input.length; i++) {
        if (input[i].startsWith(input[0])) {
          input[i] = ""
        }
      }

      eval(input.join("\n"))
    } catch (e) {
      console.error(e)
    }

    // react to try to eval console inputs, like `p5.line(0,0,500,500)`
    send.handle("input", input => {
      try{
        let rslt = eval(input)

        if (rslt != undefined)
          console.log(rslt)
      } catch (e) {
        console.error(e);
      }
    })
};

let env = new p5(sketch, div);

// handle stop-button events
send.handle("stop", e => { env.remove() })

"LIA: terminal"
</script>

<div id="p5-@0"></div>

@end
```

                         --{{1}}--
If you want to minimize loading effort in your LiaScript project, you can also
copy this code and paste it into your main comment header, see the code in the
raw file of this document.

{{1}} https://raw.githubusercontent.com/liaTemplates/p5js/main/README.md


## Demo

> Because it is so beautiful, I added some more examples, to demonstrate how
> beautiful p5js is ...

### Mouse pressed

``` js
p5.setup = function () {
  p5.createCanvas(720, 400);
  p5.background(230);
  p5.strokeWeight(2);
}

p5.draw = function () {
  if (p5.mouseIsPressed) {
    p5.stroke(255);
  } else {
    p5.stroke(237, 34, 93);
  }
  p5.line(p5.mouseX - 66, p5.mouseY, p5.mouseX + 66, p5.mouseY);
  p5.line(p5.mouseX, p5.mouseY - 66, p5.mouseX, p5.mouseY + 66);
}
```
@P5.eval

### Robot

```js    +settings.js
let w = 640;
let h = 360;
let linecolor = 33;
let L1 = 80; //Länge Glied A0-A
let L2 = 60; //Länge Glied A-TCP
let theta1 = 0; //Nullstellung
let theta2 = 0; //Nullstellung
let translation = p5.createVector(w/2,h/2); //A0 ist in der Mitte des Fensters
let A0 = p5.createVector(0,0);
let a0a = p5.createVector(L1, 0);
let A = p5.createVector(A0.x + a0a.x, A0.y + a0a.y); //A in Nullstellung
let atcp = p5.createVector(L2, 0);
let TCP = p5.createVector(A.x + atcp.x, A.y + atcp.y); //TCP in Nullstellung
let Pos = p5.createVector(TCP.x, TCP.y); //Soll = Ist
```
``` js   +init.js
/// Initialisierung
p5.setup = function() {
  p5.createCanvas(640, 360);
  p5.strokeWeight(10.0);
  p5.stroke(255, 100);
}

/// Zeichnen der Oberfläche
p5.draw = function() {
  p5.translate(640/2, 360/2);
  p5.scale(1,-1);

  // Farben einstellen
  p5.stroke(linecolor, 100);
  p5.background(255);

  // Arbeitsraumgrenzen
  p5.arc(A0.x, A0.y, (L1+L2)*2, (L1+L2)*2, 0, Math.PI * 2);
  p5.noFill();

  // Roboter einzeichnen
  p5.line(A0.x, A0.y, A.x, A.y);
  p5.line(A.x, A.y, TCP.x, TCP.y);
  p5.point(Pos.x, Pos.y);


  // Roboter einzeichnen
  //p5.line(A0.x + translation.x, A0.y + translation.y, A.x   + translation.x, A.y   + translation.y);
  //p5.line(A.x  + translation.x, A.y  + translation.y, TCP.x + translation.x, TCP.y + translation.y);
  //p5.point(Pos.x + translation.x, Pos.y + translation.y);
}

/// Wenn die Maus über die Oberfläche bewegt wird
p5.mouseMoved = function() {
  Pos.x = p5.mouseX - translation.x;
  Pos.y = -p5.mouseY + translation.y;

  moveRobot();
}

/// Neue Stellung vorgeben
function moveRobot() {
  //1. Gelenkwerte ermitteln
  inverseKinematics(Pos.x, Pos.y);

  //2. TCP ermitteln und anfahren
  forwardKinematics(theta1, theta2);
}
```
``` js -kinematics.js
/// Frage: Wenn ich theta1 und theta2 vorgebe, wie lauten dann x und y des TCP?
function forwardKinematics (t1, t2) {
  //A muss als Zwischenpunkt mit berechnet werden, sonst kann es nicht simuliert werden
  //1. Glied 1 drehen
  a0a = p5.createVector(L1, 0).rotate(t1);
  A = p5.createVector(A0.x + a0a.x, A0.y + a0a.y);

  //2. Glied 2 drehen
  atcp = p5.createVector(L2, 0).rotate(t1 + t2);
  TCP = p5.createVector(A.x + atcp.x, A.y + atcp.y);
}


/// Frage: Wenn ich x und y des TCP vorgebe, wie lauten dann theta1 und theta2?

function inverseKinematics(x, y) {
  //1. Berechnen der Strecke C
  let C = Math.sqrt(x*x + y*y);

  //2. Berechnen von Gamma
  let gamma = Math.atan2(y, x);

  // Grenzwertbetrachtung
  if (C > L1 + L2) {
    linecolor = 100;
    theta1 = gamma;
    theta2 = 0;
    //println(millis(),"Punkt außerhalb des Arbeitsraums");
  }
  else if (C < Math.abs(L1 - L2)) {
    linecolor = 100;
    //println(millis(),"Punkt innerhalb des nicht erreichbaren Arbeitsraums");
  }
  else if ((C == 0) && (L1 == L2)) {
    linecolor = 100;
    //println(millis(),"Unendlich viele Lösungen");
  }

  else {
    linecolor = 0;

    // Variantenbetrachtung
    if (C == L1 + L2) {
       theta1 = gamma;
       theta2 = 0;
    }

    //Berechnung von theta2
    theta2 = Math.acos((x*x+y*y-(L1*L1+L2*L2))/(2*L1*L2));


    //Berechnung von theta1
    let delta = Math.acos((L1*L1-L2*L2+C)/(L1*L2*C));
    theta1 = gamma - delta/2; ///???
  }
}
```
@P5.project
