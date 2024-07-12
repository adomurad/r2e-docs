---
sidebar_position: 1
---

# Driver

The `Driver` module contains functions to interact with the `Driver`.

## Creating the `Driver`

To create the driver, you use the `Driver.create` function:

```elixir
driver = Driver.create {}
```

This will create a `Driver` with connection to http://localhost:9515 (the default port when you run a webdriver locally).

When you want to connect to a different port, you can use:

```elixir
driver = Driver.create { connection: LocalServer 9514 }
```

Or you can connect to any url you want using:

```elixir
driver = Driver.create { connection: RemoteServer "http://my.internal.webdriver.com:9515" }
```

Available options:

```elixir
DriverConfiguration : {
    connection ? Connection, # connection options, Default: LocalServerWithDefaultPort
    headless ? Bool, # should run headless? Default: Bool.false
    acceptInsecureCerts ? Bool, # accept insecure certs? Default: Bool.true
}

Connection : [
    LocalServerWithDefaultPort, # http://localhost:9515
    LocalServer U8,
    RemoteServer Str,
]
```
