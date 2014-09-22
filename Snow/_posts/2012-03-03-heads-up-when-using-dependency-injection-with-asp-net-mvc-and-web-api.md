---
layout: post
title: Heads up when using dependency injection with ASP.NET MVC and Web API
---

ASP.NET MVC 3 and ASP.NET Web API (Beta) uses different but identical interfaces named `IDependencyResolver` but located in two different namespaces.

<!--excerpt-->

ASP.NET MVC 3 uses the interface [IDependencyResolver](http://msdn.microsoft.com/en-us/library/system.web.mvc.idependencyresolver.aspx) located in the namespace `System.Web.Mvc` to resolve dependencies. The [ASP.NET Web API (Beta)](http://nuget.org/packages/AspNetWebApi) on the other hand uses an interface [with the same name](http://www.asp.net/web-api/overview/extensibility/using-the-web-api-dependency-resolver) but located in the `System.Web.Http.Services` namespace to resolve dependencies.

Since both interface provide the same abstraction I wonder why it is designed this way and if they will resolve (*pun intended*) this issue in the next release.


