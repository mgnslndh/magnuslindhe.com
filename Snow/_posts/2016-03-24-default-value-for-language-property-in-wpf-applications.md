---
layout: post
tags: WPF
categories: WPF
title: Default value for the Language property in WPF applications
---

Most WPF controls you will use are derived from [FrameworkElement](https://msdn.microsoft.com/en-us/library/system.windows.frameworkelement(v=vs.110).aspx) and use the [Language](https://msdn.microsoft.com/en-us/library/system.windows.frameworkelement.language(v=vs.110).aspx) property to format values according to the corresponding culture. By setting the default value for this property you get consistent formatting for all controls in your application.
<!--excerpt-->

    FrameworkElement.LanguageProperty.OverrideMetadata(typeof(FrameworkElement), new FrameworkPropertyMetadata(XmlLanguage.GetLanguage(CultureInfo.CurrentCulture.IetfLanguageTag)));

There are also some controls, or rather elements, in the [System.Windows.Documents](https://msdn.microsoft.com/en-us/library/system.windows.documents(v=vs.110).aspx) namespace that you might encounter. One example is [Run](https://msdn.microsoft.com/en-us/library/system.windows.documents.run(v=vs.110).aspx), which can be used inside a [TextBlock](https://msdn.microsoft.com/en-us/library/system.windows.controls.textblock(v=vs.110).aspx). These elements all derive from [FrameworkContentElement](https://msdn.microsoft.com/en-us/library/system.windows.frameworkcontentelement(v=vs.110).aspx). Fine, we just override the default language dependency property on this type as well? Wrong... For some reason this throws an exception so you need to  override the property for each derived type that you care about.   

In order to get the WPF application to use the formatting provided by the regional settings in Windows I execute this code during startup:

    public partial class App : Application
    {         
        protected override void OnStartup(StartupEventArgs e)
        {            
            FrameworkElement.LanguageProperty.OverrideMetadata(typeof(FrameworkElement), new FrameworkPropertyMetadata(XmlLanguage.GetLanguage(CultureInfo.CurrentCulture.IetfLanguageTag)));
            FrameworkContentElement.LanguageProperty.OverrideMetadata(typeof(TextElement), new FrameworkPropertyMetadata(XmlLanguage.GetLanguage(CultureInfo.CurrentCulture.IetfLanguageTag)));
        }
    }
    
In this example I am only caring about the `Run` element, derived from `TextElement`. You might need to override more properties.  
    
Sadly enough, [OverideMetadata](https://msdn.microsoft.com/en-us/library/system.windows.dependencyproperty.overridemetadata(v=vs.110).aspx) will throw an exception if you try to call this method twice. This makes it hard to use this method to let the user change the language at runtime. This has not been a requirement or issue for me so far but there are solutions that can help you out:

* [Wpfsharp.Globalizer](http://rhyous.github.io/WPFSharp.Globalizer)
* [WPFLocalizationExtension](https://github.com/SeriousM/WPFLocalizationExtension)