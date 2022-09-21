# Dissecting American Fuzzy Lop - A FuzzBench Evaluation

This repo contains the code in the AFL/ folder and the artifacts to reproduce the experiments in the fuzzbench/ folder.
The reports with the output of the experiments is contained in the reports/ folder (online version at https://eurecom-s3.github.io/dissecting_afl/reports/).

To build all the AFL variants used in the paper follow the readme in the AFL/ folder, to run the experiments follow the fuzzbench documentation.
In the fuzzbench/fuzzers/ folder you find the fuzzers config used in the paper, while all the other fuzzers in fuzzbench were removed.

You can re-upload the fuzzers config to the FuzzBench service opening a PR and request an experiment (https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/#requesting-an-experiment) to reproduce our results.

Instead, to run the experiments locally, follow https://google.github.io/fuzzbench/running-a-local-experiment, but it needs a lot of time and computational power.

You can also re-generate the reports in the reports/ folder from the experiments on the FuzzBench service following the steps in [this document](reports/README.md).
