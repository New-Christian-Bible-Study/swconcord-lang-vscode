# Swedenborg Concordance Syntax Highlighting support for Visual Studio Code

This [Visual Studio Code language extension](https://code.visualstudio.com/api/language-extensions/syntax-highlight-guide) provides syntax highlighting of the Swedenborg concordance text file to aid in:

- Navigate between entries faster by making the principal phrase lines stand out as is done in the original Potts concordance.

- Make reference abbreviations stand out making it easier to see when contexts change from one work to another.

- Highlight many errors such as invalid abbreviations and numbers mixed with letters. _See [Known Issues](#known-issues) for limitations of this highlighting._

![image](https://github.com/New-Christian-Bible-Study/swconcord-lang-vscode/assets/36829186/1d392c76-57ef-4d83-8b0b-23ef27a9a526)

## Requirements

This extension is intended to be used with the concordance directory opened in Visual Studio Code. This is because the highlight color rules are defined in the file `.vscode/settings.json` under this directory.

## Known Issues

- Some valid constructs may be highlighted as invalid.
- Not all invalid constructs are being highlighted.

## Release Notes

### 0.0.1

Initial release.

### 0.0.2

Include extension icon.

### 0.0.3

- Don't attempt show English words in bold and Latin words in italic which can fail in some cases. Instead, underscore principal phrase lines.
- Fixed some numbers inappropriately marked as invalid.
- Included syntax highlighting rules in extension.

### 0.0.4

Syntax highlight #problem comments to help make stand out.

### 0.0.5

Made valid and invalid patterns checks more robust.

### 0.0.6

Continued making valid and invalid patterns checks more robust.

### 0.0.7

- Allow for parenthetical footnotes like LJ 25(i)
- Mark lines that don't begin with @ or upper case letter as invalid
- Allow spaces between "#" and "problem" in problem comments.
- Allow support for subsection [half]

### 0.0.8

- Allow for a section range to be indicated such as @SE 988-995
- For principal phrase lines only use English phrase as pattern so refs get highlighted on these lines
- Use bold for principal phrase rather than underline so spelling errors stand out.

### 0.0.9

- Fix semicolon after Bible verse (e.g.Isaiah 26:14;) being marked invalid.
- Highlight Bible references.
- Mark Bible verse number by themselves, like (verse 6), as invalid so full references will be used instead.

## Extension Development

Development of the extension can be done as follows:

1. Open directory `editing/swconcord-lang-vscode` containing the extension in Visual Studio Code.

2. Modify the grammar rules in file `syntaxes/swconcord.tmLanguage.json`

3. To test changes to the grammar rule press F5 to open an instance of Visual Studio Code with the extension automatically applied. This is considered the _extension development host_. Open the concordance directory. _Note: Close any instance of Visual Studio Code with this directory already opened before doing so, otherwise this instance will be used without the extension installed._

4. Color highlighting rules in section `editor.tokenColorCustomizations` of `.vscode/settings.json` can be changed. Saving the file will automatically cause the updates to be applied when looking at .swconcord files. There are test files under `swconcord-process/test/data/Concordance content` that can be used for testing how the concordance file looks and how some invalid constructs are rendered.

If you make changes to the grammar file, in the extension development host instance of Visual Studio Code you can press Ctrl+R to reload the extension.

### Work abbreviations as keywords

So that references to Swedenborg's works stand out, a keyword for each work abbreviation is used. The following consideration need to be made about the order of abbreviations in the language file:

- An abbreviation whose beginning portion is the same as the beginning of another larger abbreviation needs to come after the larger abbreviation so that it won't be ignored. These abbreviations are

    - LJCont
    - LJPost
    - LJ
    - WHApp
    - WH

