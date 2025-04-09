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
