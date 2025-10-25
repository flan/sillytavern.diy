---
order: 999
expanded: false
route: /extensions/_template
icon: icon-code
---

# Adding an extension

Extension entries must have a specific format to make the page easy to navigate and relatively brief, without giving too much or too little attention to any one reference.

## Criteria

For an extension to be listed, it must satisfy a few conditions:

- there must be some sort of discussion forum so prospective users can figure out whether it's a good fit for them and how difficult it is to use
- it must be at least two weeks old, helping to ensure that quick hacks made enthusiastically don't overwhelm thought-out solutions and that most critical early-adopter bugs have been ironed out
- there must be some indication that the author won't abandon it as SillyTavern's interfaces evolve

Please make sure these are clearly spelled out in your pull-request. There is no requirement that you be the original author of the extension, since the only credit given is a link to its project-page.

When submitting a pull-request, list extensions in alphabetical order. Yes, this might not give the best extensions top billing, but the purpose of this site is not to be opinionated, just to keep track of things people can actually use.

## Template

Extension entries have the following format:

- [Extension Name](http://example.org/)
  - A single sentence explaining the extension's main focus
    - A single sentence elaborating on the problem it solves
    - (optional) A single sentence elaborating on what problems it does *not* solve
  - (optional) [Reddit discussion](http://example.org/)
  - (optional) [Forum discussion](http://example.org/)
  - (optional) [Discord discussion with thread-link](http://example.org/)
    
And that's it. A link to the project (typically a Git repository), a brief description of why someone might want to consider it, and at least one link to a resource that prospective users can look at to determine whether it's worth their time or not.

## Maintenance note

When creating a new extension category, name the markdown file using Python's "snake_case" convention. If something is a work-in-progress and is not ready to make public, prefix it with an underscore, like `_template.md`.

Extension categories should not be nested: they are to be a simple list, grouped by their most-major category. If an extension falls into several categories with one not clearly being its primary focus, it is okay to place entries in multiple lists.
