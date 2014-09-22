---
category: Programming, WPF
tags: WPF, ListBox
title: ListBox with grid layout in WPF
---

I have not used WPF much and I felt that I needed to hone my skills. I wanted to layout several list items in a grid. This is what I came up with.

<!--excerpt-->

The `ListBox` is a good control to base this on. It has support for several items, selection and scrolling. They layout of items needs to be changed into a grid. This is achieved by applying a different `ItemsPanelTemplate`. I choosed the `WrapPanel` but the `UniformGrid` can also be used: 

	<ListBox.ItemsPanel>
	    <ItemsPanelTemplate>
	        <WrapPanel/>
	    </ItemsPanelTemplate>
	</ListBox.ItemsPanel>


I wanted to style the items in the `ListBox` as cards. This can be achieved by applying a `DataTemplate` to the `ListBox` like this:

	<ListBox.ItemTemplate>
	    <DataTemplate>
	        <Grid Width="332" Background="#4CFFFFFF">
	            <Grid.ColumnDefinitions>
	                <ColumnDefinition Width="132*"/>
	                <ColumnDefinition Width="200*"/>	
	            </Grid.ColumnDefinitions>
	            <Grid.RowDefinitions>
	                <RowDefinition/>
	                <RowDefinition Height="40"/>
	                <RowDefinition/>
	            </Grid.RowDefinitions>	
	            <Grid Grid.RowSpan="3" Margin="0,0,12,0" Background="{Binding Color}" Width="120" Height="120" HorizontalAlignment="Left">
	                <TextBlock Text="{Binding Id}" HorizontalAlignment="Center" VerticalAlignment="Center" FontSize="48" Foreground="White"/>
	            </Grid>
	            <TextBlock Grid.Column="1" Grid.ColumnSpan="3" Text="{Binding Title}" FontSize="16" VerticalAlignment="Center"/>
	            <TextBlock Grid.Row="1" Grid.Column="1" Grid.ColumnSpan="3" Text="{Binding Description}" TextWrapping="Wrap"/>
	        </Grid>
	    </DataTemplate>
	</ListBox.ItemTemplate>

Items in a `ListBox` are wrapped by a `ListBoxItem` and it will need some styling to get that card look I wanted:

	<ListBox.ItemContainerStyle>
	    <Style TargetType="ListBoxItem">
	        <Setter Property="Padding" Value="0"/>
	        <Setter Property="Margin" Value="6"/>
	    </Style>
	</ListBox.ItemContainerStyle> 

It was a good excercise in WPF and I am happy with the result. This is how it looks:

![ListBox with grid layout](/images/2014-09-21-listbox-with-grid-layout.png)

Colors courtsey of [Flat UI Colors](http://flatuicolors.com/).