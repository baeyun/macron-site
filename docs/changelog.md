# Changelog

``` javascript
const { System } = require('macron')

if (System.getPlatform() == 'MacOSX')
    if (System.getMacVersion() == 'Sierra High')
        displayMacTheme()
```