# Spark Streaming Example Project

[![Build Status](https://travis-ci.org/snowplow/spark-example-project.png)](https://travis-ci.org/snowplow/spark-example-project) [ ![Release] [release-image] ] [releases] [ ![License] [license-image] ] [license]

## Introduction

This is a simple time series analysis job written in Scala for the [Spark] [spark] Streaming cluster computing platform.
__First__, this app generates/sends raw events to AWS Kinesis. __Second__, we process the raw events with Apache Spark Streaming. Our data processing
sorts each event into a "bucket". __Third__, Spark counts and aggregates the raw events into 1 minute buckets. __Last__, this Spark app takes the aggregate records and saves the aggregate events into AWS DynamoDB Database. Read More about 
[Kinesis and Spark Streaming](https://spark.apache.org/docs/latest/streaming-kinesis-integration.html).
Follow along in this [blog post] (http://snowplowanalytics.com/blog/2015/06/05/spark-streaming-example-project-0.1.0-released/) to get the project up and running yourself.

Input: Example of a raw events in JSON format

```bash
{ "dateString": "2015-06-22T00:23:24.306091", "eventType": "Red" }
{ "dateString": "2015-06-22T00:23:24.450129", "eventType": "Yellow" }
{ "dateString": "2015-06-22T00:23:24.826703", "eventType": "Blue" }
```

Output: Example of the AggregateRecords table in DynamoDB
![data table png][data-table]


This was built by the Data Science team at [Snowplow Analytics] [snowplow], who use Spark on their [Data pipelines and algorithms] [data-pipelines-algos] projects.

Please ensure your AWS credentials have access policies assigned to use Cloudwatch, Kinesis, and DynamoDB services.

We assume you have an Internet connection so we can access services and download code from github. Also, you will need git, Vagrant and VirtualBox installed locally. This project is specifically configured to run in AWS region "us-east-1" to ensure all AWS services are available. Building Spark on a vagrant box requires RAM. Ensure you have at least 8GB of RAM and 64 bit OS hosting vagrant.

** Running this requires an Amazon AWS account, and it will incur charges **
	
	
# Quickstart for those who have Apache Spark already compiled with Kinesis

## Step 1 - Cloning Spark-Streaming-Example-Project

```bash
host> git clone repo
```

## Step 2 - Building Spark-Streaming-Example-Project

```bash
host> sbt assembly
```

The 'fat jar' is now available as:

```bash
target/scala-2.10/simple-project_2.10-0.1.jar
```

## Step 3 - Running Spark-Streaming-Example-Project on Local

```bash
$SPARK_HOME/bin/spark-submit --class com.snowplowanalytics.spark.streaming.StreamingCountsApp \
                             --master local[2] \
                             spark-streaming-example-project/target/scala-2.10/spark-streaming-example-project-0.1.0.jar \
                             --config spark-streaming-example-project/src/main/resources/config.hocon.sample
```

## Next steps

Fork this project and adapt it into your own custom Spark job.

To invoke/schedule your Spark job on EMR, check out:

* [Spark Plug] [spark-plug] for Scala
* [Elasticity] [elasticity] for Ruby
* [Boto] [boto] for Python
* [Lemur] [lemur] for Clojure

## Roadmap

* Spark Streaming Machine Learning example

## Copyright and license

Copyright 2013-2015 Snowplow Analytics Ltd.

Licensed under the [Apache License, Version 2.0] [license] (the "License");
you may not use this software except in compliance with the License.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

[spark]: http://spark-project.org/
[wordcount]: https://github.com/twitter/scalding/blob/master/README.md
[snowplow]: http://snowplowanalytics.com
[data-pipelines-algos]: http://snowplowanalytics.com/services/pipelines.html

[vagrant-install]: http://docs.vagrantup.com/v2/installation/index.html
[virtualbox-install]: https://www.virtualbox.org/wiki/Downloads

[spark-streaming-example-project]: https://github.com/snowplow/spark-streaming-example-project
[scalding-example-project]: https://github.com/snowplow/scalding-example-project

[issue-1]: https://github.com/snowplow/spark-example-project/issues/1
[issue-2]: https://github.com/snowplow/spark-example-project/issues/2
[aws-spark-tutorial]: http://aws.amazon.com/articles/4926593393724923
[spark-emr-howto]: https://forums.aws.amazon.com/thread.jspa?messageID=458398

[emr]: http://aws.amazon.com/elasticmapreduce/
[hello-txt]: https://github.com/snowplow/spark-example-project/raw/master/data/hello.txt
[emr-client]: http://aws.amazon.com/developertools/2264

[elasticity]: https://github.com/rslifka/elasticity
[spark-plug]: https://github.com/ogrodnek/spark-plug
[lemur]: https://github.com/TheClimateCorporation/lemur
[boto]: http://boto.readthedocs.org/en/latest/ref/emr.html

[license-image]: http://img.shields.io/badge/license-Apache--2-blue.svg?style=flat
[license]: http://www.apache.org/licenses/LICENSE-2.0
[release-image]: http://img.shields.io/badge/release-0.1.0-blue.svg?style=flat
[releases]: https://github.com/snowplow/spark-streaming-example-project/releases
[data-table]: https://raw.githubusercontent.com/bigsnarfdude/snowplow.github.com/spark-streaming-example-project/assets/img/blog/2015/06/aggregateRecords2.png