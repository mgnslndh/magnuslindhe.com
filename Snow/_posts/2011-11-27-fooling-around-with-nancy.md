---
layout: post
tags: nancy
category: Programming
title: Fooling around with Nancy
---

[Nancy][1] first got my attention when I read the [announcement][2] by [Andreas Håkansson][3] about a year ago. I thought it was an interesting project but I could not figure out how it would be useful for me at the time. I guess I also did not fully understand the potential of such a framework. 

<!--excerpt-->

[![Nancy](/images/2011-11-27-nancy-vertical-framed-wf-bb.png)](http://nancyfx.org)

I have finally realized how I can make use of Nancy in one of my own projects. I have begun experimenting with the framework and I am trying to integrate it with my own project. I have however run in to some problems and I am not really falling into [the pit of success][4]. Some things are simple but some things just don't work. 

I have decided to [create a spike][5] or two in order to limit the complexity and find out how to make the simplest solution work and **then** try to integrate what I know works in isolation. This will also enable me to be able to show a relatively simple solution to others I case I still run into problems along the way.

I hope the spike will help me answer the following questions I have about Nancy:

 - How to serve views stored as embedded resources using the `UnityNancyBootstrapper`.
 - How to serve static files such as JavaScript and CSS. 
 - How to serve static theme files depending on the selected theme.
 - How to integrate Nancy with an already existing Unity container. A container that has been created before bootstrapping Nancy that is.

I have also decided to get the [source code for Nancy][6] instead of using the NuGet packages in order to be able to understand what is going on under the hood.
 
Looking forward to fooling around with Nancy!

  [1]: http://nancyfx.org/
  [2]: http://elegantcode.com/2010/11/28/introducing-nancy-a-lightweight-web-framework-inspired-by-sinatra/
  [3]: https://github.com/thecodejunkie
  [4]: http://www.codinghorror.com/blog/2007/08/falling-into-the-pit-of-success.html
  [5]: http://www.extremeprogramming.org/rules/spike.html
  [6]: https://github.com/NancyFx

