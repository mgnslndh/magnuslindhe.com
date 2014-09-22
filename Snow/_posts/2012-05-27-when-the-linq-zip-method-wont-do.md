---
layout: post
category: Programming
tags: c#, linq
title: When the Linq Zip method won't do
---

I recently encountered a problem when I wanted to assign a color to each item of a list. The available colors were limitied to a few but there could be many items. I needed to be able to assign each color to an item and start over when all colors had been assigned.

<!--excerpt-->

I wanted an algorithm to achieve something similar to this pseudo code:

	var items = GetLotsOfItems();
    var colors = new string[] { "red", "green", "blue" }
	
	result = new {
		{ Item = item[0], Color = color[0] },
		{ Item = item[1], Color = color[1] },
		{ Item = item[2], Color = color[2] },
		{ Item = item[4], Color = color[0] },
		{ Item = item[5], Color = color[1] }
	};
    
I was first thinking of using Linq and the [Zip method](http://msdn.microsoft.com/en-us/library/dd267698.aspx) that provides a way to combine items of two lists into one list. However, the result will only be as long as the shortest list.

>If the input sequences do not have the same number of elements, the method combines elements until it reaches the end of one of the sequences. For example, if one sequence has three elements and the other one has four, the result sequence has only three elements.

That would not do since the result would only be as long as the color array.

## Modulo and indexers to the rescue

Lucky for me I  remebered the article [C#/.NET Little Wonders: Select() and Where() with Indexes](http://geekswithblogs.net/BlackRabbitCoder/archive/2012/05/17/c.net-little-wonders-select-and-where-with-indexes.aspx) by James Michael Hare that I read just the other day. By using an index I could rely on good old [modulo](http://en.wikipedia.org/wiki/Modulo_operation) to provide a color for each item like this: 

    items.Select((item,index) => new 
        { 
            Item = item, 
            Color = colors[index % colors.length] 
        });

  