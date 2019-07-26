This project is a Go client to access the Nokotime API V2.
[![GoDoc](https://godoc.org/github.com/gertv/go-Nokotime?status.svg)](https://godoc.org/github.com/gertv/go-Nokotime)


Getting started
---------------

First, grab a copy of the client code

    go get github.com/gertv/go-noko

Before you start using the Go client, you should have these
two bits of information at hand:
* your Nokotime account subdomain
* a valid token for accessing the API V2.

Once you import the package, you can start using the API
through the `Nokotime(domain, token string)` function.

A minimal example of a command-line program that uses the
client would look like this:

```Go
package main

import (
  "github.com/gertv/go-noko"
)

func main() {
  f := noko.Nokotime("mycompany", "MyNokotimeAPIV2Token")

  // once you have the Nokotime object, just start using the API
  // through one of the ...API() functions
  f.EntriesAPI().ListEntries()
}
```

Tips and tricks
---------------

#### Google Appengine

If you're using this on Google's AppEngine, you also need to configure the `appengine/urlfetch` HTTP Client.
```Go
package main

import (
  "appengine"
  "appengine/urlfetch"
  "http"
 
  "github.com/gertv/go-noko"
)

func handler(w http.ResponseWriter, r *http.Request) {
  c := appengine.NewContext(r)
  
  f := noko.Nokotime("mycompany", "MyNokotimeAPIV2Token")
  // this line configure the Nokotime client to use the urlfetch HTTP client
  f.Client(urlfetch.Client(c))

  // once you have the Nokotime object, just start using the API
  // through one of the ...API() functions
  f.EntriesAPI().ListEntries()
}
```


TODO
----

There's still some work to be done:

* Implement the other available resources of the V2 API
  * Timers
  * Expenses
  * Project Groups
  * ... (whatever else becomes availlable)
* Adding DSL methods for `Inputs` and `Parameters`
