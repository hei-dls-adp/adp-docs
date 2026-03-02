<h1>
  <img src="./img/hei-en.png" alt="HEI-Vs Logo" width="350">
  <br> Node-RED flows
    <h2>Flow Based Programming</h2>
  <br>
</h1>

Author: [Cédric Lenoir](mailto:cedric.lenoir@hevs.ch)


## Table of Contents

- [How to start a flow ?](#how-to-start-a-flow-)
  - [Default](#default)
  - [What always works on PC](#what-always-works-on-pc)
  - [What I recommend](#what-i-recommend)
  - [Other alternative](#other-alternative)
- [Option](#option)

# How to start a flow ?

When writing this course, we have experienced many issues to start Node-RED with the right flow.

## Default

By default, when starting ``node-red`` from the command line of windows.

He launches, if it exists, the flow which is located here: ``C:\Users\first_name.last_name\.node-red``.

While this works perfectly from your PC or Mac, **it poses a problem on the lab PCs because certain user rights are restricted**.

If you want to launch a new flow from this directory, you can overwrite the old flow with a new one. This isn't ideal.

## What always works on PC
- Especially on lab PCs, launch Node-RED from the Node.js console.
- Windows key, type node.js.
- Click on Node.js command prompt.

If you want to launch a flow located in a specific location:

- In Node.js, select the directory where your `flow.js` file is located.

- For example: ``cd C:\Users\first_name.last_name\Documents``.

- Type: ``node-red``.

---

## What I recommend
The simplest way, especially for launching a flow that was loaded from Git, is to launch the flow using Node.js from its location in the Git directory.

:bulb: *You can copy/paste the path from the file exporer*.

For example: if the flow is located in a Git directory: 
-   Start Node.js ``C:\Users\first_name.last_name>``
-   ``> cd C:\Users\first_name.last_name\Documents\GitHub @ HEVS\adp-lab-01_2026\node_red_base``.
-   ``...>node-red``.

---

## Other alternative
You could decide to write a batch file.
-   Create a text file with extension ``.bat``.
-   Edit the file with the a text as if it was a command line, change directory, command.
-   Save the file

```bat
> cd C:\Users\first_name.last_name\Documents\GitHub @ HEVS\adp-lab-01_2026\node_red_base
> node-red
```

-    With a double-click on the icon of the batch file, you will execute the commands in it.

# Option
You could decide, on your PC, to run Node.js and node-red in a docker. See: [Running under Docker](https://nodered.org/docs/getting-started/docker).

<!-- End of README.md -->