# Notes to Reveal — user guide

[Download the latest signed macOS release](https://github.com/max-uho/mop-notes-pres-releases/releases/latest). Open the DMG and drag **Notes to Reveal** into **Applications**.

For macOS Sonoma 14.2 or later on Intel and Apple Silicon Macs. The universal app runs natively on either processor.

Turn an Apple Note into a live presentation. Write and format your content in Notes; Notes to Reveal follows the selected note automatically.

## Get started

1. Open Apple Notes and select the note you want to present.
2. Open Notes to Reveal and allow access to Apple Notes when macOS asks.
3. Setup shows what is already allowed. For optional cursor following, choose **Allow cursor following…** and follow the macOS prompt. The permission panel may be named **Accessibility** or **Device Control and Data Access**. Turn on the exact app name shown in setup.
4. If access is already active, choose **Start presenting**. If setup says a restart is needed, choose **Restart app** or **Restart Now** to activate cursor following.

Accessibility is optional for selecting notes and navigating with arrow keys. It also lets the app read Notes’ native blockquotes and highlights and save speaker-note edits. **Continue without cursor following** is remembered so setup will not keep asking on later launches. Press **⌘,** to reopen setup at any time.

The selected note supplies the presentation even when the cursor is outside its text. If several Notes windows are open, the frontmost Notes window supplies the selection. Switching to the presentation keeps the last active note on screen.

## Write slides and cells

A cell is a group of content that the app places within a slide. Text starts at the top of its cell. The app chooses columns or a grid from the number and type of cells.

| In Apple Notes | Result |
| --- | --- |
| Press Return once | Another paragraph in the same cell |
| Leave one or more empty lines | Spacing within the same cell |
| Put `+` on its own line | A new cell |
| Insert an Apple Notes divider line, or put `---`, `===`, or `===class===` on its own line | A new slide |

Paragraph returns and soft line breaks behave the same way. Use whichever is easiest to type in Notes. Each empty line between content adds one blank line within the cell: two empty lines in Notes give two empty lines in the presentation. Blank lines immediately before or after a slide divider, `---`, `===` (including named variants), or `+` are ignored. Leading and trailing `+` markers and repeated separators without content are ignored; use `Empty:` to reserve an empty cell. Trailing blank lines are ignored, so extra space at the end does not add an empty slide. A trailing divider line, `---`, or explicit `===` still creates one.

The preferred text slide separator is `---`; `===` remains a legacy alias. Neither text separator is recognized inside lists, tables, monostyled/code content, or native Block Quotes. The separators must occupy a line by themselves; surrounding spaces and bold, italic, or underline formatting are allowed. `A + B` remains ordinary text.

Every slide divider starts a new slide: consecutive dividers and a divider at the end create empty slides. Cell separators behave differently: repeated or edge `+` markers never reserve blank slots.

If an older note uses blank lines to create columns, add `+` at each cell boundary. Use divider lines between slides. A `+` inside ordinary text, lists, tables, code, or speaker notes stays visible.

For example, this creates two slides. Format “Project overview” as **Heading** so it is visible; the first slide groups that heading with its subtitle, then places the team in another cell:

```text
Project overview
A short introduction
+
The project team
Design and research
---
The next slide
```

The first paragraph, when formatted as **Title**, is used as the note name and hidden from the slides. Use **Heading** for the first visible heading, or place your slide content after the note title. Later Title paragraphs remain visible.

Use Notes’ own Title, Heading, Subheading and Body styles, plus bold, italic, underline, strikethrough, highlights, monostyled/code text, links, lists, checklists and tables. No HTML or CSS is needed. The presentation applies its own typography and layout while preserving supported inline formatting.

One cell fills a slide; two sit side by side. Larger groups use a balanced grid, keeping cells close to the slide’s aspect ratio:

| Cells | Columns × rows |
| --- | --- |
| 3–4 | 2×2 |
| 5–6 | 3×2 |
| 7–9 | 3×3 |
| 10–12 | 4×3 |
| 13–16 | 4×4 |

Cells fill rows from left to right; the last row may have unused space. Empty slots created with `Empty:` count like other cells. A leading Title or Heading above lower-ranked cells can span the grid’s first row; the cells beneath it follow the same sizing rule.

## Style a slide

Put `===demo===` on its own line to start a slide with the default theme’s demo border. You can use it right after the note title to style the first slide. Use a native divider or `---` for the default layout; plain `===` is also supported.

A name starts with a lowercase letter and can contain lowercase letters, digits, and hyphens. Theme authors can style a name such as `demo` with `.slide-class-demo`. If a theme has no matching rule, the slide uses the default styling. A plain divider, `---`, or `===` starts the next slide without inheriting the previous slide’s name. A named marker at the very beginning styles the first slide without creating a blank slide; anywhere else it starts a new slide.

## Reserve an empty cell

Put **`Empty:`** on its own line to reserve a layout slot. It closes any preceding cell and starts following content in another cell. Repeat it to add more slots. The aliases `[]`, `[ ]`, and `[cell]` work too; spaces inside empty brackets are optional.

```text
Empty:

Text in the next cell
```

The marker disappears from the slide. Empty cells participate in the same columns and grids as other content. Their background comes from the presentation theme; the default is black in light mode and white in dark mode.

## Fit images

Paste an image into Notes. Put a caption command on its own line below the image. Blank lines between the image and its command are allowed.

| Caption | Effect |
| --- | --- |
| `Contain:` or `Fit:` (`[fit]`) | Show the whole image without cropping |
| `Cover:` (`[cover]`) | Fill the image’s cell, cropping as needed |
| `Background:` (`[bg]`) | Fill the entire slide edge to edge, with centered cropping |

A `+` separator ends the association between an image and its commands. An image without a caption uses Cover. Background requires the image to be the slide’s only content: no text, other images or empty cells.

For an empty left cell and a fitted image on the right:

```text
Empty:

[paste an image here]
Contain:
```

Replace the bracketed instruction with an actual pasted image. The image must be alone on its line. Recognized captions disappear; unmatched captions remain visible, so check for other content between the image and the command if it appears in your slide.

Image and empty-cell commands are case-insensitive and allow surrounding spaces. Named slide classes use lowercase names. All the aliases listed above remain supported.

## Style an image

Put a style directive immediately below a pasted image or its fitting command, with no blank line in between.

```text
[paste an image here]
[fit]
[style: rounded-lg border grayscale]
```

Available styles are `rounded`, `rounded-lg`, `rounded-xl`, `border`, `border-2`, `grayscale`, `sepia`, `opacity-75`, and `opacity-50`. Use one directive per image and write the utility names in lowercase. Full-slide backgrounds use `[bg]`.

## Speaker notes

In Apple Notes, create a **Block Quote** using **Format → Block Quote** for your speaker cues, normally at the end of a slide. No `Note:` header is required. Consecutive quote paragraphs belong to the current slide’s speaker notes, regardless of cells. Bold, italic, underline, strikethrough, lists, and skipped lines are preserved. The whole quote stays out of the audience presentation and PDF; normal content following the quote stays visible.

All native Block Quotes are reserved for speaker notes. For an audience-facing quotation, use quotation marks in an ordinary Body paragraph. An optional leading `Note:` or `note:` is removed from the cues. Older plain `Note:` blocks remain supported: a standalone `Note:` hides everything until the next slide divider, while `Note: cue` hides that one line. Text such as `---`, `===`, `+`, and image commands inside a native quote remains literal speaker content.

Native Mint, Orange, Purple, Pink, and Blue highlights are read from Notes and retained in the presentation theme.

Choose **View → Speaker Notes…** (**⌘⇧P**) to open the presenter window with current and next slides, speaker notes, a timer and navigation controls. Choosing it again focuses that window. Closing the main presentation also closes the presenter.

Type directly in the **Speaker Notes** field in the desktop presenter. Changes save automatically when you leave the notes field or change slides. Typing pauses do not trigger a save. Apple Notes briefly comes forward to accept the formatted edit, then the app returns to the presenter. The app saves the cues in a native Block Quote starting with `Note:` at the end of the slide, with one blank line above it. Use the compact **B**, *I*, underline, strikethrough, and list controls. The buttons show which styles are active and preserve your text selection. Blank lines and pasted rich text are preserved. The status changes from **Unsaved changes** to **Saving…**, then **Saved** only after Notes confirms the write. If saving fails, your draft stays visible with the error and a **Retry save** button. Failed drafts are retained for their original slide while the presenter remains open; return to that slide to recover them. Edits made during a save are queued, including when you move to another slide. Clear the editor to remove the cues. Editing requires Accessibility access. If the original note changes while you edit, switch slides and return to load the latest content. The exported HTML presenter displays speaker notes.

## Navigate

- Press **Left / Right arrows** in the app to move between slides.
- Move the cursor within Notes to jump to its corresponding slide when Accessibility is enabled.
- Use the presenter window’s controls when presenting from a separate window.

Manual navigation stays in place through content updates until the Notes cursor moves again. Slides use horizontal transitions.

## Light and dark mode

Press **D** in the presentation or presenter window to switch between light and dark slides. Light mode uses black text on white; dark mode uses white text on black. Empty-cell colors also reverse. Images keep their original colors.

The app remembers your choice between launches. D in either window updates the audience, current and next previews, and the presenter’s background, notes panel and controls together. The shortcut is inactive while typing in a text field or using a setup dialog.

HTML exports start in the mode selected when exporting, and **D** also toggles their mode in the browser. Each opened HTML export starts from its saved mode. PDF exports use the app’s current mode at the time you export.

## Export a PDF

Choose **File → Export PDF…** (**⌘⌥E**) and choose a filename and destination.

The save destination is the only dialog. The app automatically exports one landscape 16:9 page per slide, with zero printer margins, local fonts, images, backgrounds and selectable text. The theme’s own content spacing is preserved; Background images fill the page. Speaker notes are excluded. The PDF uses your current light or dark mode.

Exporting keeps the live presentation on its current slide.

## Export an HTML folder

Choose **File → Export Presentation…** (**⌘⇧E**) and select a parent folder. The app creates a new folder containing the presentation’s HTML, JavaScript, CSS, fonts and image assets.

Open `index.html` in a browser to present offline, or put the whole folder on a static web server. Use Left / Right arrows to navigate, D to toggle light/dark mode, and **S** to open the speaker-notes window. The speaker window uses the same layout as the app, including current/next previews, notes, timer and navigation buttons. Its arrow keys also control the presentation. D in either window changes the mode everywhere, including the speaker interface. Press S again from the presentation to focus the existing speaker window. Keep the folder’s files and assets together when copying or sharing it. Repeated exports receive a numeric suffix rather than replacing an existing folder.

**Speaker notes remain in the HTML export’s source**, although they are hidden on the audience slides. Use PDF when you want an export that excludes speaker-note text.

## If something is missing

- **No presentation:** select a note in Apple Notes. With several windows, bring the intended Notes window to the front. Reopen setup with ⌘, to check access.
- **No cursor following:** open setup with ⌘,. If the app is already switched on in System Settings, use **Restart to recheck** under the troubleshooting disclosure. If access is still missing after restarting, **Show this app in Finder** locates the running copy so you can replace a stale or different entry. The Dev and packaged app entries are separate.
- **A command appears on a slide:** place it on its own line. For image fitting, put the command below an image with no other content in between. Background requires an image-only slide.
- **An edit takes time to appear:** large notes and Notes autosave can delay updates. Images are cached and large still images are reduced for presentation, but Notes still has to supply the updated content.

Notes to Reveal works locally. It writes to Apple Notes when you edit speaker notes in the presenter window. It needs no account, cloud service or access to the private Notes database.

## Install a custom theme

Open **Settings** (**⌘,**) and choose **Themes…**. Install a theme ZIP or enter the URL of a public GitHub theme repository. Choose it under **Active theme** to apply it to every note. HTML and PDF exports include the theme in use when you export.

Reinstall a theme to replace it with a newer version. Choose **Default** to switch back to the built-in styling.