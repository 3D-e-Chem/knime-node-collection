KNIME feature for all 3D-e-Chem nodes.

[![Build Status](https://travis-ci.org/3D-e-Chem/knime-node-collection.svg?branch=master)](https://travis-ci.org/3D-e-Chem/knime-node-collection)

The 3D-e-chem project of the Netherlands eScience Center, VU Medicinal Chemistry, CMBI Radboud University made a set of KNIME nodes listed at https://www.knime.com/3d-e-chem-nodes-for-knime, this repository combines all the nodes into a single feature which can be installed from the
[community contributions update site](https://www.knime.com/community).

This project uses [Eclipse Tycho](https://www.eclipse.org/tycho/) to perform build steps.

# Installation of 3D-e-Chem KNIME nodes

Requirements:

* KNIME, https://www.knime.org, version 3.5 or higher

Steps to get the 3D-e-Chem nodes inside KNIME:

1. Goto File > Install KNIME extensions ... menu
2. Expand the `KNIME Community nodes - Cheminformatics` folder
3. Select `3D-e-Chem KNIME nodes`
4. Install software
5. Restart KNIME

Some nodes need Python packages, those nodes have install instructions in their node description and print a warning when attempting to run them without the required Python package.

# Setup

Each KNIME node developed in the 3D-e-Chem project has it own Github repository, Eclipse feature and Eclipse plugin.

The update site `https://3d-e-chem.github.io/updates` contains the Eclipse features of all the 3D-e-Chem developed nodes.
When using this update site in KNIME, it will list all the nodes by their repository.

This update site `https://3d-e-chem.github.io/knime-node-collection` contains a single Eclipse feature which combines all the 3D-e-Chem developed nodes.
When using this update site in KNIME, it will list a single feature for all 3D-e-Chem nodes.

Cons of using this repo:

* New nodes need to be tracked in the feature/feature.xml file
* Each update of a node requires a new release of this repo aswell
* License is for all nodes together instead of separate license for each node
* Maintenance overhead of 2 update sites (1. only one 3D-e-Chem nodes feature, 2. set of 3D-e-Chem node features)

Pros of using this repo:

* Single checkbox to install all 3D-e-Chem nodes
* Integrated into KNIME Community Contributions update site under `KNIME Community nodes - Cheminformatics` folder. Users do not need to configure an extra update site.

So to have the latest version of each node you should use `https://3d-e-chem.github.io/updates`, but for stable releases use `https://3d-e-chem.github.io/knime-node-collection`.

# Adding a new KNIME node

To include a KNIME node into the 3D-e-Chem KNIME nodes feature, it's plugin(s) and optional 3D-e-Chem dependencies must be added to the `feature/feature.xml` file.
Followed by making a [new release](#new-release), see below.

# Adding a new version of a KNIME node

The updated KNIME node can be included in the 3D-e-Chem nodes feature by making a [new release](#new-release), see below.

# Build

```
mvn verify
```

An Eclipse update site will be made in `p2/target/repository` repository.
The update site can be used to perform a local installation.

# Development

Steps to get development environment setup:

1. Download KNIME SDK from https://www.knime.org/downloads/overview
2. Install/Extract/start KNIME SDK
3. Start SDK
4. Install m2e (Maven integration for Eclipse)

    1. Goto Help > Install new software ...
    2. Make sure Update site is http://update.knime.org/analytics-platform/3.1 and https://3d-e-chem.github.io/updates are in the pull down list otherwise add it
    3. Select --all sites-- in work with pulldown
    4. Select m2e (Maven integration for Eclipse)
    6. Install software & restart

5. Import this repo as an Existing Maven project

During import the Tycho Eclipse providers must be installed.

# New release

1. Make sure the local clone of this repo is up to date using

    ```
    git pull
    ```

2. Make sure all included plugins are up to date on https://3d-e-chem.github.io/updates or https://github.com/3D-e-Chem/3D-e-Chem.github.io/tree/master/updates
3. Learn current version by looking in `./pom.xml` file for the `<version>x.y.z-SNAPSHOT</version>` tag.
4. Increase version. Increase minor version when KNIME node has been added. Increase patch version when KNIME node has been updated. Use following command to update multiple xml files with the new version.

    ```
    mvn org.eclipse.tycho:tycho-versions-plugin:set-version -DnewVersion=<new version>-SNAPSHOT
    ```

5. Commit changes
6. Update `docs/` directory with new update site using

    ```
    mvn install
    ```

7. Stage new files, commit and push changes.

    ```
    git add docs/
    git commit -a
    git push
    ```

8. For major or minor release

  * add message to https://www.knime.com/forum/3d-e-chem-nodes
  * create a GitHub release and DOI entry
