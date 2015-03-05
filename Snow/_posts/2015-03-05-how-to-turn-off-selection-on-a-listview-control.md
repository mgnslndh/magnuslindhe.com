---
layout: post
tags: WPF
categories: WPF
title: How to turn off selection on a ListView control
---

In .NET Framework 4.5 the [ListView](https://msdn.microsoft.com/en-us/library/system.windows.controls.listview(v=vs.110).aspx) control has a property called [SelectionMode](https://msdn.microsoft.com/en-us/library/system.windows.controls.listbox.selectionmode(v=vs.110).aspx "SelectionMode") that determines the selection of list view items. There are three modes of operation:

* `Single` - The user can select only one item at a time.
* `Multiple` - The user can select multiple items without holding down a modifier key.
* `Extended` - The user can select multiple consecutive items while holding down the SHIFT key.

There is however no selection mode `None` that disallows selection. Luckily there is another way to achieve the same behvaiour using a custom style for the [ListViewItem](https://msdn.microsoft.com/en-us/library/system.windows.controls.listviewitem%28v=vs.110%29.aspx "ListViewItem").

The following style makes it impossible for the `ListViewItem` to gain focus and become selected.

	<ListView.ItemContainerStyle>
        <Style TargetType="{x:Type ListViewItem}">
            <Setter Property="Focusable" Value="False"/>
        </Style>
    </ListView.ItemContainerStyle>

This solution also works for the [ListBox](https://msdn.microsoft.com/en-us/library/system.windows.controls.listbox%28v=vs.110%29.aspx "ListBox") since `ListView` is a dervived control.
