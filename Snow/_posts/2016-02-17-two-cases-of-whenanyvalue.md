---
layout: post
tags: reactiveui, rxnet, c#, .net, mvvm
category: ReactiveUI
title: Two cases of WhenAnyValue
---

`WhenAnyValue` is a method on `ReactiveObject` that can turn `INotifyPropertyChanged.PropertyChanged` events into an `IObservable`. 
  
    var layerNotes = this
          .WhenAnyValue(vm => vm.LayerViewModel)
          .Select(vm => vm.Notes)
          .ToProperty(this, vm => vm.Notes);

The code above will actually only push property changes through when the `LayerViewModel` property is changed. Not when its `Notes` property changes.

The correct way is to use the complete property chain in the call to `WhenAnyValue` like the following code:

    var layerNotes = this
          .WhenAnyValue(vm => vm.LayerViewModel.Notes)          
          .ToProperty(this, vm => vm.Notes);
          
The code above will push property changes containing the content of the `LayerViewModel.Notes` every time the `LayerViewModel` property changes or its `Notes` property changes.