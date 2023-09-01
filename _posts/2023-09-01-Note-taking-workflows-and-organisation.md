![](/assets/notes.jpg)
There's so much discourse around note-taking at the moment, I thought I'd throw my own workflow into the mix to further muddy the waters.

For a few years I've been trying to work out the best way to manage my thoughts, projects and knowledge in a way that's accessible and archivable. The archivability aspect is not important on it's own, as much as being able to access the archive and find what I need easily, but not have it clutter my current thoughts and in-progress projects - otherwise I can say I've achieved the archiving by simply forgetting everything I ever knew!

I started out trying to keep Trello boards for every project, but having a column for every category and a card for each item quickly got unwieldy: I'd have 20 boards, each with 20 columns and 20 cards per columns and no overarching search. To find something, you needed to really dig.

## Obsidian
I first found out about [Obsidian](https://obsidian.md/) when I started playing with [Mastodon](https://mastodon.social) last year. In exporting my Twitter followers to find who was over on the [Fediverse](https://en.wikipedia.org/wiki/Fediverse), I reconnected with an [ex-colleague](https://pkm.social/@pd) who is now very much into Personal Knowledge Management (PKM). I downloaded Obsidian immediately and have used it pretty much every day since.

To me, there are a few main advantages:
- It's free
- Write in markdown. Markdown is a simple way to style text using basic characters, so you don't need to highlight text and italicise it, you can simply wrap it in asterisks and that will do the job.
- The notes themselves are portable. The use of markdown means all notes are plain text and so can be ported to another platform easily if you ever decided Obsidian wasn't for you.
- The editor itself is basically an opensource web app. For me, a web developer, this is great, as the platform itself is editable and you can add HTML or CSS to it for custom styling or functionality. It also thus has a great existing range of community plugins, so the functionality is extensible.
 
## Organising your notes
I started devouring articles on PKM and note-taking and organisational strategies and I currently have a system is place that is a combination of several different styles.
### [Zettelkasten](https://zettelkasten.de/posts/overview/)
Zettelkasten just means "note box" in German. This is a great place to start when you begin taking notes in a new system. The concept is simply "just take notes then put them in the box", over time you may notice themes develop, at which point you can start to add structure. It is based on the work of Niklas Luhmann who created his own numbering system when linking notes together, but we can simply use links in our note apps.
One of the main ways in which I add notes to my system is via "Daily notes". In Obsidian (and a lot of other apps) you'll have a note for the day. As I have meetings or ideas, I can add to this note quickly and without having to think about where it goes. I can later file it away, or copy sections to other notes.
### [PARA](https://fortelabs.com/blog/para/)
"The PARA method", brainchild of Tiago Forte, and subject of his book of the same name, is all the rage and claims to be the best way to organise your digital footprint by breaking up your notes into broad sections:
#### Projects
Current activities or discrete items that need to be addressed in a reasonably short time period e.g. "buying a car", a work project, or something you're transiently interested in (you suddenly decide you want to write a book on the history of hovercraft, for some reason)
#### Areas
Longer term responsibilities i.e. Notes relating to your company, or perhaps sub-areas within your company (the blog linked above mentions HR, Marketing, R&D etc.), your house.
#### Resources
This is defined by Forte as "things you're interested in learning about", but I use this more as a dumping ground for items that don't fit into my projects or areas - as such my Resources folder is a little bit lighter.
#### Archive
Anything from the above that you're done with for now, like your failed hovercraft book idea.
### [Johnny.Decimal](https://johnnydecimal.com/)
I must have ended up at the above site from a link in a PKM article at some point, and I'm not sure how widely used it is. The short of it is that you assign numbers to your folders and files, which gives them an address e.g 01.02 for the 2nd item in the first folder. This address is reasonably unchanging, and because of this your files appear in a predictable and logical ordering.

I've not followed the system very closely, but my implementation (by combining with the PARA method) looks like this:
```
01. Projects
	01.01-09 Company 1
		01.01 Project 1
		01.02 Project 2
	01.10-11 Company 2
		01.10 Another project, but for company 2
	...	
02. Areas
	02.01 Company 1
		02.01.01 Features
		02.01.02 Finances
		02.01.03 Competitors
		...
03. Resources
04. Archive	
```

I spend most of my time in Projects at the top, and can find things I'm currently working on very quickly, and the further down the folder/file list you go, the less used an item is likely to be. For oft-used files, you'll start to remember the address for quickly pulling up the file via command palette shortcuts.
## Anything else?
In addition to the above structure, I have a couple of other notable folders (although probably not relevant for everyone!):
### Kerouac
I use Obsidian exclusively on desktop (I don't like paying for anything if I can help it, and in order to sync with Obsidian on mobile, I would need to pay for a subscription to keep a "vault" in the cloud), so in order to be able to take notes on my mobile, and have them appear in Obsidian, I use an app called [GitJournal](https://gitjournal.io/). This posts notes to a Github repo when I type them into my phone. I can then `git pull` locally to sync this to my desktop, and file them accordingly. This also works in reverse if I commit to the repo from my desktop, it picks it up on my mobile. The set-up took a little experimentation, so if that's something you're interested in, [let me know](mailto:riley@ramone.co) and I'll expound on it in a future blog post.
### rillus.github.io
This is the codebase for this very blog you're reading. It's authored within my Obsidian vault, and compiled into a [Jekyll](https://jekyllrb.com/) site with Github Actions and published to Github Pages. I briefly noted the build steps on the [About page](https://ramone.co/about/), but this also needs some elaboration to be truly useful to people who live outside my own head.
## Always evolving
I don't think this is my PKM's final form (and perhaps a final form for the digital representation of one's thoughts is impossible, as our own thoughts are forever shifting and dancing around our nogs), so I wouldn't be surprised if this wasn't my final article on the topic.

I hope some of this has been useful, and at least given you a jumping off point for inspiration for your own notes. Of course, you'll need to create something that works for you personally, and the format may differ depending on the subjects you're interested or your own goals. Equally, Obsidian may not be the ultimate tool for you - if you find it too much of a blank canvas (which some people have said it is, prior to establishing your own structure), have a search around for other options.

Mark these words, and everything will be all write.