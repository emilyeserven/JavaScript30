[Forked from JavaScript30](https://github.com/wesbos/JavaScript30)

## Lesson Notes

### Day 1

Key Points: Playing audio, event listeners, data attributes

**Setup**

The document was pre-setup with the styling in place, as well as some HTML elements that contained some key infrastructure. Namely...

* Divs for the individual "keys"/buttons were set up and formatted properly. They also had a `data-key` attribute set with the correct [keycode](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/keyCode) value.
* Audio elements with corresponding `data-key` attributes to readily connect to the "keys".

**Part A: Playing Audio**

1. Added a `console.log` to ensure `keydown` events could be properly detected.
2. Create an [event listener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) that listens for the `keydown` event.
3. Select DOM nodes that match the criteria of `audio` element with the [attribute](https://www.w3schools.com/css/css_attribute_selectors.asp) of [`data-key`](https://www.w3schools.com/tags/att_global_data.asp). Since we're taking in the `data-key` dynamically, we use ES6 template strings.
4. A `null` is returned if there is no corresponding key. To prevent this, add an `if` statement and stop the function from running.
5. You can use [`.play()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/play) and the `audio` `const` that was just defined.
6. Because the `.play()` method won't replay a sound that's already playing, sounds won't play on every `keydown`. To bypass this, the [`currentTime`](https://www.w3schools.com/tags/av_prop_currenttime.asp) is set to 0, effectively rewinding the audio clip.

**Part B: Adding the Animation**

1. Select DOM nodes that match the criteria of the `key` class as well as the `keyCode` `data-key` attribute
2. Add the class of `playing` to items that match that criteria by using [`classList.add()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList) (this is the vanilla JS equivalent to jQuery's [`addClass`](https://api.jquery.com/addclass/)).

**Part C: Finishing the Animation**

1. Use a `forEach` statement to add an event listener to all the items selected with the query selector in the `keys` constant.
2. Since there's multiple `transitionend` events (many properties transitioned), an `if` statement is added to check and see if the property is `transform` (this is so no elements that don't transform, are left unaffected).
3. Use the `this` keyword (which is bound to the `.key` class elements now) to remove the `playing` class.

* You could technically take out the `.playing` class with JavaScript using [`setTimeout`](https://www.w3schools.com/jsref/met_win_settimeout.asp), but this is not scalable in the long run because the `setTimeout` value needs to be changed at the same time as the CSS.
* A `forEach` is used instead of an Event Listener, because event listeners can't iterate on Node lists.
* Check what `this` is equal to by just `console.log`ing it (`this` is always what's equal to what's called against it).

**Extra: Adding click functionality**

### Day 2

**Setup**

**Part A: Get Ready for Rotation**

1. Adding a [`rotate`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/rotate) to the hands makes it rotate, but on the center of the element. To fix this, use [`transform-origin`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin) to move the origin all the way to the right-hand side.
2. Set the default time to "12 o'clock" by setting a rotation right off the bat.
3. Add a [`transition`](https://developer.mozilla.org/en-US/docs/Web/CSS/transition) to make the hand actually move and not jerk around. Using a `cubic-bezier` with [`transition-timing-function`](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function) will simulate a clock hand ticking.

**Part B: Add JavaScript to Update the Hands**

1. Test that updating an element once every second will work by creating a function and using [`setInterval`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval) on it.
2. Test that seconds can be accessed correctly by using the JavaScript [`Date()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) object and the [`getSeconds()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getSeconds) method. Console.log out the seconds to ensure it's working.
3. Convert the seconds into degrees by dividing the seconds by 60 to get the percentage, then multiply that number by 360 to get the degrees the clock hand should be set to. Add 90 degrees to that to offset the initial 90 degrees.
4. Select the clock second hand by using a `querySelector` and then set the `transform` property to dynamically update via the interval function (ES6 template literals can be utilized to make this as easier job).
5. Divide by 60 for the minute degrees and divide by 12 for the hours degrees

**Part C: Fix the Hand Reverse Looping Animation**

1. Use an `if` statement to remove the transition.
