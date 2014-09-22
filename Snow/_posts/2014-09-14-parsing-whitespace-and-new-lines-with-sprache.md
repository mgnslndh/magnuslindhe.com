---
layout: post
category: Parsing
title: Parsing whitespace and new lines with Sprache
---

[Sprache](https://github.com/sprache/Sprache) is a nice and small library for creating language parsers. In [Sprache](https://github.com/sprache/Sprache) you can use the `Token` method to get a parser for a token that disregards any whitespace that might surround the token. This is a really helpful method for any language that allows for whitespace throughout the grammar.

<!--excerpt-->

However, the `Token` method can not be used in a grammar where the new line characters are used as a terminator between other language constructs. The reason for this is that the `Token` method will swallow the new line characters as they are regarded as whitespace.

It is rather easy to solve this problem by implementing a variation of the `Token` method like this:

	public static Parser<T> WithWhiteSpace<T>(Parser<T> parser)
	{
	    if (parser == null) throw new ArgumentNullException("parser");
	
	    return from leading in Parse.WhiteSpace.Except(NewLine).Many()
	           from item in parser
	           from trailing in Parse.WhiteSpace.Except(NewLine).Many()
	           select item;
	}

	public static readonly Parser<string> NewLine = Parse
            .String(Environment.NewLine)
            .Text()
            .Named("new line");

The trick is to parse whitespace that surrounds the passed in parser **but exclude any new lines characters**.