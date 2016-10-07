# sessions
sessions - just for vodka v1

# Usage

```go
package main

import (
	"github.com/insionng/vodka"
	"github.com/vodka-contrib/sessions"
)

func main() {
	e := vodka.New()
	store := sessions.NewCookieStore([]byte("123456"))
	e.Use(sessions.Sessions("vodkasession", store))
	e.Use(mw.Logger())
	e.Use(mw.Recover())

	e.Get("/", func(c *vodka.Context) error {
		session := sessions.Default(c)
		var value int
		val := session.Get("key")
		if val == nil {
			value = 0
		} else {
			value = val.(int)
			value += 1
		}
		session.Set("key", value)
		session.Save()
		return c.JSON(200, value)
	})

	e.Run(":9991")
}

```
