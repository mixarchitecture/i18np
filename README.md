# this repository has been moved into [cillop](https://github.com/cilloparch/cillop).

# I18n Plus

I18n Plus allows you to translate your entire application.

## Dependencies

- [github.com/BurntSushi/toml](github.com/BurntSushi/toml)
- [github.com/nicksnyder/go-i18n/v2](github.com/nicksnyder/go-i18n/v2)

## Installation

```bash
go get github.com/mixarchitecture/i18np
```

## Usage

```go
package main

import (
    "fmt"

    "github.com/mixarchitecture/i18np"
)

func main() {
 i18n := i18np.New("en") // generate a new i18n instance with fallback locale "en"
    i18n.Load("./locales", "en", "tr") // load locales from "./locales" directory for "en" and "tr" locales
    i18n.Translate("my_key") // translate "my_key" with "en" locale
    i18n.Translate("my_key", "tr") // translate "my_key" with "tr" locale
    i18n.Translate("my_key", "tr", "en") // translate "my_key" with "tr" locale, fallback to "en" locale

    i18n.TranslateWithParams("my_param_key", i18np.P{"Name": "John"}) // translate "my_param_key" with "en" locale and "Name" parameter

    err := i18n.NewError("myKey") // generate translateable error
    translatedErr := i18n.TranslateFromError(err) // translate error with "en" locale
}
```

### Bad Usage

```go
package example

func Example() error {
    return errors.New("blabla")
}
```

### Good Usage

```go
package example

import (
    "github.com/mixarchitecture/i18np"
)

func Example() *i18np.Error {
    return i18np.NewError("my_errorKey")
}

func Example2() *i18np.Error {
    return i18np.NewError("my_errorKey", i18np.P{"Name": "John"})
}
```

## Documentation

Documentation is available at [pkg.go.dev](https://pkg.go.dev/github.com/mixarchitecture/i18np).

## Contributing

Contributions are always welcome!

## License

[MIT](LICENSE)
