# Create an Electron JS App

```javascript 
mkdir AwesomeProject
cd /AwesomeProject
npm init
```


# Create index.html
```html 
<html>
  <head>
    <title>Hello World Application</title>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```



# Create index.js
```javascript
const { app, BrowserWindow } = require("electron");
const url = require("url");

function newApp() {
  win = new BrowserWindow();
  win.loadURL(
    url.format({
      pathname: "index.html",
      slashes: true
    })
  );
}

app.on("ready", newApp);
```





```bash
electron .
```

