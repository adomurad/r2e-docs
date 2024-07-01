---
sidebar_position: 5
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

Checks if the **actual** `Str` is equal to the **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
# get button text
buttonText = button |> Element.getText!
# assert text
buttonText |> Assert.shouldBe! "Roc"
```

### shouldBeEqualTo

Checks if the **actual** `Num` is equal to the **expected**.

In case of fail, this function throws a `[AssertionError Str]` which will be used in the test report.

```elixir
3 |> Assert.shouldBeEqualTo! 3
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
