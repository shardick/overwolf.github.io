---
id: overwolf-games-inputTracking
title: overwolf.games.inputTracking API
sidebar_label: overwolf.games.inputTracking
---

Provides keyboard and mouse activity information while the user is in-game.

## Methods Reference

* [overwolf.games.inputTracking.getActivityInformation()](#getactivityinformationcallback)
* [overwolf.games.inputTracking.getMatchActivityInformation()](#getmatchactivityinformationcallback)
* [overwolf.games.inputTracking.getMousePosition()](#getmousepositioncallback)

## Events Reference

* [overwolf.games.inputTracking.onKeyUp](#onkeyup)
* [overwolf.games.inputTracking.onKeyDown](#onkeydown)
* [overwolf.games.inputTracking.onMouseUp](#onmouseup)
* [overwolf.games.inputTracking.onMouseDown](#onmousedown)

## getActivityInformation(callback)
#### Version added: 0.92

> Returns input activity information.

Parameter | Type                  | Description                              |
--------- | ----------------------| ---------------------------------------- |
callback  | function              | Callback with input activity information |

#### Callback argument: Success

The information includes key presses and clicks for keyboard/mouse, total session time, idle time and overall actions-per-minute. This information resets between game executions.

```json
{
  "status": "success",
  "activity": {
    "mouse": {
      "total": 34,
      "dist": 18822,
      "keys": {
        "M_Right": 29,
        "M_Left": 5
      }
    },
    "keyboard": {
      "total": 0,
      "keys": {}
    },
    "aTime": 2.86,
    "iTime": 4.63,
    "apm": 12
  }
}
```

## getMatchActivityInformation(callback)
#### Version added: 0.92

> Returns input activity information (similar to [getActivityInformation()](#getactivityinformationcallback)), however, when this is supported, it will return data only for the latest match of the current game.

In order to get the information:

* The latest match must have lasted for more than 5 minutes.
* The user must have clicked more than 30 times on either keyboard or mouse.

Parameter | Type                  | Description                              |
--------- | ----------------------| ---------------------------------------- |
callback  | function              | Callback with the activity information |

#### Callback argument: Success

```json
{  
   "status":"success",
   "activity":{  
      "mouse":{  
         "total":424,
         "dist":111176,
         "keys":{  
            "M_Right":413,
            "M_Left":11
         }
      },
      "keyboard":{  
         "total":83,
         "keys":{  
            "4":1,
            "Q":20,
            "W":20,
            "E":19,
            "R":10,
            "SPACE":4,
            "LCONTROL+TAB":2,
            "TAB":2,
            "ESCAPE":2,
            "LMENU+F4":1,
            "F":1,
            "OEM_3":1
         }
      },
      "aTime":4.36,
      "iTime":1.31,
      "apm":116
   }
}
```

## getMousePosition(callback)
#### Version added: 0.93

> Returns the last mouse position in game.

The data includes the mouse position and a boolean stating whether the click was in the game or on an Overwolf widget (onGame).

Parameter | Type                  | Description                              |
--------- | ----------------------| ---------------------------------------- |
callback  | function              | Callback with the activity information |

#### Callback argument: Success

```json
{
    "status": "success",
    "mousePosition": {
        "x": 1741,
        "y": 656,
        "onGame": true,
        "handle": {
            "value": 526402
        }
    }
}
```

## onKeyUp

#### Version added: 0.78

> Fired when a keyboard key has been released.

The event information includes the virtual key code (key) and a boolean stating whether the keypress was in the game or on an Overwolf widget (onGame).

#### Event Data Example: Success

```json
{
    "key": "81",
    "onGame": true
}
```

#### Using the onKeyUp event

We will use it to catch the user's keypress release, for example, catch the tab release:

```js
overwolf.games.inputTracking.onKeyUp.addListener(function(info) {
    if(info.key == "9") //9=tab
		console.log("Tab key released: " + JSON.stringify(info));
});
```

## onKeyDown

#### Version added: 0.78

> Fired when a keyboard key has been pressed.

#### Event Data Example: Success

```json
{
    "key": "81",
    "onGame": true
}
```

#### Using the onKeyDown event

We can use it to catch the user's keypress, for example, catch the tab keypress:

```js
overwolf.games.inputTracking.onKeyDown.addListener(function(info) {
    if(info.key == "9") //9=tab
		console.log("Tab key pressed: " + JSON.stringify(info));
});
```

The event also returns a boolean stating whether that keypress happened in the game or outside of it.

Note that it's not recommended to use this method (catching user keypresses) for hotkeys.  
For that, use the [overwolf.settings.hotkeys](overwolf-settings-hotkeys) API.

## onMouseUp

#### Version added: 0.78

> Fired when a mouse key has been released.

The event information includes whether the left or white mouse button was clicked (button), x and y coordinates (x, y) and a boolean stating whether the keypress was in the game or on an Overwolf widget (onGame).

#### Event Data Example: Success

```json
{
    "button": "none",
    "x": 1002,
    "y": 821,
    "onGame": false
}
```

## onMouseDown

#### Version added: 0.78

> Fired when a mouse key has been pressed.

#### Event Data Example: Success

```json
{
    "button": "xbutton2",
    "x": 177,
    "y": 529,
    "onGame": true
}
```
