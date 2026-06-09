---
id: 1fwop28z1f
slug: a-writefreely-contact-form
title: A writefreely contact form
created: 2025-01-17 19:47:55
updated: 2025-02-08 19:28:34
tags:
  - writefreely
  - software
  - writing
---
Thanks to [dejalavidavolar](https://discuss.write.as/t/tutorial-letterbird-contact-form/12572) and a simple Javascript injection into the custom CSS, it's possible to use a [Letterbird](https://letterbird.co/) contact form in writefreely.

You simply embed a simple script into the Customise ... CSS window, using the relevant Letterbird username and the URL of the page it will be on. Don't forget to add the terminating `<style type="text/css">` so that the CSS is correctly incorporated.

Edit your writefreely contact page to include the following text:

`<div id="letterbird-container"></div>`

Remember, the URL within the script and the URL of the page accessed containing the form must be a perfect match ... this means that a draft version of the post (which has a random filename) will *not* display the form.

I've not managed to find a way to display the graphics or header text that Letterbird forms can also incorporate (but, then again, I've not tried very hard either).
