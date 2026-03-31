

About functions



How to write a function


Example extract a message from an array.


About variables


How to use static variables.


About subflows


How to use a subflow.

Try it.

## Writing Functions

The Function node allows JavaScript code to be run against the messages that are passed through it.

The message is passed in as an object called msg. By convention it will have a ``msg.payload`` property containing the body of the message.

Other nodes may attach their own properties to the message, and they should be described in their documentation.


### Writing a Function

The code entered into the Function node represents the body of the function. The most simple function simply returns the message exactly as-is:

```js
// Code of the function in On Message
// implicitely return msg with payload "The most simple function"
return msg;
```

Example
1.  Drag a function node.
2.  Set name of the function **The most simple function**.
3.  Insert an inject node with message
4.  Add a debug node

<div align="center">
<figure>
  <img src="./img/MyFirstFunction.png"
     alt=" image lost : MyFirstFunction"
     width="600">
  <figcaption>The most simple function.</figcaption>
</figure>
</div>


<div align="center">
<figure>
  <img src="./img/InjectMyFirstFunction.png"
     alt=" image lost : InjectMyFirstFunction"
     width="500">
  <figcaption>Inject node "My first function".</figcaption>
</figure>
</div>

If the function returns null, then no message is passed on and the flow ends.

**The function must always return a msg object**. Returning a number or string will result in an error.

The returned message object does not need to be same object as was passed in; the function can construct a completely new object before returning it. For example:

```js
var newMsg = { payload: msg.payload.length };
return newMsg;
```

:bulb: Constructing a new message object will lose any message properties of the received message. In general, function nodes should return the message object they were passed having made any changes to its properties.

Use node.warn() to show warnings in the sidebar to help you debug. For example:

```js
node.warn("my var xyz = " + xyz);
```

See logging section below for more details.

### Multiple Outputs

The function edit dialog allows the number of outputs to be changed. If there is more than one output, an array of messages can be returned by the function to send to the outputs.

This makes it easy to write a function that sends the message to different outputs depending on some condition. For example, this function would send anything a message with payload ``"Sensor One"`` on output one, and anything else on output two.

```js
if (msg.payload === "Sensor One") {
    return [msg, null];
} else {
    node.warn("This is another sensor");
    return [null, msg];
}
```

:warning: Furthermore, a warning is added in the sidebar for debug.

<div align="center">
<figure>
  <img src="./img/FunctionWithTwoOutputs.png"
     alt=" image lost : FunctionWithTwoOutputs"
     width="500">
  <figcaption>Function with two outputs".</figcaption>
</figure>
</div>

<div align="center">
<figure>
  <img src="./img/SelectNumberOfOutputsInSetup.png"
     alt=" image lost : SelectNumberOfOutputsInSetup"
     width="500">
  <figcaption>Select number of outputs in Setup".</figcaption>
</figure>
</div>

:warning: zero or more outputs, but only one input.

The following example passes the original message as-is on the first output and a message containing the payload length is passed to the second output:

```js
var newMsg = { payload: msg.payload.length };
return [msg, newMsg];
```

#### Handling arbitrary number of outputs
:no_bell: *for information only*

node.outputCount contains the number of outputs configured for the function node.

This makes it possible to write generic functions that can handle variable number of outputs set from the edit dialog.

For example if you wish to spread incoming messages randomly between outputs, you could:

```js
// Create an array same length as there are outputs
const messages = new Array(node.outputCount)
// Choose random output number to send the message to
const chosenOutputIndex = Math.floor(Math.random() * node.outputCount);
// Send the message only to chosen output
messages[chosenOutputIndex] = msg;
// Return the array containing chosen output
return messages;
```

You can now configure number of outputs solely via edit dialog without making changes to the function itself.

#### Multiple Messages
:no_bell: *for information only*

A function can return multiple messages on an output by returning an array of messages within the returned array. When multiple messages are returned for an output, subsequent nodes will receive the messages one at a time in the order they were returned.

In the following example, msg1, msg2, msg3 will be sent to the first output. msg4 will be sent to the second output.

```js
var msg1 = { payload:"first out of output 1" };
var msg2 = { payload:"second out of output 1" };
var msg3 = { payload:"third out of output 1" };
var msg4 = { payload:"only message from output 2" };
return [ [ msg1, msg2, msg3 ], msg4 ];
```

The following example splits the received payload into individual words and returns a message for each of the words.

```js
var outputMsgs = [];
var words = msg.payload.split(" ");
for (var w in words) {
    outputMsgs.push({payload:words[w]});
}
return [ outputMsgs ];
```

#### Running code on start

The Function node provides an On Start tab where you can provide code that will run whenever the node is started. This can be used to setup any state the Function node requires.

For example, it can initialise values in local context that the main Function will use:

```js
if (context.get("counter") === undefined) {
    context.set("counter", 0)
}
```

The **On Start** function can return a Promise if it needs to complete asynchronous work before the main Function can start processing messages.

#### Logging events

If a node needs to log something to the console, it can use one of the follow functions:

-   ``node.log("Something happened");``
-   ``node.warn("Something happened you should know about");``
-   ``node.error("Oh no, something bad happened");``

#### Function reference API
:no_bell: *for information only*

The documentation above is what you need for basic applications. For more details you can have a look on the [Node-RED user guide for functions](https://nodered.org/docs/user-guide/writing-functions#writing-a-function).

-   ``node.id`` : the id of the Function node.
-   ``node.name`` : the name of the Function node.
-   ``node.outputCount`` : number of outputs set for Function node
-   ``node.log(..)`` : log a message
-   ``node.warn(..)`` : log a warning message
-   ``node.error(..)`` : log an error message
-   ``node.debug(..)`` : log a debug message
-   ``node.trace(..)`` : log a trace message
-   ``node.status(..)`` : update the node status
-   ``node.send(..)`` : send a message
-   ``node.done(..)`` : finish with a message

##### context

-   ``context.get(..)`` : get a node-scoped context property
-   ``context.set(..)`` : set a node-scoped context property

##### flow

-   ``flow.get(..)`` : get a flow-scoped context property
-   ``flow.set(..)`` : set a flow-scoped context property

##### global

-   ``global.get(..)`` : get a global-scoped context property
-   ``global.set(..)`` : set a global-scoped context property

---