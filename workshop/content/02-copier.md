---
title: XChem Align - copier tool
---

This page guides the user through running the **copier** tool.
This is running the `xchemalign.copier` module with the appropriate arguments.
The copying is done using `scp` (there is an alternative more manual approach).
The tool will be run in a terminal.

The result is the files required for the next steps being copied to the local filesystem.

## Configuration

The easiest way to configure copier is through the `config_1.yaml` file you created in the last step
(the tool can be run purely with commandline options if you prefer, or a bit of both).

To see all the options run this:

```terminal:execute
command: python -m xchemalign.copier --help
```

The copier tool will use the following settings from the config file.

* **base_dir**
* **inputs.dir** (can have multiple values)
* **scp.*** 

**base_dir** and the **inputs.dir**(s) are concatenated to define the location(s) of the visit
directories. the files are copied to the location specified by the `--output-dir` commandline
parameter. Your SSH credentials are specified by the **scp.*** options.

## Running copier

Once you have double-checked those settings you can run copier like this:

```terminal:execute
command: python -m xchemalign.copier \
  --mode scp \
  --config-file work/outputs/config_1.yaml \
  --output-dir work/inputs \
  --log-file work/outputs/copier.log
```

THIS WILL TAKE SEVERAL MINUTES TO COMPLETE, possibly up to an hour if you have lots of data.
And the speed will depend on your internet connection.

## Outputs

As it runs you will see data accumulate in the `work/inputs` directory
(the name is a little confusing as this directory is the *input* to the other xchemalign tools).

One complete you will have all the data that is needed to process with the **collator** and **aligner**
tools.

In brief, the copier process does the following for each visit you have configured:

1. copy the soakdb file (`soakDBDataFile.sqlite`) from Diamond
2. opens the soakdb file and queries it to identify the relevant crystals that need to handled
3. copies the corresponding PDB, MTZ and CIF files for those crystals
4. copies the `pandda_inspect_events.csv` files that are configured
5. inspects those `pandda_inspect_events.csv` files to identify the PanDDAs event map files (.ccp4 files)
   that define the ligand binding event for each crystal
6. copies those .ccp4 files

At the end you have all the files that are needed, in the exact same relative locations that they
were at Diamond and you can move on to running the **collator** tool.

TODO - is there a file explorer tool that can be used to explore the copied files?

TODO - a list of possible errors and remedial actions needs to be described.