# Obsidian Note Definitions

A personal dictionary that can be easily looked-up from within your notes.

![dropdown](./img/def-dropdown.png)

## Basic usage

1. Create a `definitions` folder in the root of your Obsidian vault (this folder can be customised in the settings).
2. Within the `definitions` folder, create definition files (with any name of your choice).
3. Add a definition using the `Add definition` command. This will display a pop-up modal, where you can input your definition.
4. Once a definition is added, the word/phrase should be underlined in your notes. You may preview the definition of the word by hovering over the underlined word/phrase with the mouse, or triggering the `Preview definition` command when your cursor is on the word/phrase.

### Editor menu

Options available:
- Go to definition (jump to definition of word/phrase)
- Add definition (the text that you want to define must be highlighted for this to be available)
- Edit definition (right-click on an underlined definition)

### Commands

You may want to assign hotkeys to the commands available for easy access:
- Preview definition (show definition popover)
- Go to definition (jump to definition of word/phrase)
- Add definition
- Add definition context (see [Definition context](#definition-context))

## How it works

**Note Definitions** does not maintain any hidden metadata files for your definitions. 
All definitions are placed in your vault and form part of your notes.
You will notice that added definitions will create entries within your selected definition file. 
You may edit these entries freely to add/edit your definitions, but if you do so, make sure to adhere strictly to the definition rules below.
**It is recommended that you read through the definition rules first before manually editing the definition files.**

### Definition rules

1. A definition block consists of a **phrase (1 or more words), an alias (optional) and a definition**. They must be provided **strictly** in that order.
2. A phrase is denoted with a line in the following format `# <PHRASE>`. This is rendered as a markdown header in Obsidian.
3. An **optional** comma-separated line of alias(es) is expected after a phrase. This must be a line surrounded by asterisks, eg. `*alias*`. *This is rendered as italics in Obsidian*.
4. A line that occurs after a registered **phrase** and is not an alias is deemed to be a definition. Definitions can be multi-line. All subsequent lines are definitions until the definition block delimiter is encountered. You may write markdown here, which will be formatted similar to Obsidian's markdown formatting.
5. A line with nothing but three hyphens `---` is used as a delimiter to separate definition blocks. This is rendered as a delimiting line in Obsidian. (This delimiter can be configured in the settings to recognise three underscores `___` as well)

Example definition file:

> # Word1
> 
> *alias of word1*
> 
> Definition of word1.
> This definition can span several lines.
> It will end when the delimiter is reached.
> 
> ---
> 
> # Word2
>
> Notice that there is no alias here as it is optional.
> The last word in the file does not need to have a delimiter, although it is still valid to have one.
> 
> ---
> 
> # Phrase with multiple words
> 
> You can also define a phrase containing multiple words. 
>
> ---
>
> # Markdown support
> 
> Markdown is supported so you can do things like including *italics* or **bold** words.

## Definition context
> _TLDR:_ "Context" is synonymous with a definition file. By specifying a context, you specify that you want to use specific definition file(s) to source your definitions for the current note.

Definition context refers to the repository of definitions that are available for the currently active note.
By default, all notes have no context (you can think of this as being globally-scoped).
This means that your newly-created notes will always have access to the combination of all definitions defined in your definition files.

This behaviour can be overridden by specifying the "context" of your note.
Each definition file that you have is taken to be a separate context (hence your definitions should be structured accordingly).
Once context(s) are declared for a note, it will only retrieve definitions from the specified contexts.
You can think of this as having a local scope for the note.
The note now sees only a limited subset of all your definitions.

### Usage

To easily add context to your note:
1. Use the `Add definition context` command
2. Search and select your desired context

You can do this multiple times to add multiple contexts.

### How it works

`Add definition context` adds to the _properties_ of your note.
Specifically, it adds to the `def-context` property, which is a `List` type containing a list of file paths corresponding to the selected definition files.
In source, it will look something like this:
```
---
def-context:
	- definitions/def1.md
	- definitions/def2.md
---
```

You can edit your properties directly, although for convenience, it is recommended to use the `Add definition context` command to add contexts as it is easy to get file paths wrong.

### Removing contexts

To remove contexts, simply remove the file path from the `def-context` property.
Or if you want to remove all contexts, you can delete the `def-context` property altogether.

## Feedback

I welcome any feedback on how to improve this tool.
Do let me know by opening a Github issue if you find any bugs, or have any ideas for features or improvements.
