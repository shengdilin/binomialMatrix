# DiFfuSR: Distortion-Free Swap-Randomization for Statistically-Testing Data Mining Results

![Java
CI](https://github.com/acdmammoths/DiFfuSR/actions/workflows/JavaCI.yml/badge.svg)
![LaTeX
CI](https://github.com/acdmammoths/DiFfuSR/actions/workflows/LaTeXCI.yml/badge.svg)
![LaTeX lint](https://github.com/acdmammoths/DiFfuSR/actions/workflows/LaTeXLint.yml/badge.svg)

Alex's thesis and hopefully a KDD'22 submission =)

## Software requirements

A recent [Java](https://www.java.com/en/) SDK,
[Maven](https://maven.apache.org/), and [Python 3](https://www.python.org/).

## Building

1. Enter the `code/` directory

```sh
cd code
```

2. Create the jar

```sh
mvn clean package
```

All commands below assume that the current working directory is `code/`.

## Driver

To run the driver:

```sh
java -cp target/DiFfuSR-1.0-SNAPSHOT-jar-with-dependencies.jar Driver \
  <datasetPath> <samplerType> <numSwaps> <numSamples> <minFreq> <numThreads> <seed> <resultsDir>
```

Driver arguments:

- `<datasetPath>`: the path to the dataset
  - A string
- `<samplerType>`: the type of sampler
  - `NaiveSampler`
  - `RefinedSampler`
  - `GmmtSampler`
- `<numSwaps>`: the number of swaps/steps to run in the chain
  - A positive integer
- `<numSamples>`: the number of samples to generate
  - A positive integer
- `<minFreq>`: the minimum frequency threshold for the frequent itemset mining
  algorithm
  - A number in the range [0, 1)
- `<numThreads>`: the number of threads to run the algorithm
  - A positive integer
- `<seed>`: a random seed for replication
  - A long
- `<resultsDir>`: the directory to output the results of the algorithm

## Experiments

Create a Python virtual environment and install necessary packages in order to
generate the figures:

```sh
python3 -m venv venv
source venv/bin/activate
pip install -r experiments/figures/requirements.txt
```

To deactivate the virtual environment later:

```sh
deactivate
```

Experiment results will be written to `experiments/results/` and figures will be
saved to `experiments/figures/images/`.

### Run all experiments

To replicate all our experiments:

```sh
./run_experiments.sh -t all
```

### Run experiment type

To run a specific type of experiment with all the configuration files in
`experiments/confs/<experiment_type>/`:

```sh
./run_experiments.sh -t <experiment_type>
```

Possible values for `<experiment_type>`:

- `distortion`: run distortion experiment
- `runtime`: run step time experiment
- `scalability`: run scalability experiment
- `convergence`: run convergence experiment
- `numFreqItemsets`: run number of frequent itemsets experiment
- `sigFreqItemsets`: run significant frequent itemsets experiment

### Run single experiment

To run a specific type of experiment with a single configuration file:

```sh
java -cp target/DiFfuSR-1.0-SNAPSHOT-jar-with-dependencies.jar \
  <experiment_class> path/to/configuration/file
```

Possible values for `<experiment_class>`:

- `DistortionExperiment`: run distortion experiment
- `RuntimeExperiment`: run step time or scalability experiment
- `ConvergenceExperiment`: run convergence experiment
- `NumFreqItemsetsExperiment`: run number of frequent itemsets experiment
- `SigFreqItemsetsExperiment`: run significant frequent itemsets experiment

## Test suite

To run the test suite:

```sh
mvn test
```

## License

Copyright (C) 2022 Alexander Lee and Matteo Riondato

The code under `code/` is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by the Free
Software Foundation, either version 3 of the License, or (at your option) any
later version.

The code under `code/` is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the [GNU General Public
License](./LICENSE) (also available
[online](https://www.gnu.org/licenses/gpl-3.0.en.html)) for more details.
