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
