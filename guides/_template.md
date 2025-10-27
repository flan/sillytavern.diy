---
order: 999
expanded: false
route: /guides/_template
icon: icon-code
---

# Adding a guide

Guides occupy their own page and must be sorted in alphabetical order (which is the default if `order` is omitted from the Retype header) within an appropriate category.

To ensure that every guide is immediately useful to a prospective reader, they must start with a well-structured header, though what follows is entirely free-form.

## Criteria

For a guide to be considered, it must be free of anything that seems malicious in nature, like directing a user to do something dangerous or clearly unnecessary.

If it is required that the user download or access an external resource, it must point to a project-page or other official-seeming source. Direct links to zipfiles, executables, or the like will be rejected.

## Template

Guide headers must follow the following format:

```markdown
---
route: /guides/<category>/guide-name-slug
---

# <Guide Title>

- Last-tested SillyTavern version: 1.2.3|N/A
- Last updated: Jan 1, 1970
- Applicable platforms: Windows|macOS|Linux|Android|iOS|N/A
- External resources required: yes|no
- Technical skill required: none|filesystem management|configuration editing|network management|systems administration|programming
- Safety: perfectly safe|make a backup|ask a friend|your SillyTavern installation could be ruined|your OS could need to be reinstalled
- Expected time-commitment for a novice: 30 minutes

A brief summary of what this guide covers and what the user can expect upon completion.

## <step 1>
```

If desired, author details may be placed in the footer of a guide, using the following format, though anonymity is completely acceptable.

```
## Credits

- Scary Sandwich-face
  - Discord: @scarysammich#1234
  - Website: http://example.org/
```

If you are amending an existing guide, be respectful and place your information below that of any previous authors. If there was no prior authorship, prepend the following block:

```
## Credits

- Original guide submitted anonymously.
```

Like, just so it's obvious that you're not trying to take credit for someone else's work.

## Maintenance note

When creating a new guide category, name the markdown files and directories using Python's "snake_case" convention. If something is a work-in-progress and is not ready to make public, prefix it with an underscore, like `_template.md`.
