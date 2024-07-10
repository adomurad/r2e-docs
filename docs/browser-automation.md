---
sidebar_position: 4
---

# Browser Automation Overview

You can use **R2E** not only for writing tests, but also to just interact with the browser.

The most common use cases are:

- data extraction from pages
- automating a form submission process
- speed testing (recording loading times)
- web crawling
- printing a PDF from a website _(not implemented yet)_
- printing a PDF from HTML _(not implemented yet)_

## Example

This is an example program, that will:

- open 2 browser windows
- move and resize them
- navigate both browsers to different urls
- close both browsers

```elixir title="main.roc"
app [main] {
   pf: platform "https://github.com/roc-lang/basic-cli/releases/download/0.11.0/SY4WWMhWQ9NvQgvIthcv15AUeA7rAIJHAHgiaSHGhdY.tar.br",
   json: "https://github.com/lukewilliamboswell/roc-json/releases/download/0.10.0/KbIfTNbxShRX1A1FgXei1SpO5Jn8sgP6HP6PXbi-xyA.tar.br",
   r2e: "https://github.com/adomurad/r2e/releases/download/v0.1.8-alpha/GAvOhHDCkE5MrD614geTEZDg9KJ1BbUnrUcuCUo1HgU.tar.br",
}


import pf.Task
import r2e.Browser
import r2e.Driver


main =
   # create a driver client for http://localhost:9515
   driver = Driver.create {}

   # create 2 browser windows
   browser1 = Browser.createBrowser! driver
   browser2 = Browser.createBrowser! driver

   # move and resize browser 1
   browser1 |> Browser.setSize! 200 200
   browser1 |> Browser.moveTo! 0 0

   # move and resize browser 2
   browser2 |> Browser.setSize! 200 200
   browser2 |> Browser.moveTo! 200 200

   # navigate browser1 to basic-cli
   browser1 |> Browser.navigateTo! "https://www.roc-lang.org/packages/basic-cli/"
   # navigate browser2 to basic-webserver
   browser2 |> Browser.navigateTo! "https://roc-lang.github.io/basic-webserver/"

   # close browser1
   browser1 |> Browser.close!
   # close browser2
   browser2 |> Browser.close!
```

:::note
This example will try to use the webdriver running on "http://localhost:9515".

If you want to use different webdriver configuration, then see [this](guide/driver).
:::

### Creating a browser window

This example creates a browser window, and then navigates to an URL:

```elixir
browser1 = Browser.createBrowser! driver
browser1 |> Browser.navigateTo! "https://www.roc-lang.org/packages/basic-cli/"
```

But you can create and navigate using one function:

```elixir
# creates a new browser and navigate to URL
browser1 |> Browser.open! driver "https://www.roc-lang.org/packages/basic-cli/"
```

To learn more interactions you can do with the `Browser`, goto the [Browser Guide](guide/browser/intro).

### Browser cleanup

When any step fails, the program terminates without closing the browser.

There are many functions that will cleanup and close the browser for you no matter
if everything will be ok, or something will terminate the program early with an error.

```elixir
Browser.createBrowserWithCleanup driver \browser ->
    browser |> Browser.navigateTo "http://google.com"
```

To learn more cleanup `Browser` functions, goto the [Browser Cleanup Guide](guide/browser/window#creating-navigating-and-closing).
