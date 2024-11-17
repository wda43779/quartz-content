[source](https://quartz.jzhao.xyz/authoring-content#:~:text=Some%20common%20frontmatter%20fields%20that%20are%20natively%20supported%20by%20Quartz%3A)

Some common frontmatter fields that are natively supported by Quartz:

- `title`: Title of the page. If it isn’t provided, Quartz will use the name of the file as the title.
- `description`: Description of the page used for link previews.
- `permalink`: A custom URL for the page that will remain constant even if the path to the file changes.
- `aliases`: Other names for this note. This is a list of strings.
- `tags`: Tags for this note.
- `draft`: Whether to publish the page or not. This is one way to make in Quartz.
- `date`: A string representing the day the note was published. Normally uses `YYYY-MM-DD` format.

我试了`permalink`没啥效果，怎么回事呢？