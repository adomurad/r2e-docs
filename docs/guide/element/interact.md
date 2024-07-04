---
sidebar_position: 2
---

# Interactions

Here are the ways to interact with the `Elements` in the `Browser`.

## Mouse

### click

Click on an `Element`.

```elixir
# click the button
button |> Element.click!
```

## Keyboard

### sendKeys

Send keys to an `Element` (e.g. put text into an input).

:::warning
Input text is not escaped for now.

Double quotes need to be escaped manually e.g. "my input \\"test\\""

This will probably change in the future.
:::

```elixir
# input an email into the email input
emailInput |> Element.sendKeys! "my.fake.email@fake-email.com"
```

Special keys sequences:

- `{enter}` - simulates an "enter" key press
  ```elixir
  # input text and submit
  searchInput |> Element.sendKeys! "roc lang{enter}"
  ```

### clear

Clear an editable or resettable `Element`.

```elixir
# find button element
input = browser |> Browser.findElement! (Css "#email-input")
# click the button
input |> Element.clear!
```
