```
https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html
```
## Why use conda
Anaconda and Miniconda provide stable python packages but they can be not the leading version
the repository can be found at https://repo.continuum.io/pkgs/

## Installing Miniconda
The anaconda software can be downloaded from https://www.anaconda.com/distribution/
The miniconda software can be downloaded from https://repo.anaconda.com/miniconda/
```
$ sudo su - dataupdate
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
$ /bin/bash Miniconda3-latest-Linux-x86_64.sh
```

## List conda environment 
In the example below a newly created conda environment is crated for the dataupdate user
```
$ sudo su - dataupdate
$ conda env list

base                  *  /home/dataupdate/miniconda3
assignee-grouping        /home/dataupdate/miniconda3/envs/assignee-grouping
cache-fill               /home/dataupdate/miniconda3/envs/cache-fill
cipher-dbsync            /home/dataupdate/miniconda3/envs/cipher-dbsync
data-update              /home/dataupdate/miniconda3/envs/data-update
influxdb-metrics         /home/dataupdate/miniconda3/envs/influxdb-metrics
most-recent              /home/dataupdate/miniconda3/envs/most-recent
t1                       /home/dataupdate/miniconda3/envs/t1
usagestats               /home/dataupdate/miniconda3/envs/usagestats
uspto-bulk-parsing       /home/dataupdate/miniconda3/envs/uspto-bulk-parsing
xl                       /home/dataupdate/miniconda3/envs/xl
```

## Create conda environment
In the example below a new environment is created called aws-metrics with a python 3.7 environment and the boto3 package installed. 
```
$ conda create -n aws-metrics python=3.7 boto3
```
Listing the conda environments shows the newly created environment
```
$ conda env list

base                  *  /home/dataupdate/miniconda3
assignee-grouping        /home/dataupdate/miniconda3/envs/assignee-grouping
aws-metrics				 /home/dataupdate/miniconda3/envs/aws-metrics
cache-fill               /home/dataupdate/miniconda3/envs/cache-fill
cipher-dbsync            /home/dataupdate/miniconda3/envs/cipher-dbsync
data-update              /home/dataupdate/miniconda3/envs/data-update
influxdb-metrics         /home/dataupdate/miniconda3/envs/influxdb-metrics
most-recent              /home/dataupdate/miniconda3/envs/most-recent
t1                       /home/dataupdate/miniconda3/envs/t1
usagestats               /home/dataupdate/miniconda3/envs/usagestats
uspto-bulk-parsing       /home/dataupdate/miniconda3/envs/uspto-bulk-parsing
xl                       /home/dataupdate/miniconda3/envs/xl
```
## Activate conda environment and install a package
Once the environment has been created it can be activated as shown below and pip can be used deploy additional packages in the environment
```
conda activate aws-metrics
pip install redis
```

## Deactivate a conda environment
To leave an environment we just deactivate
```
conda deactivate aws-metrics
```

## Using an environment with a cron job
Below is an example of using /etc/cron.d/ to trigger the execution of a python file using the aws-metrics conda environment
```
# This gets the size of the custom-classifiers task queues from Redis, and writes the data to AWS Cloudwatch.

SHELL=/bin/bash
MAILTO="mark.day@aistemos.com"
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/dataupdate/miniconda3/bin

*/5 * * * *  dataupdate source activate aws-metrics && /mnt/data/cc_queue_metrics/log-queue-metrics-aws
```
