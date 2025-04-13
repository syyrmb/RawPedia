# RawPedia
RawTherapee Documentation

## Find all links in content

This is useful for seeing what links are present in the content

```
cd content/
grep -Eori "\[.*?\]\(.*?\)"
```

## Rename translated files

This is useful for finding all the tranlated files, then rename them to the hugo-comptaible naming convention.

To rename all the Japanese files, orginally named `ja.md`:

`find . -name jp.md -exec rename jp.md index.jp.md '{}' \;`

# Fix markdown links

The script that converted media wiki into markdown files didn't produce working links. The original links looked like `[Link Texst](Link to my Page.md)`.

Running the sed command `sed -Ei 's/\[([^]]+)\]\(([^)]+)\.md\)/[\1](\L\2)/g' **/*.md` finds most of the markdown links, removes the `.md` from the end, converts the link to lowercase, and replaces spaces with underscores.
