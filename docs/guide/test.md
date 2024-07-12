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

## Running tests

### runTests

Run all **R2E** tests from a list.

Available options:

```elixir
TestRunnerOptions : {
    printToConsole ? Bool, # should print results to Stdout? Default: `Bool.true`
    screenshotOnFail ? Bool, # should take screenshot of test fail? Default: `Bool.true`
    # default reporters will change in the future to [Reporters.BasicHtmlReporter.reporter]
    reporters ? List ReporterDefinition, # list of reporters. Default: []
    outDir ? Str, # relative path to the test results. Default: "testResults"
    driver ? Driver.create {}, # the `Driver` connection to use for running tests
}
```

Default configuration:

```elixir
main =
    [test1, test2, test3] |> Test.runTests! {}
```

Without `Stdout`:

```elixir
main =
    tests = [test1, test2, test3]
    tests |> Test.runTests! { printToConsole: Bool.false }
```

You can return the result of this function from the `main` function
to indicate to the running _CI_ process if the
test run was a success or a failure.

```elixir
main =
    # run all tests
    Test.runTests! [test1, test2, test3] {}
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
