---
sidebar_position: 5
---

# Reporting

**Reporters** can write the test results into files in many different formats.

## Creating reporters

### createReporter

Create a custom `Reporters`.

```elixir
customReporter = Reporting.createReporter "myCustomReporter" \results ->
    lenStr = results |> List.len |> Num.toStr
    indexFile = { filePath: "index.html", content: "<h3>Test count: $(lenStr)</h3>" }
    testFile = { filePath: "test.txt", content: "this is just a test" }

    [indexFile, testFile]


tests |> Test.runAllTests { reporters: [customReporter] }
```

The reporter will create 2 files `index.html` and `test.txt` in a directory
named _"myCustomReporter"_ in the default test results directory _"testResults"_:

- ./testResults/myCustomReporter/index.html
- ./testResults/myCustomReporter/test.txt

The `results` parameter is a `List` of test results, you can find there error messages, screenshots, etc.

## Builtin reporters

**R2E** has couple of builtin reporters.

### BasicHtmlReporter

The `BasicHtmlReporter` create a single **html** file with the whole report.

```elixir
tests |> Test.runAllTests { reporters: [Reporting.BasicHtmlReporter.reporter] }
```

Will create an html file that looks like this:

![TODO](#)

:::warning
Right now, due to a compiler error, by default there are no reporters used.

But in future (when I'm able to compile the code) `BasicHtmlReporter` will be the default reporter.
:::
