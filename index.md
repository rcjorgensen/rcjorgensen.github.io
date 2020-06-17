<!-- Curriculum and Notes for 70-486: Developing ASP.NET MVC Applications -->


# Design the application architecture (15-20%)

## Plan the application layers

### Plan data access
TODOS:
* Brush up on EF6 and EF Core
* Read <https://docs.microsoft.com/en-us/ef/ef6/>
* Follow EF Core path: <https://app.pluralsight.com/paths/skill/entity-framework-core>
* Follow EF6 path: <https://app.pluralsight.com/paths/skill/entity-framework-6>

Documentation for EF Core: <https://docs.microsoft.com/en-us/ef/>

* Read <https://docs.microsoft.com/en-us/ef/core/get-started/?tabs=netcore-cli>

NOTES:
* Database First vs. Code First vs. Model First

### Separation of Concerns

TODOS:
* Brush up on design principles and best practices
* Learn more about domain driven design
* Watch clean code course: <https://app.pluralsight.com/library/courses/csharp-clean-coding-principles>

Pluralsight path about DDD: <https://app.pluralsight.com/paths/skills/domain-driven-design>

NOTES:

### Appropiate use of models, views, controllers, view components and dependency injection

TODOS:
* Watch introductions to MVC 5 and ASP.NET Core MVC
  * <https://app.pluralsight.com/library/courses/asp-net-mvc5-web-apps>
  * <https://app.pluralsight.com/library/courses/building-aspdotnet-core-mvc-web-applications>

NOTES:
* Controllers determine how to respond to HTTP requests
* Views contain razor syntax which is a mix of HTML and C# that will be rendered into HTML on the server before being sent to the browser
* The view is **only** responsible for presentation, not data access or business logic
* The controller is responsible for building a model that is then handed over to the view
* The model doesn't know anything about the controller or the view
* The model is only there to transport information



### Choose between client-side and server-side processing

### Design for scalability

### Choose between ASP.NET Core and ASP.NET

### Choose when to use .NET standard libraries

## Design a distributed application

## Design and implement the Azure Web Apps life cycle

## Configure state management

## Design a caching strategy

## Design and implement a Web Socket strategy

## Design a configuration management solution

### Manage configuration sources

TODOS:
* Learn about INI-files
* Brush up on how to transform web.config-files for different environments

NOTES:
* web.config files are XML-files which are used in classic ASP.NET
* web.config contains an appSettings-element where custom configuration values can be placed
* appsettings.json are JSON-files which are used in ASP.NET Core

Add configuration values to appSettings and use static method ConfigurationManager.AppSettings to access the values at runtime.

#### web.config:
```xml
<configuration>
  <appSettings>
    <add key="message" value="Hello!"/>
    ...
  </appSettings>
  ...
</configuration>
```
#### Controller:
```c#
public class GreetingController : Controller
{
    public ActionResult Index()
    {
        var model = new GreetingViewModel();
        model.Message = ConfigurationManager.AppSettings["message"]; // Hello!
        return View(model);
    }
}
```

#### View:
```html
@{
    ViewBag.Title = "Index";
}

<h2>Index</h2>

@Model.Message <!-- Displays Hello!-->
```
### Manage environment variables

### Implement Option objects

### Implement multiple environments using files and hierarchical structure

TODOS:
* Brush up on the hiearchy of configuration sources in ASP.NET Core including how environment specific configuration files like appsettings.Development.json are handled

### Manage sensitive configuration

### React to runtime configuration changes

### Implement a custom configuration source

### Secure configuration by using Azure Key Vault

### Use the secret Manager tool in development to keep secrets out of your code for configuration values

## Interact with the host environment

## Compose an application by using the framework pipeline

# Develop the User Experience (15-20%)

## Design and implement routes

### Define a route to handle a URL pattern

```
.
|-- App_Start
    |-- BundleConfig.cs
    |-- FilterConfig.cs
    `-- RouteConfig.cs

```
* Default route will map the first part of the URL to the controller, the second to the action and the last to an id
* The _defaults_ parameter makes sure that the following is true
  * it is not necessary so supply an id i.e. both "/Home/Index/5" and "/Home/Index" are valid routes
  * if no action is specified the Index action is used i.e. "/Home" is equivalent to "/Home/Index"
  * if no controller is specified the Home controller is used i.e. "/" is equivalent to "/Home/Index"
* It is not possible to specify an action without a controller, e.q. the route "/Index" would not be mapped to "/Home/Index" instead the request will probably fail because there is not "Index"-controller

```c#
public class RouteConfig 
{
    public static void RegisterRoutes(RouteCollection routes)
    {
        routes.IgnoreRoute("{resource}.axd/{*pathInfo}");

        routes.MapRoute(
            name: "Default",
            url: "{controller}/{action}/{id}",
            defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }
        );
    }
}
```