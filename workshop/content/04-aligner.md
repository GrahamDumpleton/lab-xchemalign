---
title: XChem Align - Aligner tool
---

This page describes running the `xchemalign.aligner` tool that takes the files created by `xchemalign.collator`
and generates alignments corresponding to the different sites (typically one site, but sometimes more than one.

The `xtalforms.yaml` and `assemblies.yaml` configuration files need to be generated prior to running *aligner*
and the user needs to be guided through how to generate these. Those files will be generated in the editor,
possibly with "smart insert" actions.

## Running aligner

The tool is a Python module that will be run in a terminal.

```terminal:execute
command: python -m xchemalign.aligner \
  --config-file work/outputs/upload_1 \
  --log-file work/outputs/aligner.log
```

TODO - flesh this out with some description.

## Aligner outputs

The result is the aligned files plus a `meta_aligner.yaml`.
The user should be told to view this file and be given an overview of its contents.
The file is NOT to be edited by the user.

TODO - describe the outputs.

TODO - is there a file explorer tool that can be used to explore the aligned files?

TODO - a list of possible errors and remedial actions needs to be described.
