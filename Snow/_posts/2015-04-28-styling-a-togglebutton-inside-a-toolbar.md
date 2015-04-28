---
layout: post
tags: WPF
categories: WPF
title: Styling a ToggleButton inside a Toolbar
---

If you create a default style for the `ToggleButton` control and expect your controls to pick it up when they are placed in a `Toolbar` control, you are dead wrong.

The `Toolbar` has its own default style for the `ToogleButton` that it will used when they are placed inside a `Toolbar`. It is however pretty easy to override the style like this:

	<Style x:Key="{x:Type ToolBar}" TargetType="{x:Type ToolBar}" BasedOn="{StaticResource {x:Type ToolBar}}>
        <Style.Resources>
            <Style 	x:Key="{x:Static ToolBar.ToggleButtonStyleKey}" 
					TargetType="ToggleButton" 
					BasedOn="{StaticResource {x:Type ToggleButton}}">
			
		        <!-- your toggle button style for toolbars goes here -->

			</Style>
        </Style.Resources>

        <!-- The rest of your toolbar style goes here -->

    </Style>

The snippet above defines a default style for the `Toolbar` control that redfines the style for toggle buttons inside toolbars.