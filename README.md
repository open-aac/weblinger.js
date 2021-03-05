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
```
weblinger.start({
  ...opts
});
weblinger.stop();
```
### weblinger.start
Starts the tracking system. Note that trackers need access
to the user-facing camera. If you are planning to 
getUserMedia for an alternative camera (especially on 
mobile) you will first need to hard stop weblinger
tracking, otherwise you may have unexpected failures.

*option* - does some things

*option* - does some things

*option* - does some things

*return value*  - returns a Promise

### weblinger.stop
Stops the tracking. Note that trackers are typically not 
torn down because of intiailization overhead, and are  
instead paused.

*teardown* - set to true to completely tear down all trackers.

*return value*  - returns a Promise

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
are included here for reference purposes and because the 
way they are used in this repo should be acceptable,
*but it may not be for your project*. Use the libraries
at your own risk.

- [JeelizWeboji](https://github.com/jeeliz/jeelizWeboji) has an Apache 2.0 license
- [webgazer.js](https://github.com/brownhci/WebGazer) has a GPLv3 license, but allows LGPLv3 for companies with a valuation < $1M