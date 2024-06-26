# Twig 0.5.0

Twig is a backend web framework for python utilizing the **socket** module to handle http requests and serve responses.

***IMPORTANT***
> This framework is something I made to use myself as a tool and is not recommended for production.

To install use the following command:
```cli
py -m pip install TwigWeb
```

### Changelog

---

**0.5.0**

 - Fixed dynamic router.

 - Implemented URL query parameters.

 - Implemented Headers class to separate parts of incoming request for the developer.

---

**0.4.0**

 - Added dynamic route parameters.

 - Improved route handling with Route class

---

**0.3.0**

 - Added static paths and folders functions.

 - Added element class.

 - Added component classes.

---

**0.2.0**

 - Added `set_all_routes` function

 - Fixed inconsistent request handling

 - Improved documentation

---

### Example

This example does not show all of the functionality of Twig.  There is documentation currently being worked on.

```py
from src.TwigWeb.backend.routehandler.route import Route, RouteParameter, RouteParamType
from src.TwigWeb.backend import Server
from src.TwigWeb.backend.response import Response

app = Server("", debug=True, open_root=False)

@app.route("")
def index(headers):
    #this is the index of the app
    return Response("test", ContentType.html)

@app.route("form")
def form(headers):
    #this form redirects to page/2
    return Response("""<form action="/page/2">
<label for="fname">First name:</label><br>
<input type="text" id="fname" name="fname" value="John"><br>
<label for="lname">Last name:</label><br>
<input type="text" id="lname" name="lname" value="Doe"><br><br>
<input type="submit" value="Submit">
</form>""")

@app.route("page/[num]")
def index(headers, num):
    # Headers.URL is a dictionary containing all url query parameters/variables.
    # num a dynamic route.
    return Response(f"num: {num} and {headers.URL}", ContentType.html)

@app.route("page")
def index(headers):
    return Response(f"page", ContentType.html)

app.run()
```

