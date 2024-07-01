---
sidebar_position: 3
---

# Finding Elements

Here are the ways to find `Element` in the `Browser`.

## Finding Elements

### findElement

Find an `Element` in the `Browser`.

When there is more than 1 element, then the first will be returned.

```elixir
# find the html element with a css selector "#my-id"
button = browser |> Browser.findElement! (Css "#my-id")
```

See supported locators at [Locators](#locators).

### findElements

Find many `Element` in the `Browser`.

When there are no elements found, then the list will be empty.

```elixir
# find all <li> elements in #my-list
listItems = browser |> Browser.findElements! (Css "#my-list li")
```

See supported locators at [Locators](#locators).

### tryFindElement

Try to find an `Element` in the `Browser`.

This function returns a `[Found Element, NotFound]` instead of an error
when the element is not found.

When there is more than 1 element, then the first will be returned.

```elixir
maybeButton = browser |> Browser.tryFindElement! (Css "#submit-button")

when maybeButton is
    NotFound -> Stdout.line! "Button not found"
    Found el ->
        buttonText = el |> Element.getText!
        Stdout.line! "Button found with text: $(buttonText)"
```

See supported locators at [Locators](#locators).

## Locators

All functions that require a `Locator` can use any of the following `Locators`.

### Css

Find by **css selector**.

```elixir
# find the html element with a css selector "#my-id"
button = browser |> Browser.findElement! (Css "#my-id")
```

```elixir
# find the html element with a css selector ".my-class"
button = browser |> Browser.findElement! (Css ".my-class")
```

### TestId

Find by the **\[data-testid\]** attribute.

```elixir
# find the html element with an attribute [data-testid="my-element"]
button = browser |> Browser.findElement! (TestId "my-element")
```

### XPath

Find by **XPath**.

```elixir
# find a html element by XPath.
button = browser |> Browser.findElement! (XPath "/bookstore/book[price>35]/price")
```
