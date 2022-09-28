# How to generate these reports

We suggest you to use Ubuntu 20.04 to avoid additional complications.

Install the following packages from apt:

```
sudo apt-get install build-essential python3.8-dev qt5-default python3-pyqt5.qtwebengine libpq-dev postgresql
```

To reproduce each table in the paper, look at the following online reports in the FuzzBench service:

+ Tab 1: https://www.fuzzbench.com/reports/experimental/2021-12-17-afl-edges-bug/index.html
+ Tab 2: https://www.fuzzbench.com/reports/experimental/2021-12-17-afl-edges/index.html
+ Tab 3: https://www.fuzzbench.com/reports/experimental/2021-12-16-afl-fitness-bug/index.html
+ Tab 4: It is contained in https://www.fuzzbench.com/reports/experimental/2022-05-06-dissecting/index.html, which is a cumulative experiment that was divided. https://eurecom-s3.github.io/dissecting_afl/reports/report_culling/ is the report for this single experiment.
+ Tab 5: Same as Tab 4, the produced report is https://eurecom-s3.github.io/dissecting_afl/reports/report_score/
+ Tab 6: https://www.fuzzbench.com/reports/experimental/2022-06-08-dissecting/index.html
+ Tab 7: https://www.fuzzbench.com/reports/experimental/2022-08-04-afl-new-splicing/index.html
+ Tab 8: Same as Tab 4, the produced report is https://eurecom-s3.github.io/dissecting_afl/reports/report_trimming/
+ Tab 9: Same as Tab 4, the report is https://eurecom-s3.github.io/dissecting_afl/reports/report_timeout/
+ Tab 10: Same as Tab 4, the report is https://eurecom-s3.github.io/dissecting_afl/reports/report_collisions/

The average normalized scores of https://www.fuzzbench.com/reports/experimental/2022-05-06-dissecting/index.html don't match as the score is normalized over the results of all the fuzzers, while we need a 1 vs 1 comparison most of the times (e.g. AFL vs AFL collision free). 
We need then to generate an individual report with a subset of the fuzzers starting from 2022-05-06-dissecting running the report generation script of fuzzbench and then we will get a report with only the chosen fuzzers.

The steps are:

1) Download the raw data (data.csv.gz) from the experiment https://www.fuzzbench.com/reports/experimental/2022-05-06-dissecting/data.csv.gz
2) Download the fuzzbench repo at https://github.com/google/fuzzbench and create a folder called 'report' in its root, then put data.csv.gz in such folder
3) Install the python dependencies with `pip install -r requirements.txt`
4) Open a terminal in the fuzzbench root folder and type 'PYTHONPATH=. python3 analysis/generate_report.py -q -f afl afl_something... -c my-experiment-name' changing the fuzzers after the -f argument to produce reports for the different tables.
5) Open the generated report/index.html in a browser and check the 'By avg. score' table

To make your life easier, to generate all the reports derived from the cumulative one the commands are:

+ Tab 4: PYTHONPATH=. python3 analysis/generate_report.py -q -f afl afl_no_favored afl_no_favfactor -c culling
+ Tab 5: PYTHONPATH=. python3 analysis/generate_report.py -q -f afl afl_score_random afl_score_max afl_score_min afl_score_no_novel_prioritization -c score
+ Tab 8: PYTHONPATH=. python3 analysis/generate_report.py -q -f afl afl_no_trim -c trimming
+ Tab 9: PYTHONPATH=. python3 analysis/generate_report.py -q -f afl afl_double_timeout -c timeout
+ Tab 10: PYTHONPATH=. python3 analysis/generate_report.py -q -f afl afl_collision_free -c collisions

Save the generated report folder each time you execute one of these commands otherwise the following one will overwrite the previously generated report.
