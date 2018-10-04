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

The `Window` class specifically handles calls to common tasks such as creating new windows that load a different application view, closing windows using numbered IDs and closing all windows.

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

The menubar is defined in the NodeJS end and is not dynamic. This means no mutations can occur on the menubar once it's set. It is responsible for creating a single menubar before the app starts. It cannot be accessed at runtime (check <a href='#contextmenu'>ContextMenu</a>).

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
]);
```

### Menu

Acts as a container for the menu items and seperator.

### Properties

#### Menu.Seperator

Creates a menu seperator. The seperator could appear differently according to the platform.

Value: `Object`.

### Methods

#### Menu.MenuItem

Creates a menu item.

`Menu.MenuItem(itemConfig: object)`

`itemConfig` could have any of the following options:

* **label** `string` - The title of the menu item.
* **click** `function` - Handler for the item's click event. Executed in the web context only.
* **submenu** `array` - List of `Menu.MenuItem(itemConfig: object)` items to display as children. Default is `[]`.
* **isCheckable** `boolean` - Whether the item specified can be checked. Default is `false`.
* **checked** `boolean` - Whether the item specified is checked. Can only work if `itemConfig.isCheckable` is defined. Default is `false`.

Returns `Object`.

<!-- Dialogs -->

## Dialogs

The dialogs are a single entity that manipulate all sorts of native popups with a simple common API.

### Properties

None.

### Methods

#### fileSaver

Used to create a native file-saver dialog with some options. A simple example of a file saver dialog something like:

```javascript
require('macron').fileSaver({
  title: 'Save your file...', // Optional. Sets the title of the dialog window.
  name: 'build' // Required. Name of file to save.
  initialDirectoryPath: './dist/', // Required. Describes where to save the file.
  defaultExtension: 'js', // Required. Extension to use to save file.
  fileTypes: [
    ['JavaScript', '.js'],
    ['JavaScript React', '.jsx'],
  ] // Optional. Format to save file.
});
```

Returns path to saved file.

#### filePicker

Used to pick a file from a directory.

```javascript
require('macron').filePicker({
  title: 'Save your file...', // Optional. Sets the title of the dialog window.
  allowMultiPick: true // Required. Allows selection of multiple files to pick.
  initialDirectoryPath: './dist/', // Required. Describes where to save the file.
  read: false, // Optional. Whether this method should return the file contents of the picked file(s). Default false.
  fileTypes: [
    ['JavaScript, (*.js, *.htc)'],
    ['JavaScript React (*.jsx)']
  ] // Optional. Format to save file.
});
```

Returns the path to the picked file. This path could then be used for other functionalities like reading a file to be displayed in an editor, etc.

#### directoryPicker

Used to pick a directory.

```javascript
require('macron').directoryPicker({
  title: 'Select a path', // Optional. Sets the title of the dialog window
  initialDirectoryPath: './dist/', // Required. Describes where to pick the directory from.
});
```

Returns the path to the selected directory.

<!-- ContextMenu -->

## ContextMenu

The `ContextMenu` class is dynamic and can be accessed/mutated at runtime. The API is exactly the same as the <a href='#menubar'>Menubar API</a> but the only difference is that `ContextMenu` can be overidden at any moment in the web context.

### Example

```javascript
require('macron').ContextMenu.register('#editor-body', [
  Menu.MenuItem({label: "Simple Item"}),
  Menu.MenuItem({label: "Auto Save", isCheckable: true, checked: true})
]);
```

### Properties

None.

### Methods

#### register

`ContextMenu.register(queryString: string, menuItems: array)`

Registers a new `ContextMenu` instance on the DOM element with the specified `queryString`. This overrides the element's default context menu bound to the right click (if it does) and instantiates a context menu over the element.

Returns the same `ContextMenu` instance.

<!-- System -->

## System

Contains information about the underlying machine's platform, architecture, build version, processor, release and other related information.

### Properties

None

### Methods

#### getPlatform

Returns the platform the user's machine is running on or `null`. This could be one of:

* `'Windows'`
* `'Linux'`
* `'MacOSX'`

#### getMachineVersion

Returns the version of the platform the user's machine is running on or `null`.

#### getMachineType

Returns the the user's machine type.

#### getNetworkName

Returns the network name of the computer. Not to be confused with NodeJS.

#### getProcessorName

Returns the platform's processor name.

#### getRelease

Returns the platform's release.

#### javaVersion

Returns the version interface for Java platforms

!!! warning
    This method is expected to be deprecated in future versions since Macron is not expecting to support Java platforms.

#### win32Version

Provides extra information on the Windows Registry.

Returns an array of:

* OS release
* Version number
* CSD level (service pack)
* OS type (single/multi processor)

#### macVersion

Returns version of MacOS on the user's computer.

#### libcVersion

Returns version of Linux on the user's computer.

<!-- FileSystem -->

## FileSystem

The `FileSystem` API extensively covers all the needs for rapid file prototyping. Common methods for reading, writing, updating, searching, copying and replacing files are defined. However, more intricate functionalities such as file watching are omitted to avoid unnecessary side effects to the general performance.

!!! note
    Even so, these functionalities are available as plugins. Plugins are expected to make their way to Macron
    in the coming versions.

### Properties

None

### Methods

!!! note
    All `FileSystem` methods are synchronous. You could create an asynchronous wrapper over the `FileSystem` class to gain non-blocking I/O.

#### readFile

`readFile(path: string)`

Reads a file's contents and returns it.

#### writeFile

Write contents to a file.

`writeFile(path: string, contents: string)`

Returns `void`

#### appendFile

Append contents to a file.

`appendFile(path: string, contents: string)`

Returns `void`

#### clearFile

Clear contents of a file.

`clearFile(path: string)`

Returns `boolean`.

#### copyFile

Copy file from a directory to another directory.

`copyFile(src: string, to: string)`

Returns `void`

#### isFile

Checks if the specified path is a file and returns `true` if the path is a file otherwise `false`.

`isFile(path: string)`

Returns `boolean`.

#### isDirectory

Checks if the specified path is a directory and returns `true` if the path is a directory otherwise `false`.

`isDirectory(path: string)`

Returns `boolean`.

#### mkdir

Creates a directory if the specified path does not exist.

`mkdir(path: string)`

Returns `boolean`.

#### chdir

Changes working directory into specified path.

`chdir(path: string)`

Returns `boolean`.

#### realpath

Gets the absolute path of the specified path (usually a relative path).

`isFile(path: string)`

Returns `string` or `null`.

#### rename

Renames a file to a specified new name.

`rename(oldName: string, newName: string)`

Returns `void`.

#### unlink

Removes specified file.

`unlink(path: string)`

Returns `void`.

#### rmdir

Removes directory (with contents).

`rmdir(path: string)`

Returns `void`.

#### rmdirEmpty

Removes directory if it is empty.

`rmdirEmpty(path: string)`

Returns `void`.

#### readDir

Reads contents of directory.

`readDir(path: string)`

Returns `array`.

#### readDirGlob

Read contents of directory with advanced Unix file patterns. For instance:

* `'*.js'` - Matches all files that have a .*js* extension.
* `'/macron/*.cpp'` - Matches all files that have a .*cpp* extension in a `macron` folder.

`readDirGlob(path: string, pattern: string)`

Returns `array`.

<!--
## Process
## Archive
## Sockets
## HTTP/HTTPS
## Mail
## FileSystem -->