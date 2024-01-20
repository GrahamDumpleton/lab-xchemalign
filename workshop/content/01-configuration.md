---
title: XChem Align - Configuration
---

This pages guides you through creating the vital configuration for running the XChem Align tools.
The result is a `config.yaml` page. Also, for generating the `xtalforms.yaml` file.

## Creating the config.yaml file

The configuration file is in YAML format. YAML is about as user-friendly as configuration files go,
(e.g. compared to XML or JSON) but still has some quirks that you need to know about.
Most importantly is that it's important to get the indentation correct, and to use spaces not tabs for
indenting. There are several guides to YAML on the web, for instance,
[this one](https://www.tutorialspoint.com/yaml/yaml_basics.htm).

*TODO - decide on how best to build the config.yaml file. For now we assume that we'll provide a generic template and 
walk the user through the process of editing it in the editor, but a smarter approach might be to "inject" sections into
it based on user input.*

First, let's create a directory to work in. We'll call it `work`.

```terminal:execute
command: mkdir -p work/inputs && mkdir work/outputs
```

In there we have a `inputs` directory where we'll copy the input files (using the **copier** tool) and a `output`
directory where the **collator*** and **aligner** tools will do their work. 

Now we'll create a configuration file. You can have multiple versions of your data, so in preparation for this we'll 
call the file `config_1.yaml`

```terminal:execute
command: cp ~/templates/config.yaml ~/work/outputs/config_1.yaml
```

And we'll start to edit this config file.

```editor:open-file
file: ~/work/outputs/config_1.yaml
```

Let's go through this file in sections.

The bits in angle brackets will need to be edited. Other bits *may* also need editing.

Firstly, this bit:

```editor:select-matching-text
file: ~/work/outputs/config_1.yaml
text: "<target-name>"
description: |
  target_name: <target-name>
```

Replace `<target-name>` with the name of your target. This will be the name that will be used in Fragalysis.

Now edit the `scp` section. This defines how the files are copied from Diamond, and assumes you have a Diamond FedID and access to the Diamond filesystem where the data resides.

First you need to replace the `<your-diamond-fedid>` with your FedID.

```editor:select-matching-text
file: ~/work/outputs/config_1.yaml
text: "<your-diamond-fedid>"
description: |
  username: <your-diamond-fedid>
```

The configuration file is configured to expect a copy of the SSH private key corresponding to the public SSH key you have uploaded to Diamond, in the location `~/.ssh/id_rsa-ssh.diamond.ac.uk` of this environment. You will need to upload this SSH provate key file.

```files:upload-file
path: .ssh/id_rsa-ssh.diamond.ac.uk
```

Hint: you might want to create a new SSH keypair for this purpose.

After uploading the SSH private key, you will need to make sure permissions are set correctly.

```terminal:execute
session: 1
command: chmod 0400 ~/.ssh/id_rsa-ssh.diamond.ac.uk
```

After editing, it might look a bit like this:

```yaml
scp:
  server: ssh.diamond.ac.uk
  username: abc12345
  key: ~/.ssh/id_rsa-ssh.diamond.ac.uk
  base_dir: /
```

etc. etc. for editing the rest of the config.yaml.

## Creating the xtalforms.yaml file.

*NOTE - we could defer generating the xtalforms.yaml to the aligner step, or have it as a separate step that is run
prior to the aligner step.*

You need to have the information to hand on your target's crystal forms and macromolecular assemblies. This information
needs to be defined in the `xtalforms.yaml` file. Use one of the below templates which cover basic scenarios, but for
other cases you will need to make more extensive changes.

Case 1: Single crystal form and single chain:
```terminal:execute
command: cp ~/templates/xtalforms-simple.yaml work/outputs/xtalforms.yaml
```

Case 2:: single crystal form and two chains:
```terminal:execute
command: cp ~/templates/xtalforms-2-chains.yaml work/outputs/xtalforms.yaml
```

TODO - provide other templates.

Whichever xltalforms template you used you will now need to edit it.
```editor:open-file
file: ~/work/outputs/xtalforms.yaml
```

For instance, in case 1, your `xtalforms.yaml` will look like this:

```yaml
assemblies:
  monomer:
    reference: <reference-structure>
    biomol: A
    chains: A
xtalforms:
  xtalform1:
    reference: <reference-structure>
    assemblies:
      1:
        assembly: monomer
        chains: A
```

For each assembly and xtalform you need to define the corresponding reference structure. This is the structure to which
crystals corresponding to that assembly and xtalform will be aligned.

Also, if your proteins are not chain A then you will need to change that.

TODO - describe editing the `xtalforms.yaml` file in more detail.

## Next steps

With the `config_1.yaml` and `xtalforms.yaml` files, we are now ready for the next step.
