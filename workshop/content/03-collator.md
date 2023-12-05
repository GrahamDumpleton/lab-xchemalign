---
title: XChem Align - Collator tool
---

This page describes using the `xchemalign.collator` module to collate the crystallographic
files into standard names and locations so that they can be used by the next step.

## Running collator

The tool is a Python module that will be run in a terminal.

```terminal:execute
command: python -m xchemalign.collator \
  --config-file work/outputs/config_1.yaml \
  --log-file work/outputs/collator.log
```

TODO - flesh this out with some description.

## Collator outputs

The result is the collated files plus a `meta_collator.yaml` file describing the process so far.
The user should be told to view this file and be given an overview of its contents.
The file is NOT to be edited by the user.

TODO - describe the outputs.

TODO - is there a file explorer tool that can be used to explore the collated files?

TODO - a list of possible errors and remedial actions needs to be described.

Now that we have generated the aligned files the next step allows us to view them in 3D to check
that they are what we expect.