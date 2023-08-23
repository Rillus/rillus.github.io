I was recently asked to prepare a quick introduction to HTML for some students and it made me think about how long I've been doing this for. HTML was first released by Tim Berners-Lee in 1993. That year I was 11 years old and joined senior school. I was definitely already writing HTML before I left school 7 years later, so if HTML is 30 years old this year, then I've been writing it for at least 23 years.

I'll give a quick summary of my presentation for posterity - just in case anyone asks me for the basic HTML rundown again.

HTML underpins much of the online technologies you regularly use today. Web pages, obviously - but also emails, web apps and wherever a web app has been wrapped as a desktop or mobile app.

HTML is basically a text file with content and "tags". Tags, also known as "elements" take the form of `<tag>` and end with `</tag>` with "tag" representing the name of the tag. Between these tags, any text is directly rendered to the browser (unless styling or scripts intervene). In the older versions of HTML, we only had a few tags to work with, but this was greatly expanded and improved upon with HTML5 in 2014. 

The main improvement of HTML5 was making tags semantic. "Semantic" simply means "relating to meaning or logic", which in our post-capitalist culture translates to "it does exactly what it says on the tin". If I want navigation on my page, I use `<nav>`, if I want a footer it's `<footer>`. Some of the old tags came across too: `<div>` for divisional (block) element and `<span>` for an inline. A block element sits on it's own on the page in it's own box, with the next element being on the next line down. An inline element flows with the text around it.

Here I'll give you a basic example of an HTML page:
```
<html>
	<head></head>
	<body>
		<header>
			<nav>
				My navigation
			</nav>
		</header>
		<article>
			<h1>Article heading</h1>
			<p>
				Paragraph text.
				<em>Emphasised.</em>
				<strong>Strong text.</strong>
			</p>
		</article>
		<footer>
			<a href="link.html">A footer link</a>
		</footer>
	</body>
</html>
```

The above will probably render exactly what you think it will - a page that looks a little like this:

---
My navigation
# Article heading
Paragraph text. *Emphasised.* **Strong text.** 
[A footer link]()

---

You'll see here that a browser without any styling will apply some defaults to tags: Headings are bold and large, paragraphs are "regular" text, em tags produce italicised text and strong tags make bold text... And of course links are underlined, give a different cursor when hovered, can be tabbed to and are clickable.

---
## Activity
A good exercise to do at this stage might be to take a newspaper, magazine article or even flyer.
- Using a highlighter, mark sections with the tag you think most closely matches the intended purpose of the text: paragraphs (`p`), headings (`h1`, `h2`, `h3` ...). Is there a top `header` area? are there phone numbers or web addresses that could be links (`a`)?
- Open a text editor and write up the text on your piece of publicity. Wrap each text section in the tag you identified before.
- Indentation really helps to ensure you've closed all tags properly - and failure to close tags makes for some interesting issues that can be hard to debug in a big file. 
	- Whenever you open a tag, press enter to go to the next line and the tab button to move the text cursor to set in from the line above. 
	- When you want to close a tab, make sure the closing tag is on the same vertical line as the opening tag.
- Once you're happy, save the file with a .html file extension and open it in your browser.

Has everything rendered?
Does the structure of the text look right?
Would you make any changes?

---
From here you could go on to styling, but that's outside of the scope of this article. As always the best resource for finding out about how to make the Internet is on the Internet, so have a search and see if you can make your new html file look like the original material. If you need a hand, <a href="mailto:riley@ramone.co">drop me a line</a>!