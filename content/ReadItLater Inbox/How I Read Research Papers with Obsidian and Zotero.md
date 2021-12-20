[[ReadItLater]] [[Article]]

# [How I Read Research Papers with Obsidian and Zotero](https://bagerbach.com/blog/how-i-read-research-papers-with-obsidian-and-zotero/)

19 August 2021 | 6 min read | Read more about [Learning](https://bagerbach.com/blog/tag/learning/)

How do we manage the complexity and depth from research papers in our note systems? How do we minimize the friction of taking notes in a PDF document and turning those into evergreen, permanent notes?

Those were the exact questions I was asking myself a few days ago. Reading research papers was a mess. I had no good way to import my highlighted notes to my note system, and the only good way didn't do everything I needed it to.

So I created my own system for reading research papers; a combination of [Zotero](https://zotero.org/) and [Obsidian](https://obsidian.md/). Let me show you what I made, and how it can help you.

**Process outline**

1.  Add paper to Zotero inbox
2.  Read the paper when I have time — and take notes
3.  Automatically ingest it into Obsidian with the desired template and metadata
4.  Processing the notes; creating literature notes, and turning those into permanent notes

In this article, I'll show you 1-3. Later, I'll show you how I process what I've read, turning them into literature notes, and finally, permanent notes.

Let's get to it.

## Setting up Zotero

The process always starts with me adding a paper to my Zotero inbox. [Learn how to maintain your Inbox and keep it clutter-free.](https://bagerbach.com/blog/how-i-process-inputs-from-the-internet/)

I use the [Zotero Connector](https://www.zotero.org/download/connectors) extension to save papers directly to Zotero from my browser. You can also use the magic wand button in Zotero to add papers by their DOI.

I use the new built-in PDF reader for Zotero, which allows me to extract annotations in a certain way. If you don't use it, you can use [Zotfile](https://github.com/jlegewie/zotfile) to extract annotations directly from the PDF, and they will still be inserted into the note.

To summarize; if you take notes with Zotero, extract the annotations through the right-click menu, and they'll be inserted into the note we're creating later. If you are taking notes directly in your PDF, you should use Zotfile to extract the annotations - and these will also be included when you create a new note. You can extract annotations with Zotfile by right-clicking the PDF in Zotero, clicking `Manage Attachments`, and then `Extract Annotations`.

## Setting up Obsidian

To enable the workflow on Obsidian, you'll need the [QuickAdd](https://github.com/chhoumann/quickadd) plugin. Check out my video [here](https://youtu.be/gYK3VDQsZJo) for how it works. You will also need the [Citations](https://github.com/hans/obsidian-citation-plugin) plugin. To set up Citations, follow the instructions [here](https://github.com/hans/obsidian-citation-plugin#setup).

Now, let's set up the template.

### My research paper template

The following is the template I use for papers. I use [Dataview](https://github.com/blacksmithgu/obsidian-dataview), so my metadata looks a bit different from the conventional YAML.

````
---
tags: in/paper state/process
aliases:
  - {{VALUE:title}}
cssclass: null
abstract: >
  {{VALUE:abstract}}
---

# {{VALUE:title}}

---
Type:: [[&]]
Title:: {{VALUE:title}}
Author:: {{VALUE:author}}
Year:: {{VALUE:year}}
Tags:: 
DOI:: {{VALUE:doi}}
Citekey:: {{VALUE:id}}
ZoteroURI:: [Open in Zotero: {{VALUE:title}}]({{VALUE:zoteroSelectURI}})
ReviewedDate:: [[{{DATE:gggg-MM-DD - ddd MMM D}}]]
Rating:: ==Give a rating==

---

## Citation
```latex

```

## Abstract
{{VALUE:abstract}}

## Summary of key points
- 

## Other Comments
-

## Interesting Cited References 
- 

---
{{VALUE:note}}
````

Every metadata property will be filled out by QuickAdd, except the tags and rating. Notably, the `ZoteroURI` property will contain a link which, when clicked, will open Zotero with the target paper selected. The `ReviewedDate` property will link to my daily note. Besides those, the remaining properties will just contain data about the paper itself. Something I quite like is that the script automatically links to the author(s) with WikiLinks.

### Setting up QuickAdd

We'll need to install a QuickAdd user script for this to work. The video shows you how to do so [here](https://www.youtube.com/watch?v=gYK3VDQsZJo&t=1730s). You can grab the script [here](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Attachments/citationsManager.js).

At this point, we need to create a macro — if you haven't already. In QuickAdd, go to Manage Macros, and add a new macro. Once the macro has been added, go ahead and click Configure. You'll want to add the user script to the macro — I called it 'citationsManager'.

Now, add a Template to the macro by clicking the Template button. My Template Choice looks like this:

![Template choice](https://bagerbach.com/uploads/pasted-image-20210818160734.png)

And you can't see it in the image, but I have Open enabled. Here's an explanation of the settings:

-   **Template Path** is the path to my template. I'll share that with you in a moment.
-   **File Name Format** is the format of my file names. I use & in front of papers for my file convention. The `{{VALUE:title}}` is necessary, as it grabs the paper's title and uses that — which happens through the script.
-   I use **create in folder** because I put my source notes in an inputs folder.
-   And lastly, **open**, which isn't visible. This is used to open the created file.

This is what your macro should look like.

![Macro](https://bagerbach.com/uploads/pasted-image-20210816155927.png)

Having created the macro, all you need is a QuickAdd choice to activate it. Back in the main QuickAdd menu, add a Choice of the Macro type. Click ⚙ settings for it and select your newly created macro.

## Creating notes in Obsidian from papers in Zotero

Now that we're all set up, it's time to use the script!

Having read a paper, I'll go into Obsidian and activate the `📜 Add Paper` choice. A menu like this will open:

![](https://bagerbach.com/uploads/pasted-image-20210819164144.png)

Selecting a paper will create a new note, which looks like this:

![Created note](https://bagerbach.com/uploads/pasted-image-20210819164254.png)

This paper has no DOI, which would otherwise be filled out.

So there it is. This is how I import papers into my vault; notes, metadata, and all.

## How you can use it

Any of the following variables can be accessed with `{{VALUE:variable}}`, where `variable` is the name of the variable. Most of these are from the Citations plugin, but I've added a few extra ones for convenience.

These can be used in your Template Choice as well as your markdown template.

-   `fileName` — paper title with all the special, illegal characters removed
-   `citekey`
-   `id` — also citekey
-   `author` — all authors in linked format
-   `doi` and `DOI`
-   `abstract`
-   `authorString`
-   `containerTitle`
-   `eprint`
-   `eprinttype`
-   `eventPlace`
-   `note`
-   `page`
-   `publisher`
-   `publisherPlace`
-   `title`
-   `URL`
-   `year`
-   `zoteroSelectURI`
-   `type`
-   `issueDate`

You can go into settings for the script and toggle force ignore of any empty properties. This means that, any properties that are undefined will be empty and won't be prompted for.

![Script settings](https://bagerbach.com/uploads/pasted-image-20210819165815.png)

I hope you enjoy it.

Any questions, requests, or otherwise? Feel free to reach out [(Twitter](https://twitter.com/chrisbbh)).

Sign up for my newsletter below 👇 to get updates and be the first to hear when I release new posts like this.