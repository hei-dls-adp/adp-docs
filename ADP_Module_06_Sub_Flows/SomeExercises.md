<h1>
  <img src="./img/hei-en.png" alt="HEI-Vs Logo" width="350">
  <br> Node-RED flows
    <h2>Flow Based Programming</h2>
  <br>
</h1>

Author: [Cédric Lenoir](mailto:cedric.lenoir@hevs.ch)

# Some exercises for Module 06




## Exercise one / 1.
Use the default environment variable **NR_FLOW_NAME** to display the name of any flow in the debug panel.

---

A 

Les trucs à essayer.

- Mettre un UI dans un SubFlow.
- 


### Font-size and color

```js

msg.ui_update = {};
let variable = flow.get("variable");

switch(env.get("prio")){
    case "prio1":
    msg.ui_update.fontSize = 20;
    msg.ui_update.color = "black";
    break;
    case "prio2":
    msg.ui_update.fontSize = 16;
    msg.ui_update.color = "black";
    break;
    case "prio3":
    msg.ui_update.fontSize = 16;
    msg.ui_update.color = "#717171"
    break;
}

if(global.get("language")== "en"){
    msg.payload = variable.Metadata.NomEnglish;
}else if(global.get("language")== "fr"){
    msg.payload = variable.Metadata.Nom;
}
return msg;
```

```js
msg.topic = env.get("Variable") +".Metadata"
return msg;
```

### Label

```js
msg.ui_update = {};
if (global.get("language")=="en"){
    msg.ui_update.label = "Set current flow value to max"
} else if (global.get("language") == "fr"){
    msg.ui_update.label = "Set valeur actuel sur le maximum";
}
delete msg.payload;
return msg;
```

### Set language

```js
msg.ui_update = {};
if (global.get("language")=="en"){
    msg.ui_update.label = "Reset to default value"
} else if (global.get("language") == "fr"){
    msg.ui_update.label = "Réinitialiser valeur max";
}
delete msg.payload;
return msg;
```