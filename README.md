# gorest
[![Build Status](https://travis-ci.org/ejunjsh/gorest.svg?branch=master)](https://travis-ci.org/ejunjsh/gorest)

a restful go framework
## install
````go
go get github.com/ejunjsh/gorest
````
## usage
### import
````
import "github.com/ejunjsh/gorest"
````
### create a app,run a server
````go
app:=gorest.NewApp()
app.[Get/Post/Delete/Put/Error]
app.Run(":8081")
````
### support 4 methods of http request
````go
app.Get("/", func(r *gorest.HttpRequest, w gorest.HttpResponse) {
		...
	})
app.Post("/", func(r *gorest.HttpRequest, w gorest.HttpResponse) {
		...
	})
app.Delete("/", func(r *gorest.HttpRequest, w gorest.HttpResponse) {
		...
	})
app.Put("/", func(r *gorest.HttpRequest, w gorest.HttpResponse) {
		...
	})
````
### support parameters from url path
````go
app.Get("/:abc/:cba", func(r *gorest.HttpRequest, w gorest.HttpResponse) {
		fmt.Println(w.PathParams["abc"],w.PathParams["cba"])
	})
````
### support json,xml,file as result of return
````go
app.Get("/", func(r *gorest.HttpRequest, w gorest.HttpResponse) {
        w.WriteJson(jsonObj)
        //w.WriteXml(xmlObj)
		//w.WriteFile("/Users/zhouff/file.txt")
	})
````
### support dealing with errors
````go
app.Error(func(err error, r *gorest.HttpRequest, w gorest.HttpResponse){
		if e,ok:=err.(gorest.NoFoundError);ok {
			w.Write([]byte(e.Error()))
		}
		if e,ok:=err.(gorest.InternalError);ok {
			w.Write([]byte(e.Error()))
		}
	})
````

### see [example](https://github.com/ejunjsh/gorest/blob/master/main/main.go)
