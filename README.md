# Riak - BOSH Release
A BOSH release for deploying Riak clusters.

This project is based on [BrianMMcClain/riak-release](https://github.com/BrianMMcClain/riak-release) and https://github.com/cloudfoundry/cf-riak-cs-release.

Setup 
==
This guide assumes you have a working bosh environment, for help see https://bosh.io/docs/deploy-microbosh-to-aws.html

Deploy Riak
==

```
git clone https://github.com/basho-labs/riak-cf-bosh
cd riak-cf-bosh
mkdir tmp
cp example/bosh-aws.yml tmp/
vi tmp/bosh-aws.yml
```
Edit config values for your environment:
##### Set the uuid 
(run bosh status to obtain this)
```
  director_uuid: 42e99fc6-2c3b-4c20-8e72-f83jdu283jd2d313
```  

##### Set the availability zone
( the zone in which bosh is deployed)
```
  availability_zone: us-east-1d
```
##### Set the subnet id

Set the subnet to the network created when deploying bosh to AWS.
(for more information see https://bosh.io/docs/deploy-microbosh-to-aws.html)
```
  subnet: subnet-6c892647
```

##### Download stemcell

###### Note: Riak package is currently only built for Ubunty Trusty

```
bosh public stemcells
bosh download public stemcell bosh-aws-xen-ubuntu-trusty-go_agent
bosh upload stemcell bosh-stemcell-2941-aws-xen-ubuntu-trusty-go_agent.tgz
```
##### Upload release
```
bosh deployment tmp/bosh-aws.yml
bosh create release --force
bosh upload release
```
##### Deploy release
```
bosh deploy
```

