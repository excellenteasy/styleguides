# LESS Style Guide

This guide is for use in [excellenteasy](http://github.com/excellenteasy) projects.

Please note that this is a work-in-progress: there is much more that can be specified.

## Table of Contents

* [The LESS Style Guide](#coffeescript-style-guide)
    * [Code Layout](#code-layout)
        * [Spacing and Alignment](#spacing-and-alignment)
        * [Property Order](#property-order)
    * [Comments](#comments)
        * [Block Comments](#block-comments)
        * [Inline Comments](#inline-comments)

## Code Layout

### Spacing and Alignment

Put a **space** after the **colon** in property declarations. You may put several spaces in front of it, to **align them across lines**. If you choose to align properties do it consistently throughout the file.

Use **spaces only**, with **2 spaces** per indentation level. Never mix tabs and spaces.

Put a **space** before the **leading bracket** in rule declarations.

Use a **blank line** to separate logical groups of properties.

Don't inline styles.

Don't omit the last semicolon.

Don't include trailing whitespace on any lines.

```css
/* No */
.class{position:absolute;top:10px;left:20px}

/* Yes */
.class {
  position: absolute;
  top     : 10px;
  left    : 20px;

  margin  : 10px;
  padding : 20px;
}
```

### Property Order

Property order is defined by 3 things. **Functionality**, **logical groups** and in a small part **alphabetical order**.
_These are very loose rules, because there is no order, that wouldn't require tons of execptions._

Do things on purpose and do things consistently.

## Comments

If modifying code that is described by an existing comment, update the comment such that it accurately reflects the new code.

The first word of the comment should be capitalized, unless the first word is an identifier that begins with a lower-case letter.

Comments should be written as full sentences, with proper punctuation.

### Block Comments

Block comments may only be used outside of a class, or mixin and are formatted with Markdown.

They should always describe the bigger picture use, and contain an example HTML snippet as they serve as [documentation](#documentation).

```css
/*
# Classy
This class is used to apply classy styling.

  <div class="classy">Look at me!</div>

*/
.classy {
  font-family: ComicSans MS, serif;
}
```

### Inline Comments

Inline comments are placed on the line immediately above the property (group) that they are describing. If the inline comment is sufficiently short, it can be placed on the same line as the property (separated by a single space from the end of the statement).

All inline comments should be indented and start with `//` and a single space.

Do not use inline comments when they state the obvious:

```css
.class {
  // Filling up space
  width: 100%;
  height: 100%;
}
```
