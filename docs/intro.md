---
sidebar_position: 1
---

# What is R2E?

**R2E** is a End2End UI testing library for the [Roc](https://www.roc-lang.org/) language.

You can use **R2E** to in 2 main ways:

- writing End2End UI tests
- directly controlling the browser/browsers

## How does it work?

**R2E** is a using a rest client for the [webdriver](https://www.selenium.dev/documentation/webdriver/).

You will need to download a web driver or use an already available to you webdriver server.

More info on the [setup](./setup) page.

## Is this ready to use on production?

No!

:::warning

The **R2E** package is importing the [basic-cli](https://github.com/roc-lang/basic-cli) platform.

```elixir
package [
    Browser,
    Element,
    Driver,
    Assert,
] {
    pf: "https://github.com/roc-lang/basic-cli/releases/download/0.11.0/SY4WWMhWQ9NvQgvIthcv15AUeA7rAIJHAHgiaSHGhdY.tar.br",
    json: "https://github.com/lukewilliamboswell/roc-json/releases/download/0.10.0/KbIfTNbxShRX1A1FgXei1SpO5Jn8sgP6HP6PXbi-xyA.tar.br",
}
```

This is necessary, because this package has to use `Task` and `Http` module to make http calls to communicate with the webdriver.

Right now, this does work and all the examples in this documentation should work without any problems.

But this should not be possible in Roc and sooner or later this will be blocked in the compiler ([Issue #6850](https://github.com/roc-lang/roc/issues/6850)).
In this case this package will **stop working**!.

This package will be stable and will get a **1.0.0** release when the [module params proposal](https://docs.google.com/document/d/110MwQi7Dpo1Y69ECFXyyvDWzF4OYv1BLojIm08qDTvg/edit#heading=h.cxx7dzgwu0ye) will be implemented in Roc.

So for now you have to use the exact same version of [basic-cli](https://github.com/roc-lang/basic-cli) platform as used in the examples _(At least I think so...)_

[basic-cli 0.11.0](https://github.com/roc-lang/basic-cli/releases/tag/0.11.0)

:::

## Why does this online documentation exist?

Unfortunately I'am not able to generate `roc docs` for this package yet due to the [problem described above](#is-this-ready-to-use-on-production).

This documentation site is temporary.
