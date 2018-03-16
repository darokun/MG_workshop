# Kraken

## Kraken algorithm summary
* Chop genomes into k-mers and link to a taxonomic id
* Chop read into k-mers and search for exact hits in the database
* Search for the highest-weighted root-to-leaf paths and assign the taxonomic id of the lowest node to the read

## Build a standard database
* Containts complete Archaea, Bacteria and Viral genome in RefSeq
* Need 75 GB of memory to build and run
* Depending on the computational resources, this can take a few hours

`kraken-build --db standardDB --threads 10 --standard`
* `kraken-build --db`: command to build the database
* `standardDB`: location for building database
* `--threads 10`: computational power/threads
* `--standard`: type of database

## Build custom database
```
kraken-build --db customDB --download-taxonomy
kraken-build --db customDB --download-library bacteria # possible choices: archaea, bacteria, plasmid, viral, human.
...
kraken-build --db customDB --threads 10 --build
```
* To add other genomes: `kraken-build --db customDB add-to-library customGenome.fna`

## Running Kraken
Files to have in the folder:
* Reads: example_R1.fastq, example_R2.fastq
* Database: minikraken_20141208      
`kraken --db minikraken_20141208 --thread 2 --paired --output example.kraken example_R1.fastq example_R2.fastq`

* Transform to Kraken reports:
`kraken-report --db minikraken_20141208 example.kraken > example.report`

* Then, visualize the report using Pavian in R:
```
R
pavian::runApp()
```



