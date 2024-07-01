---
sidebar_position: 4
---

# Test

The `Test` module contains functions for creating and running tests in the E2E mode.

## Creating tests

### test

Create a **R2E** test with basic `Driver` configuration - targeting http://localhost:9515.

The **name** parameter will be used to identify the test in the results.

```elixir
import Test exposing [test]

myTest = test "open roc-lang.org website" \browser ->
    # open roc-lang.org
    browser |> Browser.navigateTo! "http://roc-lang.org"
```

### customTest

Create a custom `test` function.

Use this instead of the [test](#test-1) function when you want to use a different [driver configuration](driver).

```elixir
driver = Driver.create { connection: RemoteServer "http://my.webdriver.hub.com:9515" }
test = Test.customTest

myTest = test "open roc-lang.org website" \browser ->
    # open roc-lang.org
    browser |> Browser.navigateTo! "http://roc-lang.org"
```

## Running tests

### runTest

Run a single **R2E** test.

```elixir
import Test exposing [test]

main =
    testResult = Test.runTest! myTest
    Test.printResults! [testResult]

myTest = test "open roc-lang.org website" \browser ->
    # open roc-lang.org
    browser |> Browser.navigateTo! "http://roc-lang.org"
```

### runAllTests

Run all **R2E** tests from a list.

```elixir
main =
    testResults = Test.runAllTests! [test1, test2, test3]
    Test.printResults! testResults
```

### getResultCode

Get the result code from test results.

You can return this code from the `main` function
to indicate to the running _CI_ process if the
test run was a success or a failure.

```elixir
main =
    # run all tests
    testResults = Test.runAllTests! [test1, test2, test3]
    # print results to Stdout
    Test.printResults! testResults
    # return an exit code for the cli
    testResults |> Test.getResultCode
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

## Reporting

Here are the ways to convert the test results into something else.

### printResults

Print **R2E** test results to `Stdout`.

```elixir
main =
    # run all tests
    testResults = Test.runAllTests! [test1, test2]
    # print results to Stdout
    Test.printResults! testResults
```

This is how to expect when running **2** tests (1 success and 1 fail):

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
```
