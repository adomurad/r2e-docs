---
sidebar_position: 2
---

# Retrieving Details

Here are the ways to extract more information about `Elements` in the `Browser`.

## Text and value

### getText

Get **text** of the `Element`.

```elixir
# get button text
buttonText = button |> Element.getText!
```

### getValue

Get **value** of the `Element`.

When `Element` does not have a value property
then returns empty `Str`.

```elixir
# get input value
inputValue = input |> Element.getValue!
```

### getProperty

Get **property** of the `Element`.

Valid **properties** are keys that you get when using `GetOwnProperty` on the element in the browser.

Returns a `Task` of `Result a [Empty]`.

The return type `a` should be same type like in the browser.

Using with `Str` properties:

```elixir
# get input value
inputValue = input |> Element.getAttribute! "value"
# expect to have value "email@emails.com"
inputType |> Assert.shouldBe (Ok "email@emails.com")
```

Using with `Bool` properties:

```elixir
isChecked = nameInput |> Element.getProperty! "checked"
when isChecked is
    Ok value -> value |> Assert.shouldBe Bool.false
    Err Empty -> Assert.failWith "input should have a checked prop"
```

Using with `Num` properties:

```elixir
clientHeight = nameInput |> Element.getProperty! "clientHeight"
clientHeight |> Assert.shouldBe (Ok 17)
```

When checking for `[Empty]` it is a good practice to use
a type annotation - this way in case it is a value
(like a `Str`, `Bool`, etc.) the Json decoder will know how
to decode the value.

```elixir
# a div should not have the property "value"
divValue : Result Str [Err Empty]
divValue = div |> Element.getProperty! "value"
divValue |> Assert.shouldBe (Err [Empty])
```

### getAttribute

Get **attribute** of the `Element`.

**Attributes** are the values you can see
in the HTML DOM, like `<input class="test" type="password">`.

Returns a `Task` of `Result Str [Empty]`.

```elixir
# get input type
inputType = nameInput |> Element.getAttribute! "type"
inputType |> Assert.shouldBe (Ok "email")
```

## Printing

### getScreenshotBase64

Take a screenshot of a `Element`.

The result will be a **base64** encoded `Str` representation of a PNG file.

```elixir
base64PngStr = button |> Element.getScreenshotBase64!
```
