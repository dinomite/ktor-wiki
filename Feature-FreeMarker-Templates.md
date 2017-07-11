## Freemarker Templates

Ktor includes support for [Freemarker](http://freemarker.org/) templates through the FreeMarker
feature.  Initialize the FreeMarker feature with a
[TemplateLoader](http://freemarker.org/docs/pgui_config_templateloading.html).

```
    install(FreeMarker) {
        templateLoader = ClassTemplateLoader(TheApp::class.java.classLoader, "templates")
    }
```

This TemplateLoader sets up FreeMarker to look for the template files on the classpath in the
"templates" package, relative to the current class path.  A basic template looks like this:

```
<html>
<h2>Hello ${user.name}!</h2>

Your email address is ${user.email}
</html>
```

With that template in `resources/templates` it is accessible elsewhere in the the application
using the `call.respond()` method:

```
    get("/{...}") {
        val user = user("user name", "user@example.com")
        call.respond(freemarkercontent("index.ftl", mapof("user" to user), "e"))
    }
```
