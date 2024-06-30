---
sidebar_position: 6
---

# Congratulations!

You have just learned the **basics of Docusaurus** and made some changes to the **initial template**.

Docusaurus has **much more to offer**!

Have **5 more minutes**? Take a look at **[versioning](../tutorial-extras/manage-docs-versions.md)** and **[i18n](../tutorial-extras/translate-your-site.md)**.

Anything **unclear** or **buggy** in this tutorial? [Please report it!](https://github.com/facebook/docusaurus/discussions/4610)

```elixir title="Example.roc"
app [main] {
    pf: platform "https://github.com/roc-lang/basic-cli/releases/download/0.11.0/SY4WWMhWQ9NvQgvIthcv15AUeA7rAIJHAHgiaSHGhdY.tar.br",
    json: "https://github.com/lukewilliamboswell/roc-json/releases/download/0.10.0/KbIfTNbxShRX1A1FgXei1SpO5Jn8sgP6HP6PXbi-xyA.tar.br",
    r2e: "../package/main.roc",
}

import pf.Stdout
import pf.Task
import r2e.Browser
import r2e.Element
import r2e.Test exposing [test]
import r2e.Assert

main : Task.Task {} _
main =
    tests = [test1, test2, test3, test4, test5, test6]

    results = Test.runAllTests! tests
    Test.printResults! results

test1 = test "Find by Css" \browser ->
    browser |> Browser.navigateTo! "https://devexpress.github.io/testcafe/example/"
    button = browser |> Browser.findElement! (Css "#submit-button")
    buttonText = button |> Element.getText!
    Stdout.line! "Button text is: $(buttonText)"

test2 = test "Find by XPath" \browser ->
    browser |> Browser.navigateTo! "https://devexpress.github.io/testcafe/example/"
    button = browser |> Browser.findElement! (XPath "//*[@id=\"submit-button\"]")
    buttonText = button |> Element.getText!
    Stdout.line! "Button text is: $(buttonText)"

test3 = test "Find by TestId" \browser ->
    browser |> Browser.navigateTo! "https://devexpress.github.io/testcafe/example/"
    button = browser |> Browser.findElement! (TestId "populate-button")
    buttonText = button |> Element.getText!
    # TODO getValue
    Stdout.line! "Button text is: $(buttonText)"

test4 = test "Try find element - Found" \browser ->
    browser |> Browser.navigateTo! "https://devexpress.github.io/testcafe/example/"
    maybeButton = browser |> Browser.tryFindElement! (Css "#submit-button")

    when maybeButton is
        NotFound -> Stdout.line! "Button not found"
        Found el ->
            buttonText = el |> Element.getText!
            Stdout.line! "Button found with text: $(buttonText)"

test5 = test "Try find element - NotFound" \browser ->
    browser |> Browser.navigateTo! "https://devexpress.github.io/testcafe/example/"
    maybeButton = browser |> Browser.tryFindElement! (Css "#fake-id-fake-abcd")

    when maybeButton is
        NotFound -> Stdout.line! "Button not found"
        Found el ->
            buttonText = el |> Element.getText!
            Stdout.line! "Button found with text: $(buttonText)"

test6 = test "Find many elements" \browser ->
    browser |> Browser.navigateTo! "https://devexpress.github.io/testcafe/example/"
    optionElements = browser |> Browser.findElements! (Css "option")
    optionElements |> List.len |> Num.toStr |> Assert.shouldBe "3"
```

## What's next?

- Read the [official documentation](https://docusaurus.io/)
- Modify your site configuration with [`docusaurus.config.js`](https://docusaurus.io/docs/api/docusaurus-config)
- Add navbar and footer items with [`themeConfig`](https://docusaurus.io/docs/api/themes/configuration)
- Add a custom [Design and Layout](https://docusaurus.io/docs/styling-layout)
- Add a [search bar](https://docusaurus.io/docs/search)
- Find inspirations in the [Docusaurus showcase](https://docusaurus.io/showcase)
- Get involved in the [Docusaurus Community](https://docusaurus.io/community/support)
