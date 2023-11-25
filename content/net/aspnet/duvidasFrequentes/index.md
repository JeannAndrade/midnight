---
layout: default
---

# Dúvidas frequentes em projetos ASP.NET Core

## @model e @Model na view

É sempre uma dúvida a questão de onde usar o @model e onde usar o @Model em uma view.
O tipo do modelo de visualização é especificado usando a expressão @model, com m minúsculo. O valor do modelo de visualização é incluído na saída HTML usando a expressão @Model, com M maiúsculo.

Veja no exemplo a seguir na controller:

```csharp
using Microsoft.AspNetCore.Mvc;
namespace FirstProject.Controllers {
  public class HomeController : Controller {
    public ViewResult Index() {
    int hour = DateTime.Now.Hour;
    string viewModel =
    hour < 12 ? "Good Morning" : "Good Afternoon";
    return View("MyView", viewModel);
    }
  }
}
```

A string `viewModel` será passada como model para view *MyView*.

A view:

```html
@model string
@{
  Layout = null;
}
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-width" />
    <title>Index</title>
  </head>
  <body>
    <div>
      @Model World (from the view)
    </div>
  </body>
</html>
```

----
