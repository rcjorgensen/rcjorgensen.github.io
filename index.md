# 70-486: Developing ASP.NET MVC Applications

## Design the application architecture (15-20%)

### Plan the application layers

#### Plan data access
TODOS:
* Read up on EF6 and EF Core
* Read https://docs.microsoft.com/en-us/ef/ef6/
* Follow EF Core path: https://app.pluralsight.com/paths/skill/entity-framework-core
* Follow EF6 path: https://app.pluralsight.com/paths/skill/entity-framework-6

Documentation for EF Core: https://docs.microsoft.com/en-us/ef/

* Read https://docs.microsoft.com/en-us/ef/core/get-started/?tabs=netcore-cli

NOTES:
* Database First vs. Code First vs. Model First

#### Separation of Concerns

TODOS:
* Read up on design patterns
* Read up on domain driven design
* Watch clean code course: https://app.pluralsight.com/library/courses/csharp-clean-coding-principles/table-of-contents

Pluralsight path about DDD: https://app.pluralsight.com/paths/skills/domain-driven-design

NOTES:

#### Appropiate use of models, views, controllers, view components and dependency injection

TODOS:
* Watch/rewatch introductions to MVC 5 and ASP.NET Core MVC
  * https://app.pluralsight.com/library/courses/asp-net-mvc5-web-apps
  * https://app.pluralsight.com/library/courses/building-aspdotnet-core-mvc-web-applications

NOTES:
* Controllers determine how to respond to HTTP requests
* Views contain markup that is rendered by the browser
* The view is **only** responsible for presentation, not data access or business logic
* The controller is responsible for building a model that is then handed over to the view
* The model doesn't know anything about the controller or the view
* The model is only there to transport information