# [SHAREing](https://shareing-dri.github.io) directory of HPC testbeds

The aim of this repository is to collate information about
all available testbeds and production HPC systems in the UK
providing accelerated compute.

The live directory is available at
<https://shareing-dri.github.io/hpc-testbeds>

If you are aware of a system available to UK researchers
that is not listed in the directory,
please add it!

## Adding your system

To add a new system,
first please check the criteria for inclusion below,
and then follow either of the following sets of instructions:

### Using Git at the command line

1. Fork this repository.
2. Clone your fork:

       git clone git@github.com:yourusername/hpc-testbeds

3. Create a new copy of the template `_systems/system-template`,
   making sure to use the extension `.md`:

       cp _systems/system-template _systems/my-awesome-system.md

4. Fill out the fields listed in
   the block at the top of the file surrounded by `---`.
5. Add as much or as little text description of the system as you like,
   below the `---` block.
   Examples of things to include are described in the template.
6. Commit this file to the repository and push to your fork:

       git add _systems/my-awesome-system.md
       git commit -m "add My Awesome System"

7. If you are adding multiple systems as part of the same cluster
   (for example,
   if you there are multiple diverse partitions),
   repeat the above steps 3&ndash;6 for each system.
8. Open a pull request to the `SHAREing-dri/hpc-testbeds` repository.

### Using GitHub on the web

1. Go to the [`_systems` directory](_systems/)
2. Click `Add file` > `+ Create new file`
3. When prompted by GitHub,
   create a fork in which to make your changes.
4. Give your new file a name ending `md`;
   for example,
   `my-awesome-system.md`.
4. Copy the contents of the file
   [`_systems/system-template`](_systems/system-template)
   into your new file.
4. Fill out the fields listed in
   the block at the top of the file surrounded by `---`.
5. Add as much or as little text description of the system as you like,
   below the `---` block.
   Examples of things to include are described in the template.
6. Commit this file to the repository.
7. When prompted by GitHub,
   open a pull request to the `SHAREing-dri/hpc-testbeds` repository.

## Updating system information

Pull requests to update system information where this has changed are encouraged.
   
## Inclusion criteria

To be included in this directory,
a system should:

- Be currently running, or to become available soon.
  - Information on existing systems may be retained when they are decommissioned,
    but additional decommissioned systems will not be added to the directory.)
- Be in the UK or accessible to UK researchers.
  - For example,
    EuroHPC systems to which the UK subscribes would be in scope;
    systems at US National Labs requiring a US collaborator to gain access would not.
- Be accessible to researchers from outside the system owner's research group
  via some defined process.
  - A "defined process" may be "send an email request",
    provided this is made explicit in the system description;
    a formal application form or similar bureaucracy are not required.
- Make use of one or more accelerator technologies
  - A GPU cluster or FPGA testbed would be in scope;
    a pure CPU cluster would not.

If you are not part of
the technical team managing the system you are providing information on,
please also provide details of
a contact with whom we can confirm the correctness of the information.
