# WebLinger.js
WebLinger.js is a library for supporting alternative
access to web page content. It is a wrapper library for
some very slick and (and large Mb) libraries that can
support head tracking and eye gaze. These sub-libraries
are dynamically loaded to help with startup time.

Camera-based, in-browser head and eye tracking is
process-intensive, so don't expect awesomoe battery
life when using these libraries.

## Documentation
```js
weblinger.start({
  source: 'head', // head, gaze, cursor
  calibration: 'default', // default, callback function
  mode: 'pointer', // pointer, joystick
  cursor: 'red_circle', // red_circle, dot, image_url
  selection_type: 'linger', // linger, expression, [keycodes], none
  selection_action: 'click', // click, callback function
  linger_duration: 1000, // ms
  linger_type: 'auto', // auto, maintain, rest
  target: 'tabbable', // tabbable, [elements], callback function
  target_highlight: 'overlay' // overlay, .css_classs
});
weblinger.stop();
```
### weblinger.start
Starts the tracking system. Note that trackers need access
to the user-facing camera. If you are planning to 
getUserMedia for an alternative camera (especially on 
mobile) you will first need to hard stop weblinger
tracking, otherwise you may have unexpected failures.

*source* - What behavior will drive the cursor. Possible
values are `head` (head tilt tracking), `gaze` (eye
gaze tracking)  or `cursor` (mouse cursor position).

*mode* - For head-tracking, specifies whether to have 
the cursor follow the current position exactly (`pointer`),
or to move the cursor gradually based on the tilt 
amount (`joystick`)

*selection_type* - What actions will trigger selection
on the page. Possible values are `linger` (required the
cursor staying on the target for `linger_duration`), 
`expression` (see `selection_expressions`), `none`,
or an array of keyCodes that can trigger selection.

*linger_type* - Specifies whether the cursor must
continue moving on the target for the entire `linger_duration`
(`maintain`), or if it just needs to get to the target
and then not leave it for the duration (`rest`)

*event_callback* - A callback method to provide 
updates on weblinger events. Most of these events can
be intercepted via the DOM if you prefer that approach,
but this data is a little more fine-grained. The first
argument will have a `type`, check out demo.html for
examples of use (including getting the video or canvas
element for rendering in the UI)

*tilt_sensitivity* - Used for head tracking in joystick
mode. 1.0 is default 0.5 is less-sensitive (more movement
required), 2.0 is
extra-sensitive (less movement required)

*joystick_speed* - Cursor speed when `mode=joystick`. Default
is 1.0

*selection_expressions* - Array of strings describing
expressions that will be used to trigger selection
when `selection_type=expression`. Possible values are
`smile`, `smirk`, `eyebrows`, `mouth-open`, `kiss`,
`blink`, `wink` (NOTE: a smile will trigger `smirk`
if `smile` is not set but `smirk` is, same with
`blink` and `wink`)

*return value*  - returns a Promise when fully initialized,
calibrated and running

### weblinger.stop
Stops the tracking. Note that trackers are typically not 
torn down because of intiailization overhead, and are  
instead paused.

*teardown* - set to true to completely tear down all trackers.
Otherwise it will just pause.

*return value*  - returns a Promise when fully stoppeed/paused

### Gotchas
Trackers leverage getUserMedia to track and analyze the
user-facing camera. If you are planning to call
getUserMedia for a different camera, you will first need
to hard stop weblinger tracking, otherwise you may
have unexpected (and hard to troubleshoot) failures -- 
especially on mobile devices.

## LICENSE

MIT

NOTE: This repo includes sub-libraries with their own 
licenses, so you must decide which you will include. They
are included here for reference purposes and because we had
to make minor tweaks to get them working together,
*but their licensing may mean they are not appropriate for your project*. Use the libraries
at your own risk.

- [JeelizWeboji](https://github.com/jeeliz/jeelizWeboji) has an Apache 2.0 license
- [webgazer.js](https://github.com/brownhci/WebGazer) has a GPLv3 license, but allows LGPLv3 for companies with a valuation < $1M