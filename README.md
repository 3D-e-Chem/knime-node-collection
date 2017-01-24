KNIME feature for all 3D-e-Chem nodes.

[![Build Status](https://travis-ci.org/3D-e-Chem/knime-node-collection.svg?branch=master)](https://travis-ci.org/3D-e-Chem/knime-node-collection)

This project uses [Eclipse Tycho](https://www.eclipse.org/tycho/) to perform build steps.

# Installation of 3D-e-Chem KNIME nodes

Requirements:

* KNIME, https://www.knime.org, version 3.1 or higher

Steps to get the 3D-e-Chem nodes inside KNIME:

1. Goto Help > Install new software ... menu
2. Press add button
3. Fill text fields with `https://3d-e-chem.github.io/knime-node-collection`
4. Select --all sites-- in `work with` pulldown
5. Select `3D-e-Chem KNIME nodes`
6. Install software
7. Restart KNIME

# Background

Each KNIME node developed in the 3D-e-Chem project has it own Github repository Eclipse feature and Eclipse plugin.

The update site `https://3d-e-chem.github.io/updates` contains the Eclipse features of all the 3D-e-Chem developed nodes.
When using this update site in KNIME, it will list all the nodes by their repository.

The update site `https://3d-e-chem.github.io/knime-node-collection` contains a single Eclipse feature which combines all the 3D-e-Chem developed nodes. When using this update site in KNIME, it will list a single feature for all 3D-e-Chem nodes.

Cons:

* New nodes need to be tracked in the feature/feature.xml file
* Each update of a node requires a new release of this repo aswell
* License is for all nodes together instead of separate license for each node
* Maintenance overhead of 2 update sites (1. only 3D-e-Chem nodes feature, 2. set of 3D-e-Chem node features)

Pros:

* Single checkbox to install all 3D-e-Chem nodes
* Easy to integrate into KNIME Community Contributions update site (https://tech.knime.org/book/general-instructions)

# Adding a new KNIME node

To include a KNIME node into the 3D-e-Chem KNIME nodes feature, it's plugin must be added to config file called `feature/feature.xml`.

Note! The node must be available in the `https://3d-e-chem.github.io/updates` update site.

# Releasing a new version of a KNIME node

The updated KNIME node can be included in the 3D-e-Chem nodes feature by creating a (new release)[#new-release], see below.

Note! The new version of the node must be available in the `https://3d-e-chem.github.io/updates` update site.

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

1. Make sure all included plugins are up to date on https://3d-e-chem.github.io/updates
2. Update versions in pom files with

```
mvn org.eclipse.tycho:tycho-versions-plugin:set-version -DnewVersion=<version>
```

3. Update `docs/` directory with new update site using

```
mvn install
```

4. Commit and push changes.
