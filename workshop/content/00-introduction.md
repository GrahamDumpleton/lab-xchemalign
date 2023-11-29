---
title: XChem Align - Introduction
---

This page provides an introduction to the XChem Align process and tools, as well as expectations for
what's needed in terms of data and configuration to go through the process.
It is purely textual with no clickable actions.

Probably there are two version of this workshop. One with pre-prepared data where all the configuration is known 
up-front (acting purely as a training workshop), the second where the user provides their own data (where the workshop
is acting as a guided assistant).

## What you need before you start.

You need to know:

### Which XChem 'visits' contain your data
This might be a single visit, or data from multiple visits. A visit will typically be located on the Diamond filesystem
at a place like `/dls/labxchem/data/xyz123456`.

You will need this information as part of the `config.yaml` configuration
file you will create in the next section.

We will refer to one of these locations as a **visit dir**.

### Which PanDDAs event maps to use
You need to know which `pandda_inspect_events.csv` files contain information on the PanDDAs event maps that correspond
to your crystals. These will be in your **visit dir** probably at a location like
`processing/analysis/panddas/analyses/pandda_inspect_events.csv`, but there might be multiple of these files and you need
to know which one(s) to use for each visit.

You will need this information as part of the `config.yaml` configuration
file you will create in the next section.

### Crystal forms and macromolecular assemblies
You need to know the different crystal forms and macromolecular assemblies for your crystals. In the simplest case you
might have a single crystal form and the assembly is a monomer. You will need this information to generate the 
`xtalforms.yaml` file you will create in the next section.

## Ready to go?

Once you have the above information to hand you are ready to continue. The process will be:

1. Generate the configuration information
2. Run the **copier** tool to collect the data you need from Diamond
3. Run the **collator** tool to collate the files into the right locations and names to use
4. Run the **aligner** tool to generate the site alignments
5. View the aligned data to confirm that it's what you expect.
