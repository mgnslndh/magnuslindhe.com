---
layout: post
tags: google sheets, icons, cdn, hyperlink, image
category: Miscellaneous
title: Display link icon for hyperlink in Google Sheets
---

Google Sheets can display hyperlinks in cells but sometimes you do not want to see the whole hyperlink in the cell. Why not display a nice icon instead? Let me explain how to do it.

![Link icon instead of text url](/images/2015-09-14-link-icon-instead-of-text-url-in-google-sheets.png)
 
The following formula insert a icon that is hyperlinked to an issue on [GitLab](http://www.gitlab.com "GitLab"). The cell `A17` should contain the issue number on GitLab. If `A17` is blank the icon will not be displayed.

    =IF(ISBLANK(A17);;HYPERLINK(CONCAT("https://gitlab.com/gitlab-org/omnibus-gitlab/issues/";A17);IMAGE("https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-link.svg")))

I use the [link icon](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-link.svg) from the [foundicons library](http://zurb.com/playground/foundation-icon-fonts-3) hosted on [cdnjs](https://cdnjs.com/).

![](https://cdnjs.cloudflare.com/ajax/libs/foundicons/3.0.0/svgs/fi-link.svg)

