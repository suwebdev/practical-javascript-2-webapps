# Handling Events in Vue.js
Events are a key part of any web-based application. The user interacts with a page by scrolling, clicking, hovering, touching, dragging, submitting forms, and more. All of these interactions can be captured. Responding to these events is a primary method we have for building reactive interfaces that help the user accomplish their goals.

As a quick recap about what events are: Many components of HTML will emit (signal, or "fire") ["events."](https://developer.mozilla.org/en-US/docs/Web/Events) Events are meant to provide a signal that something interesting has happened, and much of what we do in our coding is to create situations where responding to these built-in events becomes useful to the user. For example, when a button is clicked, a "click" event is fired. This event can be detected in our code and we can respond by doing something the user expects.

Events are "handled" by event listeners (which we will often just call "listeners"). Listeners are specific watchers we have defined to detect an event and then execute some code in response to the event. Events are happening all the time when a user interacts with a website, but if no listeners have been defined then only the default event "handlers" will be invoked. 

For example, a web browser will automatically submit a form when the form emits the `submit` event. A form could be submitted by a user pressing `enter` on their keyboard, or by clicking a button to submit the form. Regardless, the browser has a default event listener watching for that signal from any HTML forms, and it will execute code to respond to an event. 

As developers, we can also detect events and we can choose to augment or replace the default response to any event. Vue.js provides us with a range of tools for [working with events](https://vuejs.org/v2/guide/events.html). These tools make it much easier to define, manage, and execute event handling in Vue.js projects.

## Defining Event Listeners
The core directive used to define event listeners is the `v-on` directive. This directive takes an argument, which is the name of the event for which to listen. Because each HTML element can emit a different set of events, it's best to refer to a list of relevant events (such as the [Web Events page at MDN](https://developer.mozilla.org/en-US/docs/Web/Events)) to know we are using the proper event label. But much of the time we use relatively standard events in our projects (e.g. `submit`, `click`, `keydown`, `keyup`, etc.). 

Here is an example of a simple `v-on:click` listener that increments the value of a `counter` variable in the template context:

```html
<h2>Counter</h2>
<button v-on:click="counter++">Add 1</button> {{ counter }}
```

All of the logic that responds to this event is in the template here. As long as `counter` is initialized to `0` in the component's data, no other logic is required in the component to make this work. When the template loaded in a browser, it looks like this:

![Simple click event handler](/img/event-handler-click-counter.gif)
<br>Simple click event handler

This is easy enough to set up, but usually we want to do something more with our event handlers. Typically, rather than executing a simple line of code when an event is detected, we execute a component method to handle the event. Component methods can be used in many ways, and they are straightforward to add to our components.

## Component Methods
Component methods are functions that can be executed in various ways within a Vue.js component. Much of the time, these methods will be executed in response to some event that has been triggered in the system. The `v-on` directive can define a method call that will be executed in response to an event signal. Let's look at an example:

```html
<template>
  <div class="events">
    <h2>Message: {{ message }}</h2>
    <p><button v-on:click="setMessage('Danger! Danger!')">Show Danger Message.</button></p>
    <p><button v-on:click="setMessage('All Clear!')">Show All Clear Message.</button></p>
  </div>
</template>

<script>
export default {
  name: 'EventDemos',
  data () {
    return {
      message: 'Component loaded successfully.'
    }
  },
  methods: {
    setMessage: function (text) {
      this.message = text
    }
  }
}
</script>
```
In this example, there is only one variable revealed to the template: `message`. The message is initialized to a load statement, but the user can click a button to change the message. Each button has a `click` event listener defined using the `v-on` directive. When the `click` event is detected on one of the buttons it will execute the `setMessage` method. This method is a function that expects to receive some text to change the value of the `message` variable. In this example, the text is set by hand, but this text could also be provided by referencing another variable or data point.

Here is what this code looks like when displayed to the user:

![Event handler using component method](/img/event-handler-method1.gif)
<br>Event handler using component method

We can see that when the user clicks the buttons the message is changed instantly. This demonstrates the fundamental ability to use methods to respond to events. With this tool, we can make all sorts of things happen in our interfaces.

## Preventing Default Event Handling
Although we can now respond to events, there are situations when we will find ourselves fighting against the default event handling provided by the web browser. Vue.js provides us with several modifiers we can use alongside the `v-on` directive to prevent the default actions from taking place. We should keep the following modifiers in mind as we work through trickier event handling situations.

### `.prevent`
The `.prevent` modifier will prevent the default event handlers from executing when an event is triggered. This is most commonly used to prevent form submissions. If no `action` property is supplied on a `<form>` element, the browser will still refresh the page. That refresh could be enough to really interrupt our well-planned user experience. Luckily, it's easy to prevent the default form submit event from happening thanks to `.prevent`.

```html
<template>
  <div class="forms">
    <h2>Message: {{ message }}</h2>
    <form v-on:submit.prevent="handleMyForm">
      <p><label>New Message: <input v-model="newMessage" type="text"></label></p>
      <p><input type="submit"></p>
    </form>

  </div>
</template>

<script>
export default {
  name: 'FormsPractice',
  data () {
    return {
      message: 'Submit the form to change this text.',
      newMessage: ''
    }
  },
  methods: {
    handleMyForm: function () {
      this.message = this.newMessage
    }
  }
}
</script>
```
Rather than directly binding the `message` value to the form input, this example uses a component method to handle the form submission. The method is called `handleMyForm` and it changes the value of the `message` variable. Note the use of `.prevent` on the `<form>` element's event listener: This is used to prevent the browser from refreshing to submit the form. 

Here is what this example looks like to the user:



### `.stop`


## Detecting Keyboard Input

## Other Event Modifiers

## `v-on` Shorthand
If we get sick of writing `v-on:click`, we can alter our templates to use the shorthand version: `@click`. Here is an example of what one of our previous templates would look like using the shorthand.

```html
<template>
  <div class="events">
    <h2>Message: {{ message }}</h2>
    <p><button @click="setMessage('Danger! Danger!')">Show Danger Message.</button></p>
    <p><button @click="setMessage('All Clear!')">Show All Clear Message.</button></p>
  </div>
</template>
```










