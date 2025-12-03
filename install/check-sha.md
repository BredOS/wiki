---
title: About Checksums 
description: 
published: true
date: 2025-12-03T08:18:57.403Z
tags: 
editor: markdown
dateCreated: 2025-12-01T10:08:42.952Z
---

# 1. Introduction
Checksums are compact digital fingerprints used to confirm that data has not been altered. Modern hash functions such as the SHA family (e.g., SHA-256) generate these fingerprints reliably and securely. By comparing a file’s published checksum with one you compute yourself, you can quickly verify its integrity and authenticity. This article provides an overview of how checksums and SHA hashes work and explains the basic steps for checking them.

# 2. What is a fingerprint/checksum?
A fingerprint or checksum is a string of numbers and letters generated from a file using an algorithm. This string is unique to the given file; any other file or even the slightest change to the file will result in a different fingerprint. There are many use cases for this. For example, many console manufacturers use fingerprints to validate the integrity of a file before executing it. This way, it becomes impossible to run a file, like homebrew, on such a device, effectively ensuring that only files approved by the manufacturer execute.

# 3. How to compare a fingerprint?
To compare our SHA fingerprint with your downloaded file, you need to obtain the fingerprint we provide on our website and generate a new one from your downloaded file.

- To generate the SHA fingerprint from your downloaded file, run:
```
sha256sum <path to file here>
```

- This outputs the fingerprint of the file:
```
2a6d1e524766e82ad36aeaafc41d6511f628ec0ee39fa3d14a42f5ead1f62c87 <path to file>
```

- Compare this value to the fingerprint found in our download section:

![sha.png](/sha/sha.png)

- You can either compare both values by hand or do it all in one step with:
```
[ "$(sha256sum <path to .img.xz here> | cut -d' ' -f1)" = "<fingerprint from our website here>" ] && echo OK || echo FAIL
```

> The fingerprint we publish is generated against the .img.xz file. Do not uncompress the file before validating its fingerprint.
{.is-info}


# 4. Why should i do this?
By comparing a fingerprint to a file, you validate its integrity. So if your fingerprint matches, you can be sure that the file has been correctly downloaded. Today's network devices and stacks are pretty solid, but there are scenarios in which a downloaded file will not be the same as the file on the server. If you have a bad internet connection, a hardware failure, or you have a bit flipper that was not corrected by your network stack, the bytes you receive can be different from the bytes sent from the server. Comparing the file to a published fingerprint is a simple and fast way to ensure the file's validity.

> If you have flashed our image onto your storage medium and it does not boot, it's probably a good idea to validate its fingerprint.
{.is-warning}
