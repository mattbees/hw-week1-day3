![codeclan_logo](https:  user-images.githubusercontent.com/11422619/54070681-ca4c5200-425a-11e9-8cf8-cd6a191bc3cd.png)

# Scope: Who Dunnit

### Learning Objectives

- Understand function scope
- Know the difference in between the let and const keywords

## Brief

Using your knowledge about scope and variable declarations in JavaScript, look at the following code snippets and predict what the output or error will be and why. Copy the following episodes into a JavaScript file and add comments under each one detailing the reason for your predicted output.

### MVP

#### Episode 1

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Library',
  weapon: 'Rope'
};

const declareMurderer = function() {
  return `The murderer is ${scenario.murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```

<!-- Episode 1 - prediction:
   This will return:
   The murderer is Miss Scarlet

   return value:
   The murderer is Miss Scarlet.

   reason:
   The const variables are declared in global scope.
   -->


#### Episode 2

```js
const murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```

<!--    Episode 2 - prediction:
   This will return:
   "The murderer is Mrs Peacock."

   return value:
   The murderer is Professor Plum.

   reason:
   changeMurderer() updates the value before it is written out. All in global scope.
   CORRECTION: const murderer cannot be reassigned
   -->


#### Episode 3

```js
let murderer = 'Professor Plum';

const declareMurderer = function() {
  let murderer = 'Mrs. Peacock';
  return `The murderer is ${murderer}.`;
}

const firstVerdict = declareMurderer();
console.log('First Verdict: ', firstVerdict);

const secondVerdict = `The murderer is ${murderer}.`;
console.log('Second Verdict: ', secondVerdict);
```

<!--    Episode 3 - prediction:
   This will return "Second verdict: The murderer is Professor Plum."

   return value:
   Second Verdict:  The murderer is Professor Plum.

   reason:
   declareMurderer() and firstVerdict are never called.
   -->


#### Episode 4

```js
let suspectOne = 'Miss Scarlet';
let suspectTwo = 'Professor Plum';
let suspectThree = 'Mrs. Peacock';

const declareAllSuspects = function() {
  let suspectThree = 'Colonel Mustard';
  return `The suspects are ${suspectOne}, ${suspectTwo}, ${suspectThree}.`;
}

const suspects = declareAllSuspects();
console.log(suspects);
console.log(`Suspect three is ${suspectThree}.`);
```

<!--    Episode 4 - prediction:
    This will return:
    The suspects are Miss Scarlet, Professor Plum, Colonel Mustard.
    Suspect three is Mrs. Peacock.

    return value:
    The suspects are Miss Scarlet, Professor Plum, Colonel Mustard.
    Suspect three is Mrs. Peacock.
    reason:
    When declareAllSuspects() is called, let suspect3 is updated within the block.
    Outside of declareAllSuspects() suspect3 retains its original value.
   -->


#### Episode 5

```js
const scenario = {
  murderer: 'Miss Scarlet',
  room: 'Kitchen',
  weapon: 'Candle Stick'
};

const changeWeapon = function(newWeapon) {
  scenario.weapon = newWeapon;
}

const declareWeapon = function() {
  return `The weapon is the ${scenario.weapon}.`;
}

changeWeapon('Revolver');
const verdict = declareWeapon();
console.log(verdict);
```

<!--    Episode 5 - prediction:
    This will return:
    The weapon is the Revolver.

    return value:
    The weapon is the Revolver.

    reason:
    changeWeapon('Revolver') updates the value of scenario.weapon to 'Revolver' as it is mutable.
   -->


#### Episode 6

```js
let murderer = 'Colonel Mustard';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    murderer = 'Mrs. White';
  }

  plotTwist();
}

const declareMurderer = function () {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```

<!--    Episode 6 - prediction:
    This will return:
    The murderer is Mrs. White.

    return value:
    The murderer is Mrs. White.

    reason:
    changeMurderer() updates the value of let murderer (global scope).
   -->


#### Episode 7

```js
let murderer = 'Professor Plum';

const changeMurderer = function() {
  murderer = 'Mr. Green';

  const plotTwist = function() {
    let murderer = 'Colonel Mustard';

    const unexpectedOutcome = function() {
      murderer = 'Miss Scarlet';
    }

    unexpectedOutcome();
  }

  plotTwist();
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

changeMurderer();
const verdict = declareMurderer();
console.log(verdict);
```

<!--    Episode 7 - prediction:
    This will return:
    The murderer is Colonel Mustard.

    return value:
    The murderer is Mr. Green.

    reason:
    New let murderer declaration within function? I think this updates existing variable as its in global scope.
    CORRECTION: the new let murderer declaration in plotTwist() creates a new let that only exists within its scope and so global let murderer is not updated.
    -->


#### Episode 8

```js
const scenario = {
  murderer: 'Mrs. Peacock',
  room: 'Conservatory',
  weapon: 'Lead Pipe'
};

const changeScenario = function() {
  scenario.murderer = 'Mrs. Peacock';
  scenario.room = 'Dining Room';

  const plotTwist = function(room) {
    if (scenario.room === room) {
      scenario.murderer = 'Colonel Mustard';
    }

    const unexpectedOutcome = function(murderer) {
      if (scenario.murderer === murderer) {
        scenario.weapon = 'Candle Stick';
      }
    }

    unexpectedOutcome('Colonel Mustard');
  }

  plotTwist('Dining Room');
}

const declareWeapon = function() {
  return `The weapon is ${scenario.weapon}.`
}

changeScenario();
const verdict = declareWeapon();
console.log(verdict);
```

<!--    Episode 8 - prediction:
    The weapon is Lead Pipe.

    return value:
    The weapon is Candle Stick.

    reason:
    scenario.weapon is not updated by unexpectedOutcome() because the condition evaluates to false.
    CORRECTION: plotTwist() is called first and unexpectedOutcome() is called within plotTwist(). murderer has therefore been updated and the condition evaluates to true.
   -->


#### Episode 9

```js
let murderer = 'Professor Plum';

if (murderer === 'Professor Plum') {
  let murderer = 'Mrs. Peacock';
}

const declareMurderer = function() {
  return `The murderer is ${murderer}.`;
}

const verdict = declareMurderer();
console.log(verdict);
```

<!--    Episode 9 - prediction:
    The murderer is Professor Plum.

    return value:
    The murderer is Professor Plum.

    reason:
    The if statement does not impact the global variable.
   -->


### Extensions

Make up your own episode!

```js
const scenario = {
  murderer: "Professor Plum",
  room: "Dining room",
  weapon: "Candle stick"
}

let victim = "Colonel Mustard";

const crime = (perp) => {
  if (perp === "Mrs. Peacock") {
    scenario.room = "Pantry";
    let victim = "Miss Plum";
  }
}

const declareCrime = function() {
  crime("Mrs. Peacock");
  return `The victim, ${victim}, was found in the ${scenario.room}.`;

}

console.log(declareCrime());
```
