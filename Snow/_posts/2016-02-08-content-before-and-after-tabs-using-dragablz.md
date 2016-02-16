---
layout: post
tags: material design, dragablz, WPF, c#, .net
category: WPF
title: Content before and after tabs using Dragablz
---

The `TabablzControl` in [Dragablz](http://dragablz.net/ "Tearable TabControl for WPF") is capable of displaying content before and after the tab headers in a simple way. 
Use the `HeaderPrefixContent` and `HeaderSuffixContent` properties on `TabablzControl`. Use `HeaderPrefixContentTemplate` and `HeaderSuffixContentTemplate` respectively to provide a template to your content in case it is something else than XAML.

    <dragablz:TabablzControl HeaderSuffixContent="After">
        <TextBlock Text="Tab 1"/>
        <TextBlock Text="Tab 2"/>

        <dragablz:TabablzControl.HeaderPrefixContent>
           <TextBlock>Before</TextBlock>
        </dragablz:TabablzControl.HeaderPrefixContent>        

        <dragablz:TabablzControl.HeaderSuffixContentTemplate>
          <DataTemplate>
             <TextBlock Text="{Binding}" ToolTip="You can easily insert content here using HeaderSuffixContent"/>
          </DataTemplate>
        </dragablz:TabablzControl.HeaderSuffixContentTemplate>       

    </dragablz:TabablzControl>

