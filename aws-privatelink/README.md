# aws-privatelink

* The [terraform](./terraform) directory contains a method to setup an AWS
Private Link with Confluent Cloud.

* The [dns-endpoints.sh](./dns-endpoints.sh) script runs the AWS CLI
commands to emit the correct DNS Zone records for a specific VPC Endpoint.

* The [debug-connectivity.sh](./debug-connectivity.sh) script runs commands
that should be sent to Confluent Cloud support to assist with verification
of Private Link Setup.

## Using Docker

You can also run the script `debug-connectivity.sh` and `dns-endpoints.sh` using Docker:

* Using Credentials file:

```bash
$ docker run --rm -it -v $HOME/.aws:/home/appuser/.aws vdesabou/ccloud-connectivity debug-connectivity.sh <bootstrap> <api-key>
```

```bash
$ docker run --rm -it -v $HOME/.aws:/home/appuser/.aws vdesabou/ccloud-connectivity dns-endpoints.sh <VPC Endpoint>
```

* Using environment variables

This is supported, although NOT encouraged, as the environment variables can end up in command-line history, available for container inspection, etc.

```bash
$ docker run --rm -it -e AWS_ACCESS_KEY_ID=my-key-id -e AWS_SECRET_ACCESS_KEY=my-secret-access-key vdesabou/ccloud-connectivity debug-connectivity.sh <bootstrap> <api-key>
```

```bash
$ docker run --rm -it -e AWS_ACCESS_KEY_ID=my-key-id -e AWS_SECRET_ACCESS_KEY=my-secret-access-key vdesabou/ccloud-connectivity dns-endpoints.sh <VPC Endpoint>
```

The [vdesabou/ccloud-connectivity](https://hub.docker.com/repository/docker/vdesabou/ccloud-connectivity) image is based on [confluentinc/cp-kafkacat](https://hub.docker.com/r/confluentinc/cp-kafkacat), therefore it's RHEL8 based image which contains kafkacat and several other tools like awscli, netstat, nc, openssl, dig, etc..

Example:

```bash
$ docker run --rm -it vdesabou/ccloud-connectivity dig https://www.confluent.io
```

```bash
$ docker run --rm -it -v $HOME/.aws:/home/appuser/.aws vdesabou/ccloud-connectivity aws configure
```
