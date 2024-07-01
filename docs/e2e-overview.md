---
sidebar_position: 3
---

# E2E Framework Overview

When using **R2E** as a E2E framework, you don't have to worry about
creating and closing the browser window.

You just run all your tests and get the results.

Here is an example with 2 tests:

```elixir title="main.roc
app [main] {
   pf: platform "https://github.com/roc-lang/basic-cli/releases/download/0.11.0/SY4WWMhWQ9NvQgvIthcv15AUeA7rAIJHAHgiaSHGhdY.tar.br",
   json: "https://github.com/lukewilliamboswell/roc-json/releases/download/0.10.0/KbIfTNbxShRX1A1FgXei1SpO5Jn8sgP6HP6PXbi-xyA.tar.br",
   r2e: "https://github.com/adomurad/r2e/releases/download/v0.1.3-alpha/7bd2vEo0xTR0rti7dVewUe1Idp_oHEWMcBIE1DeSq9A.tar.br",
}


import pf.Stdout
import pf.Task
import r2e.Test exposing [test]
import r2e.Browser
import r2e.Element
import r2e.Assert


main =
   Stdout.line! "Starting test suite!"

   tests = [test1, test2]

   # run all tests
   results = Test.runAllTests! tests
   # print results to Stdout
   Test.printResults! results
   # return an exit code for the cli
   results |> Test.getResultCode


test1 = test "check roc header" \browser ->
   # go to roc-lang.org
   browser |> Browser.navigateTo! "http://roc-lang.org"
   # find header text
   header = browser |> Browser.findElement! (Css "#homepage-h1")
   # get header text
   headerText = header |> Element.getText!
   # check text
   headerText |> Assert.shouldBe "Roc"


test2 = test "use roc repl" \browser ->
   # go to roc-lang.org
   browser |> Browser.navigateTo! "http://roc-lang.org"
   # find repl input
   replInput = browser |> Browser.findElement! (Css "#source-input")
   # send keys to repl
   replInput |> Element.sendKeys! "0.1+0.2{enter}"
   # find repl output element
   outputEl = browser |> Browser.findElement! (Css ".output")
   # get output text
   outputText = outputEl |> Element.getText!
   # assert text - fail for demo purpose
   outputText |> Assert.shouldBe "0.3000000001 : Frac *"
```

When you run this example 1 test should succeed and 1 test should fail.
The output should look like this:

```sh
➜ roc ./main.roc
Starting test suite!
Results:
Test 0: "check roc header": OK
// error
Test 1: "use roc repl": AssertionError: Expected "0.3 : Frac *" to be "0.3000000001 : Frac *"

// error
Total:  2
// error
Pass:   1
// error
Fail:   1
Test run failed
```

:::note
This example will try to use the webdriver running on "http://localhost:9515".

If you want to use different webdriver configuration, the see [this](#).
:::

## main

The main function is simple.

1.  First you run all tests sequentially by using:

    ```elixir
    results = Test.runAllTests! tests
    ```

1.  Then you can print the results to `Stdout` by using:

    ```elixir
    Test.printResults! results
    ```

    :::tip
    If you are interested in different report formats like **HTML**, **JSON**, **JUnit XML**, etc.
    then checkout the [Reporting](#) section.
    :::

1.  And if you are running this in a automated pipeline and you want
    the pipeline to fail in case of any errors, then you can get and return
    the exit code:

    ```elixir
    results |> Test.getResultCode
    ```

    :::warning
    When your run:

    ```sh
    roc ./main.roc
    ```

    Then the output of this execution will always be a "0" - success.

    When you run tests in a pipeline like "github action", it is better to build the test suite and then run it directly.
    This way in case of any tests fails the whole pipeline will fail.

    ```sh
    roc build ./main.roc

    ./main
    ```

    :::

## tests

### Defining tests

Each test is defined by using the `Test.test` function:

```elixir
import r2e.Test exposing [test]

test1 = test "check roc header" \browser ->
    # test body
```

The first argument is the test name - it will be used in reports.

The second argument is a callback function that will be the test body.
The callback gives you a `Browser` object that can be used to interact with the browser.
After the test, in case of either success or failure the browser will be closed.

### Interacting with the `Browser`

You can use the `Browser` module to interact with the browser.

To **navigate** the browser to a url, use:

```elixir
browser |> Browser.navigateTo! "http://roc-lang.org"
```

To find `Elements` in the `Browser`, use:

```elixir
replInput = browser |> Browser.findElement! (Css "#source-input")
```

To learn more interactions you can do with the `Browser`, goto the [Browser Guide](#).

### Interacting with the `Elements`

You can use the `Element` module to interact with the found `Elements`.

You can get **text** from an element by using:

```elixir
headerText = header |> Element.getText!
```

You can _type into_ inputs by sending keys:

```elixir
replInput |> Element.sendKeys! "0.1+0.2{enter}"
```

:::note
By using the **"\{enter\}"** snippet, you can simulate the **enter** key press in the input.
:::

To learn more interactions you can do with the `Elements`, goto the [Element Guide](#).

### Making `Assertions`

You can make `Assertions` by using the `Assert` module.

To check if a `Str` is equal to an expected value, you can use:

```elixir
outputText |> Assert.shouldBe "0.3000000001 : Frac *"
```

:::note
This assertion will fail!

In [Roc](https://www.roc-lang.org/) **_0.1 + 0.2_** is exactly **_0.3_**
:::

To learn more about `Assertions`, goto the [Assertion Guide](#).
