# API Reference

This section extensively covers (in detail) all the APIs that are common to all native apps. Each entry in this section describes an abstract class that has several static methods.

## CurrentWindow

Methods of the `CurrentWindow` refer to the window of the caller so accessing the `close` method on the
main window closes the entire app, for instance.

### Properties

None.

### Methods

#### title

Gets/sets the current window's title.

`CurrentWindow.title([, windowName: string])`

Returns `windowName: string`.

#### clone

Clones the current window using the parent window's configurations.

`CurrentWindow.clone()`

Returns `boolean`. Default `true`.

#### close

Closes the current window.

`CurrentWindow.close()`

Returns `boolean`. Default `true`.

#### width

Gets/sets the width of the current window.

`CurrentWindow.width([, length: number])`

Returns `width` value of the current window.

#### height

Gets/sets the height of the current window.

`CurrentWindow.height([, length: number])`

Returns `height` value of the current window.

#### maxWidth

Gets/sets the maximum width of the current window.

`CurrentWindow.maxWidth([, length: number])`

Returns `maxWidth` value of the current window.

#### maxHeight

Gets/sets the maximum height of the current window.

`CurrentWindow.maxHeight([, length: number])`

Returns `maxHeight: number`.

#### minWidth

Gets/sets the minimum width of the current window.

`CurrentWindow.minWidth([, length: number])`

Returns `minWidth` value of the current window.

#### minHeight

Gets/sets the minimum height of the current window.

`CurrentWindow.minHeight([, length: number])`

Returns `minHeight` value of the current window.

#### resizable

Gets/sets resizability of the current window.

`CurrentWindow.resizable(shouldResize: boolean)`

Returns `resizable` value of the current window. Default `true`.

#### focusOnStartup

Gets/sets the whether the current window should be focused when started.

`CurrentWindow.focusOnStartup(shouldFocus: boolean)`

Returns `focusOnStartup` value of the current window.

!!! note
    This method is only available as a configuration option in a subsequent window created by <a href='/window#create'>Window.create()</a>

#### hideInTaskbar

Gets/sets whether the current window should be displayed in the taskbar.

`CurrentWindow.hideInTaskbar(shouldHideInTaskbar: boolean)`

Returns `hideInTaskbar` value of the current window. Default `false`.

#### hideOnStartup

Gets/sets whether the current window should be hidden on window startup.

`CurrentWindow.hideOnStartup(shouldHideOnStartup: boolean)`

Returns `hideOnStartup` value of the current window. Default `false`.

#### startupFromCenter

Gets/sets whether the current window should be centerized.

`CurrentWindow.startupFromCenter(shouldStartupFromCenter: boolean)`

Returns `startupFromCenter` value of the current window. Default `true`.

#### state

Gets/sets the current window state which could be one of:
* `'normal'`
* `'maximized'`
* `'minimized'`

`CurrentWindow.state(state: string)`

Returns `state` value of the current window. Default `'normal'`.

#### frameless

Gets/sets whether the current window should have no outer frame.

`CurrentWindow.frameless(shouldSetFrameless: boolean)`

Returns `frameless` value of the current window. Default `'false'`.

#### activate

Gets/sets whether the current window should be activated.

`CurrentWindow.activate(shouldActivate: boolean)`

Returns `activate` value of the current window. Default `'true'`.

#### focus

Gets/sets whether the current window should have a focus.

`CurrentWindow.focus(shouldSetFocus: boolean)`

Returns `focus` value of the current window. Default `'true'`.

#### hide

Gets/sets whether the current window should be hidden.

`CurrentWindow.hide(shouldBeHidden: boolean)`

Returns `hide` value of the current window. Default `'false'`.

#### show

Gets/sets whether the current window should be displayed once it's hidden.

`CurrentWindow.show(shouldShowAfterHide: boolean)`

Returns `show` value of the current window. Default `'true'`.

<!-- Window API -->

## Window

### Properties

None.

### Methods

#### create

Creates a new window with a new configuration.

`Window.create(newConfig: object)`

Returns `Window` (the new window created).

#### close

Closes a window with the specified `id`. This means a window 5 levels deep can close another window that is 3 levels deep, for instance. All the values of `id` are indexed starting from 1.

`Window.close(id: string)`

Returns `boolean`. Default `true`.

#### closeAll

Closes all queued windows.

`Window.closeAll()`

Returns `boolean`. Default `true`.

<!-- Menubar -->

## Menubar

The menubar is defined in the NodeJS end and is not dynamic. This means no mutations can occur on the menubar once it's set.

A simple example of a menubar:

```javascript
const { Menubar, Menu } = require('macron');

module.exports = new Menubar([
  Menu.MenuItem({
    label: "File",
    submenu: [
      Menu.MenuItem({label: "New File", click: function() {
        console.log(
          require('macron').Dialog.filePicker({
            title: 'Pick file...',
            read: true,
            initialDirectoryPath: 'C:/Users/default/Desktop/macron_tests/',
            fileTypes: [
              ['All files', '.*'],
              ['Text', '.txt'],
              ['HTML', '.html'],
              ['JavaScript', '.js'],
              ['CSS', '.css'],
              ['Markdown', '.md']
            ]
          })
        );
      }),
      Menu.MenuItem({label: "New Window"}),
      Menu.Seperator,
      Menu.MenuItem({label: "Open File"}),
      Menu.MenuItem({label: "Open Folder"}),
      Menu.Seperator,
      Menu.MenuItem({label: "Open Recent", submenu: [
        Menu.MenuItem({label: "./views/CodeEditor/index.js"}),
        Menu.MenuItem({label: "../components/windows/MenuButton"}),
        Menu.MenuItem({label: "./app/scripts/"}),
        Menu.MenuItem({label: "../static/img/logo.png"}),
        Menu.MenuItem({label: "../projects/"})
      ]}),
      Menu.Seperator,
      Menu.MenuItem({label: "Auto Save", isCheckable: true, checked: true})
    ]
  }),
  Menu.MenuItem({label: "Edit", submenu: [
    Menu.MenuItem({label: "Word Wrap", isCheckable: true, click: function(menuitem) {
      console.log(menuitem)
    }})
  ]}),
  Menu.MenuItem({label: "Selection"}),
  Menu.MenuItem({label: "View"}),
  Menu.MenuItem({label: "Go", submenu: [
    Menu.MenuItem({label: "Share", icon: "&#xE72D;"}),
    Menu.MenuItem({label: "Copy"}),
    Menu.MenuItem({label: "Delete"}),
  ]}),
  Menu.MenuItem({label: "Debug"}),
  Menu.MenuItem({label: "Tasks"}),
  Menu.MenuItem({label: "Help"})
])
```

### Menu

Acts as a container for the menu items and seperator.

### Properties

#### Menu.Seperator

Creates a menu seperator. The seperator could appear differently according to the platform.

Value `Object`.

### Methods

#### Menu.MenuItem

Creates a menu item.

Returns `Object`.

<!--
## Menubar
## Dialogs
## ContextMenu
## Process
## Platform
## Archive
## Sockets
## HTTP/HTTPS
## Mail
## FileSystem -->