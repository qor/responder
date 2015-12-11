# Responder

Respond differently according to request's accepted mime type

## Usage

```go
import "github.com/qor/responder"

// Register new mime type
responder.Register("text/html", "html")
responder.Register("application/json", "json")
responder.Register("application/xml", "xml")
// responder already registered those three mime types, you could use the API to register new mime types

func(writer http.ResponseWriter, request *http.Request) {

  responder.With("html", func() {
    writer.Write([]byte("this is a html request"))
  }).With([]string{"json", "xml"}, func() {
    writer.Write([]byte("this is a json or xml request"))
  })Respond(request)
  // if failed to responsible mime type, will use the first one
})
```
