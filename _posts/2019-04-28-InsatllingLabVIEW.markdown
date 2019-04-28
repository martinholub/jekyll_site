---
layout: post
mathjax: true
title: Installing LabVIEW on Debian Linux
date: 2019-04-28 11:02
tags: code linux
categories: code
description: |
    I am no fan of LabVIEW for multiple reasons, but the truth is, it is hard to replace when it comes to instrument control. Installing it on a Debian machine (e.g. Ubuntu) is possible despite not being officially supported by National Instruments. Here is how to do it.
---

I am no fan of LabVIEW for multiple reasons, but the truth is, it is hard to replace when it comes to instrument control. Installing it on a Debian machine (e.g. Ubuntu) is possible despite not being officially supported by National Instruments. Here is how to do it.

Comment out the line in `./INSTALL` script that makes installation of `niwebpipeline` necessary for success:

```bash
#webpipepkg="$webpipebase-$NIWEBPIPELINEVERS.i386.rpm"
```

Install `nisyscfg-runtime` manually:

```bash
cd ./dists/nisyscfg-runtime-18.0.0f0
sudo bash ./INSTALL "--no-prompt --accept-license --nodeps"
```

Comment out corresponding section in `./INSTALL` script (*l. 1025-1030*):

```bash
echo "Installing NI System Configuration Runtime..."
pushd "$CDPATH/dists/$nisyscfgdist" > /dev/null 2>&1
#/bin/sh ./INSTALL "--no-prompt --accept-license"
#InstallStatus=$?
InstallStatus=0
popd >/dev/null 2>&1
```
Finally, install LabVIEW:
```bash
sudo bash ./INSTALL
```
and make an alias:
```bash
alias labview='/usr/local/natinst/LabVIEW-2018-64/labview'
```

If anything goes wrong, you can try to inspect the execution with:
```bash
sudo bash -x ./INSTALL
```

Good luck!
