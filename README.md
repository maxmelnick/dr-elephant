# Dr. Elephant

[![Build Status](https://api.travis-ci.org/linkedin/dr-elephant.svg)](https://travis-ci.org/linkedin/dr-elephant/)
[![Join the chat at https://gitter.im/linkedin/dr-elephant](https://badges.gitter.im/linkedin/dr-elephant.svg)](https://gitter.im/linkedin/dr-elephant?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

<a href=""><img src="images/wiki/dr-elephant-logo-150x150.png" align="left" hspace="10" vspace="6"></a>

**Dr. Elephant** is a performance monitoring and tuning tool for Hadoop and Spark. It automatically gathers all the metrics, runs analysis on them, and presents them in a simple way for easy consumption. Its goal is to improve developer productivity and increase cluster efficiency by making it easier to tune the jobs. It analyzes the Hadoop and Spark jobs using a set of pluggable, configurable, rule-based heuristics that provide insights on how a job performed, and then uses the results to make suggestions about how to tune the job to make it perform more efficiently.

## Configuring on EMR

1. Provision EMR cluster
2. Provision MySQL RDS instance and open port 3060 from EMR master
3. Add Security Group to EMR Master to enable 1) Internal SSH from bastion, 2) port 8080 traffic for Dr Elephant UI, 3) 18080 = Spark History Server UI, 4) 8890 = Zeppelin
4. SSH into Master and install Dr Elephant per [quick setup](https://github.com/linkedin/dr-elephant/wiki/Quick-Setup-Instructions-(Must-Read))

**HINTS**

```
cd ~
wget https://downloads.typesafe.com/typesafe-activator/1.3.12/typesafe-activator-1.3.12.zip
unzip typesafe-activator-1.3.12.zip
export ACTIVATOR_HOME=/home/hadoop/activator-dist-1.3.12
export PATH=$ACTIVATOR_HOME/bin:$PATH

sudo yum install nodejs npm --enablerepo=epel
sudo npm config set registry http://registry.npmjs.org/
sudo npm install -g bower

git clone https://github.com/maxmelnick/dr-elephant.git
cd dr-elephant
git checkout emrInstall
cd web/
bower install

export HADOOP_HOME=/usr/lib/hadoop
export SPARK_HOME=/usr/lib/spark
export SPARK_CONF_DIR=/usr/lib/spark/conf
export PATH=$HADOOP_HOME/bin:$PATH
export HADOOP_CONF_DR=/etc/hadoop/conf
export $HADOOP_CONF_DIR=/etc/hadoop/conf
export HADOOP_CONF_DIR=/etc/hadoop/conf

cd ..
./compile.sh

vim ~/dr-elephant/app-conf/elephant.conf

# Make sure ~/dr-elephant/app-conf/Fetcher.conf uses experimental Spark Fetcher that uses REST API for event log

cd dist/dr-elephant-2.1.7
./bin/start.sh ~/dr-elephant/app-conf

less ~/dr-elephant/dist/logs/elephant/dr_elephant.log
```

## Documentation

For more information on Dr. Elephant, check the wiki pages [here](https://github.com/linkedin/dr-elephant/wiki).

For quick setup instructions: [Click here](https://github.com/linkedin/dr-elephant/wiki/Quick-Setup-Instructions-(Must-Read))

Developer guide: [Click here](https://github.com/linkedin/dr-elephant/wiki/Developer-Guide)

Administrator guide: [Click here](https://github.com/linkedin/dr-elephant/wiki/Administrator-Guide)

User guide: [Click here](https://github.com/linkedin/dr-elephant/wiki/User-Guide)

Engineering Blog: [Click here](https://engineering.linkedin.com/blog/2016/04/dr-elephant-open-source-self-serve-performance-tuning-hadoop-spark)

## Mailing-list & Github Issues

Google groups mailing list: [Click here](https://groups.google.com/forum/#!forum/dr-elephant-users) (Reached upper limit! please create github issues)

Github issues: [click here](https://github.com/linkedin/dr-elephant/issues)

## Meetings

We have scheduled a weekly Dr. Elephant meeting for the interested developers and users to discuss future plans for Dr. Elephant. Please [click here](https://github.com/linkedin/dr-elephant/issues/209) for details.

## How to Contribute?

Check this [link](https://github.com/linkedin/dr-elephant/wiki/How-to-Contribute%3F).

## License

    Copyright 2016 LinkedIn Corp.

    Licensed under the Apache License, Version 2.0 (the "License"); you may not
    use this file except in compliance with the License. You may obtain a copy of
    the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
    WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
    License for the specific language governing permissions and limitations under
    the License.
