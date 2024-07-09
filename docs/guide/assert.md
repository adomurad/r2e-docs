---
sidebar_position: 6
---

# Assert

The `Assert` module contains functions asserting properties of `Elements` and other types.

## Browser

### urlShouldBe

Checks if the current **URL** in the `Browser` is equal to **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
browser |> Assert.urlShouldBe! "https://roc-lang.org/"
```

### titleShouldBe

Checks if the current page **title** in the `Browser` is equal to **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
browser |> Assert.titleShouldBe! "https://roc-lang.org/"
```

## Other types

### shouldBe

Checks if the **actual** value is equal to the **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
# get button text
buttonText = button |> Element.getText!
# assert text
buttonText |> Assert.shouldBe! "Roc"
```

```elixir
inputType = nameInput |> Element.getProperty! "checked"
when inputType is
    Ok value -> value |> Assert.shouldBe Bool.false
    Err Empty -> Assert.failWith "this should not happen"
```

```elixir
# Result I32 [Empty]
inputType = nameInput |> Element.getProperty! "clientHeight"
inputType |> Assert.shouldBe (Ok 17)
```

### shouldBeGreaterThan

Checks if the **actual** `Num` is greater than the **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
10 |> Assert.shouldBeGreaterThan! 5
```

### shouldBeGreaterOrEqualTo

Checks if the **actual** `Num` is greater or equal to the **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
10 |> Assert.shouldBeGreaterOrEqualTo! 5
```

### shouldBeLesserThan

Checks if the **actual** `Num` is lesser than the **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
5 |> Assert.shouldBeLesserThan! 10
```

### shouldBeLesserOrEqualTo

Checks if the **actual** `Num` is lesser or equal to the **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
5 |> Assert.shouldBeLesserOrEqualTo! 10
```

### failWith

Fails with given error message.

```elixir
Assert.failWith! "this should not happen"
```

Can be useful when in cases like:

```elixir
inputType = nameInput |> Element.getAttribute! "class"
when inputType is
    Ok _ -> Assert.failWith "this input should not have a class"
    Err Empty -> Task.ok {}
```
