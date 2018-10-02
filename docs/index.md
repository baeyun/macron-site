# Getting Started

Macron is a light framework for building cross-platform desktop applications with JavaScript, HTML and CSS. It does so by creating a single thread where all static content runs alongside native modules tailored for rapid development. To learn more about Macron, check the <a href="/">homepage</a> or <a href="/">the tutorial</a>.

As far as you need to get up and running, you will only need a single configuration file to make things happen. This section will get you covered with all the basic commands to start, serve and build a full Macron application in a few simple steps.

## Installation

* `macron init [app-name]` - Create a new Macron project. Run without <code>app-name</code> to initialize in current directory.
* `macron start` - Start the application.
* `macron build` - Build a stable app (with included setup/installer).
* `macron help` - Revisit commands and further information.

## Project layout

When you run the `macron init` command, you will get a few files. The most important of these is the `macron.config.js` configuration file which we will cover in a moment. Traditionally, the general project layout is defined in the following order even though it is not necessary.

    macron.config.js                  # The configuration file
    native/                           # Included runtime modules (Python)
    public/
        index.html                    # The entry point to the application
    src/                              # All application logic and backend

## Macron configuration endpoint

After a successful initialization, `macron.config.js` is created.

``` python
import tensorflow as tf
```

!!! bug
    Refer to issue <a href="/">#871</a> for more information regarding shared
    assets in Macron applications. If the issue is confirmed to be anomalous,
    you could use the following to re-run the entire application window
    ``` javascript
    const { System } = require('macron')
    
    if (System.getPlatform() == 'MacOSX')
        if (System.getMacVersion() == 'Sierra High')
            displayMacTheme()
    ```
