NLP Fall 2022 Final Project: Namas Mankad nkm9348 | Kevin Tong kt2653 | Haozhen Bo hb2432

See README_old.md for the original readme.

# How to run the code

The data files are in part/ and percentage/. The parse trees are inside gold_parses/.

First, you need to run the baseline code to generate the fancy features. To do so simply run `./main.py`. If you decide to run it yourself it would take you about 5 hrs so don't do it. Instead, run `tar -zxf backup.tar.gz` and `mv backup/* ./ && rm -r backup`. You'll find some .embedding and .features files inside the data folder. Those are the feature files generated by the baseline system. I compressed them because they are too large (800MB in total) to upload to GitHub but OK (50MB) for uploading after compression.

Next, you just run `python run.py` and wait for the result. On my computer it takes at most 2 minutes the first time it runs and less than a minute later (because I saved the extracted features from the baseline system as pickle files). To run the percent task instead of partitive task, simple comment and uncomment the lines for various filenames at the head of the file. To run the test set instead of dev set however, you need to manually change all four `dev.xxx` occurrences to `test.xxx` and run again. You should see a result of 77%+ on both dev and test sets.

To do ablation tests, you need to modify `get_data()` and delete those features you don't want. For example, if you want to remove path features, just change

``` python3
str_data = pd.concat([str_data, relation_feature, path_features], axis=1)
```

to

``` python3
str_data = pd.concat([str_data, relation_feature], axis=1)
```

And you will see in no time that the performance drops sharply to about 50%.

# Some results:

dev set F1 score: 77.46%

Running almost the same dataset with no one-hot encoding (aka running it with the baseline system): ~65%

Running without path features: 47.41%

Running without embedding and all the boolean features from baseline system: 77.0%

Running with only simple look-behind and look-ahead features: 39.47%




So it turns out that the things that matter here are:
* Path features. Even the most basic features such as the path between the two nodes would help a lot
* Implementing ML with correct practice (i.e. One-Hot Encoding!!!).
