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

### 0.1.0

- Fix semicolon after Bible verse (e.g.Isaiah 26:14;) being marked invalid.
- Highlight Bible references.
- Mark Bible verse number by themselves, like (verse 6), as invalid so full references will be used instead.

### 0.1.1

- Change so that (verse N) where N is any number is considered valid but verse followed by anything other than number is not valid.

### 0.1.2

- Update to account for abbrev Adversaria being used instead of WE
- Don't mark a ")" after a reference as invalid

### 0.1.3

- Highlight @CanonsNC differently from other abbreviations to indicate it shouldn't be modified
- Add AngIdea as an abbreviation of "The Angelic Idea about the Creation of the Universe" at the end of Divine Wisdom
- Highlight cross reference sentences starting with "See" or "Under"

### 0.1.4

- Make Bible verse highlighting more robust

### 0.1.5

- Fix bug encountered making Bible verse highlighting more robust
- When ":" before or after a number and it's not part of a Bible verse show as invalid

### 0.2.0

- Add back showing Latin principal words in italic as was also done by Potts. This time the search pattern is more robust than the previous attempt.
- Added support for subsections quarter and third, in addition to half.
- Account for Adversaria sections that start with characters like 3/.
- Don't show an error if a `@<section-num>` is followed by a `)`.

### 0.2.1

- Mark as invalid lines missing principal Latin phrase

### 0.2.2

- Detect stray characters
- Detect invalid word case changes
- Make cross-reference expression more robust

### 0.2.3

- Show injected Latin words in italic
- Make cross-reference expression more robust

### 0.2.4

- Make cross-reference expression more robust

### 0.2.5

- Extend highlighting for Latin injected region to allow for a Latin phrase to used in addition to just a word

### 0.2.6

- Fix injected Latin highlighting so English word can be after ' and ( in addition to a space

### 0.2.7

- Add Continued to words that can begin a cross-reference sentence

### 0.2.8

- Made detection of invalid chars before and after digits more robust

### 0.2.9

- Allow appending an a or b to a section number

### 0.3.0

- Extend invalid checks

### 0.3.1

- Further extend invalid checks

### 0.3.2

- When words have underscores on either side of them, then show in italic to indicate they're used for emphasis.

### 0.3.3

- Perform a check in cross-reference sentence for principal phrase missing quote. (Only the first cross-reference in the sentence is handled.)
- Allow for a period following "General article" in the validation for this phrase.

### 0.3.4

- Adding grammar for individual cross-references, such as `<"Sake of, For the"-Propter>`. This allows a cross-reference to be marked as such when it's not part of a "See..." sentence.

### 0.3.5

- Extend check for extra spaces to also include extra non-alphabet characters.
- Check for missing opening or closing parenthesis.

### 0.3.6

- When emphasizing, match to next `_`, not last `_` in line.
- Extend check for space between periods to also include other chars
- Check for unexpected adjacent chars.
- Check for matching quote missing.

### 0.3.7

- Made detection of principal phrase lines more robust
- Made detection of unexpected lines more robust
- Highlight text inside single quotes

### 0.3.8

- Make a footnote a first-class concordance element

### 0.3.9

- Highlight footnote keyword

### 0.4.0

- Various fixes to matching patterns.

### 0.4.1

- Allow c and d to follow section # in addition to a and b.
- Update list of work abbreviations to match what's in swedenborg-works-info.csv.

### 0.4.2

- Updates to account for single quote changed to double quote for Bible quotes

### 0.4.4

- Convert from subsections half, third, and quarter to decimal form (e.g. [1.2]).
- Remove check for invalid Bible verses that resulted in too many false positives.

### 0.4.5

- Disable highlighting of quotes so that highlighting of injected Latin will done inside the quotes.

### 0.4.6

- Remove works no longer being referenced.

### 0.4.7

- Update validation checks.

### 0.4.8

- Account for update of PPEs being separated by PPLs using a semicolon.

### 0.4.9

- Fix so Latin injections are always marked.

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
