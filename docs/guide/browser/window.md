---
sidebar_position: 2
---

# Window Management

Here are the things you can do with the `Browser` window.

## Creating, navigating and closing

### create

Create a new `Browser` window on a blank page.

```elixir
browser = driver |> Browser.createBrowser!
```

### navigateTo

Navigate the `Browser` to the given URL.

```elixir
browser |> Browser.navigateTo! "http://roc-lang.org"
```

### navigateBack

Navigate the `Browser` back in history.

```elixir
browser |> Browser.navigateBack!
```

### navigateForward

Navigate the `Browser` forward in history.

```elixir
browser |> Browser.navigateForward!
```

### reloadPage

Reload the current `Browser` page.

```elixir
browser |> Browser.reloadPage!
```

### open

Create a new `Browser` window and navigate to the given URL.

```elixir
browser = driver |> Browser.open! "http://roc-lang.org"
```

### createBrowserWithCleanup

Create a new `Browser` window with a callback function.

When the callback function ends on either `Task.ok` or `Task.err`
the `Browser` window will be automatically closed.

```elixir
Browser.createBrowserWithCleanup driver \browser ->
    browser |> Browser.navigateTo "http://google.com"
```

### openWithCleanup

Create a new `Browser` window and navigate to the given URL
with a callback function.

When the callback function ends on either `Task.ok` or `Task.err`
the `Browser` window will be automatically closed.

```elixir
url = "http://google.com"
Browser.openWithCleanup! driver url \browser ->
    # browser opens at google.com
    # should cleanup and close the browser when not found
    el = browser |> Browser.findElement! (Css "#fake-id-abcd")
```

### close

Close the `Browser` window.

```elixir
browser |> Browser.close!
```

## Retrieve Details

### getTitle

Get browser title.

```elixir
browser |> Browser.navigateTo! "http://google.com"
# get title
title = browser |> Browser.getTitle!
# title = "Google"
```

### getUrl

Get current URL.

```elixir
browser |> Browser.navigateTo! "http://google.com"
# get url
url = browser |> Browser.getUrl!
# url = "https://google.com/"
```

## Resize and move

### setWindowRect

Set `Browser` window position and size.

- `x` - new x position
- `y` - new y position
- `width` - new width
- `height` - new height

```elixir
browser |> Browser.setWindowRect! {
    x: Some 100,
    y: Some: 100,
    width: Some 400,
    height: Some 400,
}
```

All parameters are optional.

You can set just a new position:

```elixir
browser |> Browser.setWindowRect! {
    x: Some 100,
    y: Some: 100,
}
```

Or for e.g. only the width:

```elixir
browser |> Browser.setWindowRect! {
    width: Some 400,
}
```

### setSize

Set `Browser` size.

- `width` - new width
- `height` - new height

```elixir
# set browser window size to 200x800
browser |> Browser.setSize! 200 800
```

### moveTo

Move the `Browser` window to a new x,y coordinates.

- `x` - new x
- `y` - new y

```elixir
# move to 500x400
browser |> Browser.moveTo! 500 400
```

### maximizeWindow

Maximize the `Browser` window.

This function returns new position and dimensions of the `Browser` window.

```elixir
newRect = browser |> Browser.maximizeWindow!
# newRect: { x: I32, y: I32, width: I32, height: I32 }
```

In most use cases you want to ignore the output:

```elixir
browser |> Browser.maximizeWindow!
```

### minimizeWindow

Minimize the `Browser` window.

This function returns new position and dimensions of the `Browser` window.

```elixir
newRect = browser |> Browser.minimizeWindow!
# newRect: { x: I32, y: I32, width: I32, height: I32 }
```

### fullScreenWindow

Make the `Browser` window full screen.

This function returns new position and dimensions of the `Browser` window.

```elixir
newRect = browser |> Browser.fullScreenWindow!
# newRect: { x: I32, y: I32, width: I32, height: I32 }
```

## Printing

### printPdfBase64

Print current page to PDF.

The result will be **base64** encoded `Str`.

```elixir
base64PdfStr = browser |> Browser.printPdfBase64! {}
```

You can use mostly the same options,
that are available when printing the page manually in the browser.

Here are all available options with the **default** values:

```elixir
base64PdfStr = browser |> Browser.printPdfBase64! {
    page: {
        width: 21.59, # pageWidth if orientation is "portrait" otherwise pageHeight [cm]
        height: 27.94, # pageHeight if orientation is "portrait" otherwise pageWidth [cm]
    },
    margin: { # page margins [cm]
        top: 1.0,
        bottom: 1.0,
        left: 1.0,
        right: 1.0,
    },
    scale: 1.0, # zoom the size of the content by a factor scale
    orientation: Portrait, # [Portrait, Landscape]
    shrinkToFit: Bool.true, # resize the content to match the page width
    background: Bool.false, # false = suppress output of background images and colors
    pageRanges: [], # ["1","3","5-7"] = print only pages 1,3,5,6,7
}
```

:::note
Right now using `Browser.printPdfBase64` requires the _"--linker=legacy"_ compiler flag.
:::
