# Mutexion Compressor

This repository contains the source codes of the Mutexion compressor and sample web pages for demos.

We implemented the Mutexion compressor based on [zlib 1.2.11](https://github.com/madler/zlib)


# How to build and run the compressor

The following instructions assume that this repository has been cloned into the `$HOME/mutexion_repository` directory.

We tested these instructions on 64-bit Ubuntu 20.04 LTS with the `build-essential` package (including `gcc`, `make`, etc.) installed.

To build the executables, run the following command inside the `$HOME/mutexion_repository/mutexion` directory:

```shell
$ make clean all
```

## Preprocessing web page

Before running the compressor for a sample web page (e.g., `$HOME/mutexion_repository/samples/addressbook_contact.html`), we first need to preprocess the web page with the `markers_to_brs` program to parse the taint markers in the web page and generate an input file to be compressed without markers.

```shell
$ cd $HOME/mutexion_repository
$ mutexion/markers_to_brs ./samples/addressbook_contact.html
```

Running the above command will generate 3 files:

- `$HOME/mutexion_repository/samples/addressbook_contact.html.nomarkers`, the resulting file after parsing and removing the taint markers from `addressbook_contact.html`
- `$HOME/mutexion_repository/brs_input` containing the `nextUserInput[]` array in the compression algorithm pseudocode
- `$HOME/mutexion_repository/brs_secret` containing the `nextSecret[]` array in the compression algorithm pseudocode

## Compressing web page

Then, inside the `$HOME/mutexion_repository` directory, run the compressor as follows:

```shell
$ mutexion/minigzip ./samples/addressbook_contact.html.nomarkers
```

Running the above command will generate the compressed web page, i.e., `$HOME/mutexion_repository/samples/addressbook_contact.html.nomarkers.gz`.

## Decompressing web page

Then, by running the following command, you can recover `$HOME/mutexion_repository/samples/addressbook_contact.html.nomarkers` by decompressing `$HOME/mutexion_repository/samples/addressbook_contact.html.nomarkers.gz`.

```shell
$ mutexion/minigzip -d ./samples/addressbook_contact.html.nomarkers.gz
```

# Authors
- Sangwon Hyun (shyun@mju.ac.kr), Myongji University
- Taegeun Moon (taegeun@skku.edu), Sungkyunkwan University
- Hyoungshick Kim (hyoung@skku.edu), Sungkyunkwan University








