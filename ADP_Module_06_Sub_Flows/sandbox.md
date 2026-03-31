

About functions



How to write a function


Example extract a message from an array.


About variables


How to use static variables.


About subflows


How to use a subflow.

Try it.

## Node-RED Variables

Global, Flow, Context & Environment Variables.

Variables are essential for building anything beyond basic message routing in Node-RED. They let you store state, share data across your application, and manage configuration—capabilities you'll need for almost any real-world project.

Node-RED provides four types of variables, each with different visibility and use cases.

### What Are Node-RED Variables?

Variables in Node-RED serve as containers for storing and managing data throughout your application. Understanding the different types and their scopes is essential for building efficient, organized flows.

Node-RED offers three primary variable categories:

**Message variables** travel with the message object as it flows through your nodes. The most common example is ``msg.payload``, which carries the primary data between nodes.

These are the variables that we have already used in previous modules, for example to display numerical values ​​via Node-RED Dashboard.

Example of an object message payload:
```js
{"ID":1001,
 "Name":"Axes Velocity",
 "Unit":"m/s",
 "Value":0.1}
```

**Context variables** store application state at different levels—**node**, **flow**, or **global** scope. They persist data that needs to be accessed across multiple message events, making them ideal for tracking counters, storing configuration, or maintaining state.



**Environment variables** handle configuration data and sensitive information like API keys and credentials. By storing this data separately from your flows, you maintain security and make configuration management more flexible.

---

#### Global Variables: Instance-Wide Data Storage

Global variables provide a centralized storage mechanism accessible throughout your entire Node-RED instance. Any function, change, inject, or switch node can read or write global variables, making them perfect for sharing data across multiple flows.

When to use global variables: Consider using them for system-wide settings, shared configuration, or data that multiple flows need to access. For example, in a home automation system with separate flows for lighting, security, and climate control, global variables can store user preferences that all flows reference.

##### Working with Global Variables

Setting global variables can be done through the change node or programmatically in a function node:

Using the change node:

1.  Select **global** from the variable type dropdown
2.  Enter your variable name
3.  Set the value or expression

<div align="center">
<figure>
  <img src="./img/BuildGlobalVariable.png"
     alt=" image lost : BuildGlobalVariable"
     width="500">
  <figcaption>Build global variable using Change Node</figcaption>
</figure>
</div>

or using a function:

```js
global.set('MyFlowFunctionObject', msg.payload);
```

##### Retrieving global variables
 follows a similar pattern:

In a change, inject, or switch node, simply set the action to **set**, choose the type as **global**, and specify the variable name.

<div align="center">
<figure>
  <img src="./img/ReadGlobalObject.png"
     alt=" image lost : ReadGlobalObject"
     width="500">
  <figcaption>Read global object with change node.</figcaption>
</figure>
</div>

:bulb: you could access directly to a variable of the global object too.

<div align="center">
<figure>
  <img src="./img/ReadGlobalObjectName.png"
     alt=" image lost : ReadGlobalObjectName"
     width="500">
  <figcaption>Read global variable from object with change node.</figcaption>
</figure>
</div>

In function nodes:

```js
const axisVelocity = global.get('MyFlowFunctionObject');
```

Deleting global variables can be accomplished through the change node by selecting **delete** from the action dropdown, or via the Context Data sidebar panel, which provides a comprehensive view of all variables.

<div align="center">
<figure>
  <img src="./img/DeleteGlobalVariable.png"
     alt=" image lost : DeleteGlobalVariable"
     width="500">
  <figcaption>Delete global variable with change node.</figcaption>
</figure>
</div>

---

#### Flow Variables / Tab-Scoped Data

Flow variables exist within a single tab or flow in your Node-RED editor. They're accessible to all nodes within that specific flow but isolated from other flows, providing logical data separation.

When to use flow variables: Use them for data that's relevant only to a specific workflow. For instance, in a temperature monitoring flow with multiple sensor nodes, flow variables can track the current reading, alert thresholds, or calculation results—data that doesn't need to be shared with other parts of your application.
Working with Flow Variables

##### Setting flow variables:

Using the change node, select the action **set**, choose **flow** as the variable type, and configure your variable.

<div align="center">
<figure>
  <img src="./img/BuildFlowObject.png"
     alt=" image lost : BuildFlowObject"
     width="500">
  <figcaption>Build flow object with change node.</figcaption>
</figure>
</div>

of with a function

```js
flow.set('MyFlowFunctionObject', msg.payload);
```

##### Retrieving flow variables

In a change, inject, or switch node, simply set the action to **set**, choose the type as **flow**, and specify the variable name.

<div align="center">
<figure>
  <img src="./img/ReadFlowObjectVariable.png"
     alt=" image lost : ReadFlowObjectVariable"
     width="500">
  <figcaption>Read flow object with change node.</figcaption>
</figure>
</div>

or with a variable:

```js
const axisVelocity = flow.get('MyFlowFunctionObject');
```

Deleting flow variables works the same way as global variables—use the change node's delete action or the Context Data panel.

<div align="center">
<figure>
  <img src="./img/DeleteFlowVariable.png"
     alt=" image lost : DeleteFlowVariable"
     width="500">
  <figcaption>Delete flow object with change node.</figcaption>
</figure>
</div>

---

#### Node Variables / Node-Level Isolation

Node variables, **also called node context**, are the most restrictive scope—they exist only within a single node. No other node can access or modify these variables, making them ideal for maintaining private state.

When to use node variables: Perfect for counters, temporary calculations, or any data that should remain private to a specific node. For example, a function node that generates unique IDs for database records can maintain a counter variable that's never exposed to other parts of your flow.

##### Working with Node Variables

Node variables are local to a Function node and **cannot be read or modified by other nodes**.

**Setting node variables**
Write that in the On Start of a function node

<div align="center">
<figure>
  <img src="./img/EditOnStartFunctionNode.png"
     alt=" image lost : EditOnStartFunctionNode"
     width="500">
  <figcaption>Edit On Start of a function node.</figcaption>
</figure>
</div>

```js
// Code added here will be run once
// whenever the node is started.
context.set('counter', 0);
```

**Retrieving node variables**
For example in a function:

```js
var _counter = context.get('counter');
_counter++;
context.set('counter', _counter);

msg.payload = _counter

return msg;
```

<div align="center">
<figure>
  <img src="./img/EditOnMessageFunctionNode.png"
     alt=" image lost : EditOnMessageFunctionNode"
     width="500">
  <figcaption>Edit On Message function node.</figcaption>
</figure>
</div>

<div align="center">
<figure>
  <img src="./img/BuildAndTestCounter.png"
     alt=" image lost : BuildAndTestCounter"
     width="500">
  <figcaption>Build and test the counter.</figcaption>
</figure>
</div>

---

#### Finally
You can use the navigation panel on the right to watch the variables.

<div align="center">
<figure>
  <img src="./img/TheContextNavigation.png"
     alt=" image lost : TheContextNavigation"
     width="500">
  <figcaption>The context navigation panel.</figcaption>
</figure>
</div>

You will need to refresh the variables to display them.

:bulb: you can delete the variables in  the navigation panel using the trash icon.

---