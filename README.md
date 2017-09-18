# Redis BOSH Release

This is a [BOSH](http://bosh.io/) release for [Redis](https://redis.io/), an open source, in-memory data structure store, used as a database, cache and message broker.

## Disclaimer

This is **NOT** a production ready [BOSH](http://bosh.io/) release. I created it for my own experimentation and it may not be supported in the future.

If you are looking for a supported [Redis](https://redis.io/) [BOSH](http://bosh.io/) release, please check the [bosh.io](http://bosh.io/releases) releases page or the [cloudfoundry-community](https://github.com/cloudfoundry-community) github organization.

## Table of Contents

* [Usage](https://github.com/frodenas/redis-boshrelease#usage)
  * [Requirements](https://github.com/frodenas/redis-boshrelease#requirements)
  * [Clone the repository](https://github.com/frodenas/redis-boshrelease#clone-the-repository)
  * [Basic deployment](https://github.com/frodenas/redis-boshrelease#basic-deployment)
  * [Operations files](https://github.com/frodenas/redis-boshrelease#operations-files)
  * [Deployment variables and the var-store](https://github.com/frodenas/redis-boshrelease#deployment-variables-and-the-var-store)
* [Contributing](https://github.com/frodenas/redis-boshrelease#contributing)
* [License](https://github.com/frodenas/redis-boshrelease#license)

## Usage

### Requirements

In order to use this BOSH release you will need:

* [BOSH CLI v2](https://bosh.io/docs/cli-v2.html)
* An already deployed [BOSH environment](http://bosh.io/docs/init.html)
* A compatible [cloud-config](http://bosh.io/docs/terminology.html#cloud-config) with a `default` option for `network` and `vm_types` (you can use the example that comes from [cf-deployment](https://github.com/cloudfoundry/cf-deployment/blob/master/bosh-lite/cloud-config.yml))

###  Clone the repository

First, clone this repository into your workspace:

```
git clone https://github.com/frodenas/redis-boshrelease
cd redis-boshrelease
export BOSH_ENVIRONMENT=<name>
```

### Basic deployment

To deploy a basic `redis` server use the following command:

```
bosh -d redis deploy manifests/redis.yml \
  --vars-store tmp/deployment-vars.yml
```

### Operations files

Additional [operations files](http://bosh.io/docs/cli-ops-files.html) are located at the [manifests/operators](https://github.com/frodenas/redis-boshrelease/tree/master/manifests/operators) directory. Those files includes a basic configuration, so extra ops files might be needed for additional configuration.

Please review the op files before deploying them to check the requeriments, dependencies and necessary variables.

| File | Description |
| ---- | ----------- |
| [enable-cluster-mode.yml](https://github.com/frodenas/redis-boshrelease/blob/master/manifests/operators/enable-cluster-mode.yml) | Enables clustering mode |
| [enable-slaves.yml](https://github.com/frodenas/redis-boshrelease/blob/master/manifests/operators/enable-slaves.yml) | Enables slave nodes |

### Deployment variables and the var-store

Some operators files requires additional information to provide environment-specific or sensitive configuration such as various credentials. To do this in the default configuration, we use the `--vars-store`. This flag takes the name of a `yml` file that it will read and write to. Where necessary credential values are not present, it will generate new values based on the type information stored at the different deployment files. Necessary variables that BOSH can't generate need to be supplied as well.
See each particular op files you're using for any additional necessary variables.

See also the [BOSH CLI documentation](http://bosh.io/docs/cli-int.html#value-sources) for more information about ways to supply such additional variables.

## Contributing

Refer to [CONTRIBUTING.md](https://github.com/frodenas/redis-boshrelease/blob/master/CONTRIBUTING.md).

## License

Apache License 2.0, see [LICENSE](https://github.com/frodenas/redis-boshrelease/blob/master/LICENSE).
