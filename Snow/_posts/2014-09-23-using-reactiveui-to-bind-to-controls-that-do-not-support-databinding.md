---
layout: post
category: Programming, Windows Forms
tags: WinForms, Windows Forms, ReactiveUI, ToolStripMenuItem, Data Binding
title: Using ReactiveUI to bind to controls that do not support data binding
---

I am using [ReactiveUI](http://www.reactiveui.net/) in Windows Forms project and want to bind a view model property to a tool strip menu item checked property. The [`ToolStripMenuItem`](http://msdn.microsoft.com/en-us/library/system.windows.forms.toolstripmenuitem(v=vs.110).aspx) control is not bindable and there is no built in support for this control in ReactiveUI. 

<!--excerpt-->

A simple two way bind will not work since the control will not notify about property changes:

    this.Bind(ViewModel, vm => vm.ReuseAddresses, view => view.ReuseAddresses.Checked);

ReactiveUI to the rescue! There is an overload method that will allow you to pass an observable (of any type) that will trigger an update of the view model property:

    this.Bind(ViewModel, vm => vm.ReuseAddresses, view => view.ReuseAddresses.Checked, ReuseAddresses.CheckedObservable());

I made a simple extension method on [`ToolStripMenuItem`](http://msdn.microsoft.com/en-us/library/system.windows.forms.toolstripmenuitem(v=vs.110).aspx) that returns an observable for the [`CheckedChanged`](http://msdn.microsoft.com/en-us/library/system.windows.forms.toolstripmenuitem.checkedchanged(v=vs.110).aspx) event like this:

	public static IObservable<bool>  CheckedObservable(this ToolStripMenuItem self)
    {
        var observable = Observable
            .FromEventPattern(
                h => self.CheckedChanged += h,
                h => self.CheckedChanged -= h
                )
            .Select(e => ((ToolStripMenuItem)e.Sender).Checked);

        return observable;
    }


There is a NuGet package [ReactiveUI.Events](http://www.nuget.org/packages/reactiveui-events/) that adds lots of extension methods for events in WPF. But for Windows Forms you are stuck with creating your own, at least for now.