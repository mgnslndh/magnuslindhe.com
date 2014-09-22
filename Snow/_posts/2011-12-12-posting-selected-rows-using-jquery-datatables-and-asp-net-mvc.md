---
layout: post
tags: jquery, datatables, asp.net-mvc
category: Programming
title: Posting selected rows using jQuery Datatables and ASP.NET MVC
---

How do you make an ajax call to and ASP.NET MVC controller with the selected rows in a [jQuery datatable](http://datatables.net/)? Well, this is how I did it.

<!--excerpt-->

The table rows are rendered in a Razor view, each one with a column containing a checkbox like this:

    <td>
    	<input type="checkbox" name="id" value="@item.Id"/>
    </td>

I use a click handler for a hyperlink that does some validation and eventually does something like this:

	var oTable = $("#dataTable").dataTable();
    var sData = $('input', oTable.fnGetNodes()).serialize();
   
    $.post("@Url.Content("~/Controller/Action")", sData, function() {
        // success!
    }, "json");

The function [fnGetNodes()](http://datatables.net/api#fnGetNodes) will return all row elements and combined with the 'input' selector and [serialize](http://api.jquery.com/serialize/) we will get all "form" data we need to include in the ajax call.

The Controller that handles the ajax call needs to be wired for HTTP POST.

	[AcceptVerbs(HttpVerbs.Post)]
    public ActionResult Action(string[] id)
    {
    	return new JsonResult();
    }

The thing that I struggled with was the action's `id` string array parameter. It has to be a string array since there are multiple checkbox input elements with the same id. The serialize method will return something looking like this:

    id=1&id=2&id=3

When that string is posted to the action it will be converted into a string array like this:

	id[0] = "1"
	id[1] = "2"
	id[2] = "3"

With no checkboxes selected you will get a null reference for the string array.  

