---
title: How to release RawTherapee
contributors:
  - DrSlony
---

<div class="pagetitle">

How to Release RawTherapee

</div>

1.  Tea
2.  Pull and update
3.  Run:
        ./tools/generateTranslationDiffs

    Perform final language file updates.
4.  Run:
        dos2unix rtdata/languages/* rtdata/profiles/*
5.  Update splash screen, `RELEASE_NOTES.txt`, AppData, language files,
    profiles, etc. Once ready, commit to new branch:
      
        :git checkout -b release-5.10
        :git commit -a -m "Preparing for release 5.10-rc1"
        :git push --set-upstream origin release-5.10
6.  Once others have revised the changes, merge this `release-5.10`
    branch into `releases`:
      
        :git checkout releases
        :git pull
        :git merge release-5.10
7.  Tag and push:
      
        :git tag -a "5.10-rc1" -m "Tagged RawTherapee 5.10-rc1"
        :git push origin "5.10-rc1"
        :git push
8.  Make a source tarball:
        ./tools/generateSourceTarball

        sha1sum rawtherapee-5.10-rc1.tar.xz > rawtherapee-5.10-rc1.tar.xz.sha1
9.  Over at GitHub, create a release for the new tag. Copy the
    description from the previous tag, updating the version as
    necessary. Attach the source tarball and hash file to the release:
    <https://github.com/Beep6581/RawTherapee/tags>
10. Upload the source tarball and hash file to the website, to
    `shared/source`.
11. Upload Linux/Windows/macOS installers/packages to the website, to
    `shared/builds`.
12. Update the website, see
    <https://gitlab.com/patdavid/rawtherapee-web/-/blob/master/README.md>
    1.  `cd` into your cloned website repo and run `hugo` (no arguments)
        to generate the static website in the `/public` folder.
    2.  Log in via ssh, `cd rawtherapee.com/web/` and run
        `./danger_cleanup_hugo.sh` to delete the contents of the
        `public` folder without deleting files placed there manually and
        used by third-party services (screenshots for appdata, etc).
    3.  Then upload everything from inside your local `public` folder.

When ready for a final release (5.10, not 5.10-rc1), do as above, merge
`release-5.10` into `releases`, tag `5.10`, finally deleted branch
`release-5.10`. Never delete branch `releases`.

Once done with the release, you may need to merge `releases` back into
`dev` if new commits were made exclusively to the `release-5.10` branch.
To do that,

1.  `git checkout releases`,
2.  Edit `RELEASE_NOTES.txt` and revert the contents to describe the
    development build (`git show dev:RELEASE_NOTES.txt`).
3.  Edit the splash screen in Inkscape to revert it to the dev one.
4.  `git commit -a -m "Preparing to merge back to dev"`
5.  `git checkout dev`
6.  `git merge releases`
7.  `git push`
