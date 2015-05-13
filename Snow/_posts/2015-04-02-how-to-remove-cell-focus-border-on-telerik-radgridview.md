---
layout: post
tags: WPF
categories: WPF, Telerik
title: How to remove the cell focus border on Telerik's RadGridView
---

When it comes to removing the focus border on a grid cell of the [RadGridView](http://docs.telerik.com/devtools/wpf/controls/radgridview/overview2.html) control the [current help](http://docs.telerik.com/devtools/wpf/controls/radgridview/styles-and-templates/how-to-override-default-styles.html#remove-the-border-of-the-current-cell) is a bit outdated on the subject or does not cover different themes . This short post describes how to remove the cell focus border for the Visual Studio 2013 theme. It could work for other themes as well but I have not tried.

<!--excerpt-->

The reason you might want to remove the focus border on a cell is when the grid is supposed to be read only. In that case the focus border is not really relevant on a cell. Removing the focus border also makes the grid appear more like a regular `ListView` which is what I am after in my particular case.

![Ugly cell focus border on read only grid](/images/2015-04-02-how-to-remove-cell-focus-border-on-telerik-radgridview.png)

Lets get started! Create a dummy `GridViewCell` in your XAML in order to extract its default style.

    <telerik:GridViewCell/>

Select the `GridViewCell` control and find the `Style` property in the **Properties** window. Click on the property marker (appears as a box symbol) and select **Local Resource**. The style will now be extracted into a resource in the current file.

Find the following snippet of XAML. It defines an animation that will display the focus border when the cell is regarded as "current". This is esentially when the cell has been clicked on.

	<VisualState x:Name="Current">
	    <Storyboard>
	        <ObjectAnimationUsingKeyFrames Storyboard.TargetProperty="Visibility" Storyboard.TargetName="Background_Current">
	            <DiscreteObjectKeyFrame KeyTime="0">
	                <DiscreteObjectKeyFrame.Value>
	                    <Visibility>Visible</Visibility>
	                </DiscreteObjectKeyFrame.Value>
	            </DiscreteObjectKeyFrame>
	        </ObjectAnimationUsingKeyFrames>
	    </Storyboard>
	</VisualState>

Remove the storyboard all together so the final current visual state looks like this:

	<VisualState x:Name="Current">	    
	</VisualState>

This will make the cell look just like the normal state when it is not focused.

The last thing you need to do is to apply the style to any column in your `RadGridView` or make it implicit by removing any `x:Key` from the style and rely on its `TargetType` property.