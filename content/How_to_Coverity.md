---
title: How to Coverity
contributors:
  - DrSlony
---

1.  Download Coverity Build Tool <https://scan.coverity.com/download>
    and extract to e.g. \$HOME/programs/
2.  cd to RawTherapee source clone:
      
    `cd ~/programs/code-rawtherapee/`
3.  Clean up:
      
    `make clean && ./clean`
4.  Run "cov-build", either passing a script which compiles RawTherapee:
      
    `~/programs/cov/bin/cov-build --dir cov-int ~/scripts/crunch`

    or by passing the compilation instructions manually, in which case
    first create the build directory, enter it and run "cmake":

    `mkdir build-cov && cd build-cov && cmake -DPROC_TARGET_NUMBER="2" -DBUILD_BUNDLE="ON" ..`

    and then "cov-build" with "make":

    `~/programs/cov/bin/cov-build --dir cov-int make -j3`
5.  Create a compressed tar archive of the results (xz has the best
    compression) with "cov-int" as the root:
      
    `tar caf rawtherapee.xz cov-int`
6.  Upload the build to
    <https://scan.coverity.com/projects/3455/builds/new?tab=upload>
7.  Notify: <https://github.com/Beep6581/RawTherapee/issues/3558>

## All in One

    mkdir build-cov && cd build-cov && \
    cmake -DPROC_TARGET_NUMBER="2" -DBUILD_BUNDLE="ON" .. && \
    ~/programs/cov/bin/cov-build --dir cov-int make -j3 && \
    tar caf rawtherapee.xz cov-int && \
    curl --form token=8qD9bol24Dc2vjJC4_O5ug \
      --form email=contactus@rawtherapee.com \
      --form file=@rawtherapee.xz \
      --form version="$(grep Version AboutThisBuild.txt | sed 's/Version: //')" \
      --form description="$(date)" \
      https://scan.coverity.com/builds?project=RawTherapee && \
    echo "Done!"
