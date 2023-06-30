# TI Product Type Baseline: Konnektor

This repository is part of a PoC demonstrator in order to conduct a feasibility study whether to utilize a git/flow based specification development methodology for the telematics infrastructure specification (TI) of the German federal health system.

The PoC utilises [sphinx](https://www.sphinx-doc.org/en/master/index.html) for describing the required specifications and the [sphinx-needs](https://sphinx-needs.readthedocs.io/en/latest/index.html) extension module to be able to manage requirements which is essential for specifying a robust system, targeted to process delicate personal data of about 80 million German citizens.

The content of this repository covers the configuration the product type baseline of the "Konnektor", which is an edge product type within the TI.
This baseline is realised by specifying the aggregation of several specification projects (additional repositories) in a so called [manifest file](default.xml). This file is intended to be used with the [google repo tool](https://gerrit.googlesource.com/git-repo/+/refs/heads/master/README.md) which will be used to automatically and reproducibly fetch all the required repositories, which are necessary to fully specify the product type and places those in a local workspace while respecting a well defined folder structure.

The baseline consisits of two parts:
1. The manifest.xml to assemble the [google repo tool](https://gerrit.googlesource.com/git-repo/+/refs/heads/master/README.md) based workspace for building the specifications.
2. The [sphinx-external-toc plugin](https://sphinx-external-toc.readthedocs.io/en/latest/intro.html) [_toc.yml] file, specifying which [sphinx-needs](https://sphinx-needs.readthedocs.io/en/latest/index.html) based source files have to be used how during the build process.

## Prerequisites

### Install the 'repo' tool

Before being able to use the content of this manifest repository, the [google repo tool](https://gerrit.googlesource.com/git-repo/+/refs/heads/master/README.md) needs to be locally installed.

With Ubuntu:

```
sudo apt-get install repo
```

Or manually:
```
mkdir -p ~/.bin
$ PATH="${HOME}/.bin:${PATH}"
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
$ chmod a+rx ~/.bin/repo
```

### Verify the installation

```
repo --version
```

## Assemble the workspace

In order to assemble the workspace according to the configuration of the [manifest file](default.xml), this repository has to be fetched from remote. This is being done by plain git command:

```
git clone git@github.com:muenzerik/manifest-telematik.git
```

You can initialize repo on this fetched repository. This creates a .repo/ directory with Git repositories for the Repo source code and the standard manifest files.

```
repo init -u <path-to-this-checked-out-repository>/konnektor-manifest -m default.xml
```

From the path where you executed the ``repo init`` command, do:

```
repo sync -c
```

Please also check the [repo docs](https://source.android.com/docs/setup/create/repo) to see what other stuff you are able to do with it and what options you might be able to use.

## Build the specification

The [sphinx-needs](https://sphinx-needs.readthedocs.io/en/latest/index.html) based build of the specification is not fully configured in this manifest repository. Only what files have to be used in which TOC tree is defined here. Format, structure, needs-objects, custom functions etc. are mostly defines somewhere else. However, there should be a repository defined in the manifest.xml, called ``spec-telematik``. There, you shall find all that missing stuff and you should be able to retrieve from the description there, how to build the full specification.

# NOTE:

This repository represents an experimental proof-of-concept.
Information and requirements are only test data and are neither normative nor legally binding.
The official normative documents of the TI are available here: https://fachportal.gematik.de