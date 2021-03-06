[![Build Status](https://travis-ci.org/JohnSnowLabs/spark-nlp.svg?branch=master)](https://travis-ci.org/JohnSnowLabs/spark-nlp)
# Spark-NLP
John Snow Labs Spark-NLP is a natural language processing library built on top of Apache Spark ML. It provides simple, performant & accurate NLP annotations for machine learning pipelines, that scale easily in a distributed environment.

# Project's website
Take a look at our official spark-nlp page: http://nlp.johnsnowlabs.com/ for user documentation and examples

# Slack community channel
Questions? Feedback? Request access sending an email to nlp@johnsnowlabs.com

# Usage

## spark-packages

This library has been uploaded to the spark-packages repository https://spark-packages.org/package/JohnSnowLabs/spark-nlp .

To use the most recent version just add the `--packages JohnSnowLabs:spark-nlp:1.6.0` to you spark command

```sh
spark-shell --packages JohnSnowLabs:spark-nlp:1.6.0
```

```sh
pyspark --packages JohnSnowLabs:spark-nlp:1.6.0
```

```sh
spark-submit --packages JohnSnowLabs:spark-nlp:1.6.0
```

## Jupyter Notebook

```
export SPARK_HOME=/path/to/your/spark/folder
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS=notebook

pyspark --packages JohnSnowLabs:spark-nlp:1.6.0
```

## Apache Zeppelin
This way will work for both Scala and Python
```
export SPARK_SUBMIT_OPTIONS="--packages JohnSnowLabs:spark-nlp:1.6.0"
```
Alternatively, add the following Maven Coordinates to the interpreter's library list
```
com.johnsnowlabs.nlp:spark-nlp_2.11:1.6.0
```

## Python without explicit Spark installation
If you installed pyspark through pip, you can now install sparknlp through pip
```
pip install --index-url https://test.pypi.org/simple/ spark-nlp==1.6.0
```
Then you'll have to create a SparkSession manually, for example:
```
spark = SparkSession.builder \
    .appName("ner")\
    .master("local[4]")\
    .config("spark.driver.memory","4G")\
    .config("spark.driver.maxResultSize", "2G") \
    .config("spark.driver.extraClassPath", "lib/sparknlp.jar")\
    .config("spark.kryoserializer.buffer.max", "500m")\
    .getOrCreate()
```

## Pre-compiled Spark-NLP and Spark-NLP-OCR
You may download fat-jar from here:
[Spark-NLP 1.6.0 FAT-JAR](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/spark-nlp-assembly-1.6.0.jar)
or non-fat from here
[Spark-NLP 1.6.0 PKG JAR](http://repo1.maven.org/maven2/com/johnsnowlabs/nlp/spark-nlp_2.11/1.6.0/spark-nlp_2.11-1.6.0.jar)
Spark-NLP-OCR Module (Requires native Tesseract 4.x+ for image based OCR. Does not require Spark-NLP to work but highly suggested)
[Spark-NLP-OCR 1.6.0 FAT-JAR](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/spark-nlp-ocr-assembly-1.6.0.jar)

## Maven central

Our package is deployed to maven central. In order to add this package as a dependency in your application:

#### Maven

```xml
<dependency>
  <groupId>com.johnsnowlabs.nlp</groupId>
  <artifactId>spark-nlp_2.11</artifactId>
  <version>1.6.0</version>
</dependency>
```

#### SBT
```sbtshell
libraryDependencies += "com.johnsnowlabs.nlp" % "spark-nlp_2.11" % "1.6.0"
```

If you are using `scala 2.11`

```sbtshell
libraryDependencies += "com.johnsnowlabs.nlp" %% "spark-nlp" % "1.6.0"
```

## Using the jar manually 

If for some reason you need to use the jar, you can download the jar from the project's website: http://nlp.johnsnowlabs.com/

From there you can use it in your project setting the `--classpath`

To add jars to spark programs use the `--jars` option

```sh
spark-shell --jars spark-nlp.jar
```

The preferred way to use the library when running spark programs is using the `--packages` option as specified in the `spark-packages` section.

## Downloading models for offline use

If you have troubles using pretrained() models in your environment, here a list to various models (only valid for latest versions).
If there is any older than current version of a model, it means they still work for current versions.

### Pipelines
* [Basic Pipeline](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/pipeline_basic_en_1.6.0_2_1530947669208.zip)
* [Advanced Pipeline](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/pipeline_advanced_en_1.6.0_2_1530947692578.zip)
* [Vivekn Sentiment Pipeline](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/pipeline_vivekn_en_1.5.4_2_1526672003128.zip)

### Models
* [PerceptronModel (POS)](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/pos_fast_en_1.6.0_2_1530947179686.zip)
* [ViveknSentimentModel (Sentiment)](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/vivekn_fast_en_1.5.3_2_1525275364141.zip)
* [SymmetricDeleteModel (Spell Checker)](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/spell_sd_fast_en_1.5.3_2_1525273109034.zip)
* [NorvigSweetingModel (Spell Checker)](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/spell_fast_en_1.5_2_1522181401412.zip)
* [NerDLModel (NER)](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/as_fast_dl_en_1.5.2_2_1525218818894.zip)
* [NerCRFModel (NER)](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/ner_precise_en_1.5_2_1522918062000.zip)
* [LemmatizerModel (Lemmatizer)](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/lemma_fast_en_1.5_2_1522181347222.zip)

# Special community aknowledgments
Thanks in general to the community who have been lately reporting important issues and pull request with bugfixes.
Community has been key in the last releases with feedback in various Spark based environments.

Here a few specific mentions for recurring feedback and slack participation
* @maziyarpanahi (https://github.com/maziyarpanahi) - For contributing with testing and valuable feedback
* @easimadi (https://github.com/easimadi) - For contributing with documentation and valuable feedback

# Contribute
We appreciate any sort of contributions:
* ideas
* feedback
* documentation
* bug reports
* nlp training and testing corpora
* development and testing

Clone the repo and submit your pull-requests! Or directly create issues in this repo.

# Contact
nlp@johnsnowlabs.com

# John Snow Labs
http://johnsnowlabs.com/
