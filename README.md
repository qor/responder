# Responder

Respond differently according to request's accepted mime type

## Usage

```go
import "github.com/qor/responder"

// Register new mime type
responder.Register("text/html", "html")
responder.Register("application/json", "json")
responder.Register("application/xml", "xml")
// `responder` has registered above three mime types, you could register more types with the API

func (writer http.ResponseWriter, request *http.Request) {
  responder.With("html", func() {
    writer.Write([]byte("this is a html request"))
  }).With([]string{"json", "xml"}, func() {
    writer.Write([]byte("this is a json or xml request"))
  })Respond(request)
  // if failed to find responsible mime type, will use the first one
})
```

## License

Released under the [MIT License](http://opensource.org/licenses/MIT).
