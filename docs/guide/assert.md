---
sidebar_position: 5
---

# Assert

The `Assert` module contains functions asserting properties of `Elements` and other types.

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
