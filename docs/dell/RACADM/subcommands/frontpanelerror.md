# frontpanelerror

## Description

Enables or disables the live-feed of the errors currently being displayed on the LCD screen.

For error acknowledge use hide, and error assert use show.

## Synopsis

```
racadm frontpanelerror show
racadm frontpanelerror hide
```

## Input

- `show` — To view the errors currently being displayed on the LCD screen.
- `hide` — To hide the errors currently being displayed on the LCD screen.

## Output/Example

Show the errors currently being displayed on the LCD screen.

```
racadm frontpanelerror show
Front Panel Error—Show Enabled.
```

Hide the errors currently being displayed on the LCD screen.

```
racadm frontpanelerror hide
Front Panel Error—Hide Enabled.
```