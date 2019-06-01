<img src="https://github.com/ArunMichaelDsouza/joypad.js/blob/master/icon.png?raw=true" width="250" height="auto" alt="joypad.js icon"/>

# joypad.js
JavaScript library that lets you connect and use various gaming controllers with browsers that support the [Gamepad API](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API).
> Less than 5KB in size with zero dependencies and support for button press, axis movement events and vibration play effect.

<br/>

## Installation

#### via npm

```bash
npm install joypad.js --save
```

#### via yarn

```bash
yarn add joypad.js
```

Or, [download](https://github.com/ArunMichaelDsouza/joypad.js/releases) the latest version and include ``joypad.min.js`` to your project.

<br/>

## Usage

Once joypad.js is installed and included in your project it becomes available on the global scope - ``window.joypad``. 

If you're working with ``ES6`` modules you can include the library as follows -

```javascript
import * as joypad from 'joypad.js';
```

Once set up you can start listening to joypad.js events like so -

```javascript
joypad.on('connect', e => {
    const { id } = e.gamepad;

    console.log(`${id} connected!`);
});
```

<br/>

## API

### ``joypad.instances {object}``

Lists all the connected [Gamepad](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad) instances. Each instance defines an individual gamepad or controller with access to information such as button presses, axis movements, id, index etc.

```javascript
console.log(joypad.instances); // {0: Gamepad {id: "Wireless Contr..", index: 0 ..}, 1: Gamepad {id: "Wireless Contr..", index: 1 ..}}
```

### ``joypad.on(event, callback) {method}``

Used to attach event listeners to joypad.js events. It takes 2 parameters, an ``event`` name (which is a string) and a ``callback`` function which is fired whenever the specified event is triggered.

```javascript
joypad.on('button_press', e => {
    const { buttonName } = e.detail;

    console.log(`${buttonName} was pressed!`);
});
```

View all of the supported events [here](#user-content-events).

### ``joypad.set({settings}) {method}``

Used to set the global ``settings`` for joypad.js such as the threshold for axis movement and options for vibration play effect. It expects a single parameter, which is an object with the required setting values to be applied.

```javascript
joypad.set({
    axisMovementThreshold: 0.3
});
```

View all of the available settings [here](#user-content-settings).

### ``joypad.settings {object}``

Lists all the global settings applied to joypad.js.

```javascript
console.log(joypad.settings); // {axisMovementThreshold: 0.3, vibration: {..}}
```

### ``joypad.vibrate(gamepad, options) {method}``

Triggers the vibration play effect for a particular ``gamepad`` (which is an instance of [Gamepad](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad)). The ``options`` parameter is an object with the required vibration setting values to be applied.

```javascript
joypad.on('connect', e => {
    const { gamepad } = e;
    const options = {
        startDelay: 500,
        duration: 2000,
        weakMagnitude: 1,
        strongMagnitude: 1
    };

    joypad.vibrate(gamepad, options);
});
```

> Note: Options passed to the vibrate method will override the global vibration settings.

<br/>

## Events

### ``connect``

Fired whenever a controller is connected.

### ``disconnect``

Fired whenever a controller is disconnected.

### ``button_press``

Fired whenever a controller's button is pressed.

joypad.js supports the ``standard`` gamepad button layout which is supported by most controllers in which button locations are layed out in a left cluster of four buttons, a right cluster of four buttons , a center cluster of three buttons (some controllers have four) and a pair of front facing buttons (shoulder buttons) on the left and right side of the gamepad. 

The following table describes the default button mappings -

| Button    | Location                       |
|-----------|--------------------------------|
| button_0  | Bottom button in right cluster |
| button_1  | Right button in right cluster  |
| button_2  | Left button in right cluster   |
| button_3  | Top button in right cluster    |
| button_4  | Shoulder left front button     |
| button_5  | Shoulder right front button    |
| button_6  | Shoulder left back button      |
| button_7  | Shoulder right back button     |
| button_8  | Left button in center cluster  |
| button_9  | Right button in center cluster |
| button_10 | Left stick pressed button      |
| button_11 | Right stick pressed button     |
| button_12 | Top button in left cluster     |
| button_13 | Bottom button in left cluster  |
| button_14 | Left button in left cluster   |
| button_15 | Right button in left cluster    |
| button_16 | Vendor button 1                |
| button_17 | Vendor button 2                |

### ``axis_move``

Fired whenever a controller's axis (analog stick) is moved.

The standard button layout has four axes associated with a pair of analog sticks, one on the left and one on the right.

<br/>

## Settings

<br/>

## Testing

joypad.js uses the [jest](https://facebook.github.io/jest/) test runner. Run the following command to initiate it - 

```bash
npm test
```

<br/>

## Support

If you'd like to help support the development of the project, please consider backing me on Patreon -

[<img src="https://arunmichaeldsouza.com/img/patreon.png" width="180px;"/>](https://www.patreon.com/bePatron?u=8841116)

<br/>

## License

MIT Licensed

Copyright (c) 2019 Arun Michael Dsouza (amdsouza92@gmail.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
