[![GitHub version](https://d25lcipzij17d.cloudfront.net/badge.svg?id=gh&type=6&v=v1.10.1&x2=0)](https://github.com/Praqma/helmsman/releases) [![CircleCI](https://circleci.com/gh/Praqma/helmsman/tree/master.svg?style=svg)](https://circleci.com/gh/Praqma/helmsman/tree/master)

![helmsman-logo](docs/images/helmsman.png)

# What is Helmsman?

Helmsman is a Helm Charts (k8s applications) as Code tool which allows you to automate the deployment/management of your Helm charts from version controlled code.

# How does it work?

Helmsman uses a simple declarative [TOML](https://github.com/toml-lang/toml) file to allow you to describe a desired state for your k8s applications as in the [example toml file](https://github.com/Praqma/helmsman/blob/master/example.toml).
Alternatively YAML declaration is also acceptable [example yaml file](https://github.com/Praqma/helmsman/blob/master/example.yaml).

The desired state file (DSF) follows the [desired state specification](https://github.com/Praqma/helmsman/blob/master/docs/desired_state_specification.md).

Helmsman sees what you desire, validates that your desire makes sense (e.g. that the charts you desire are available in the repos you defined), compares it with the current state of Helm and figures out what to do to make your desire come true.

To plan without executing:
``` $ helmsman -f example.toml ```

To plan and execute the plan:
``` $ helmsman --apply -f example.toml ```

To show debugging details:
``` $ helmsman --debug --apply -f example.toml ```

To run a dry-run:
``` $ helmsman --debug --dry-run -f example.toml ```

To limit execution to specific application:
``` $ helmsman --debug --dry-run --target artifactory -f example.toml ```

# Features

- **Built for CD**: Helmsman can be used as a docker image or a binary.
- **Applications as code**: describe your desired applications and manage them from a single version-controlled declarative file.
- **Suitable for Multitenant Clusters**: deploy Tiller in different namespaces with service accounts and TLS.
- **Easy to use**: deep knowledge of Helm CLI and Kubectl is NOT mandatory to use Helmsman.
- **Plan, View, apply**: you can run Helmsman to generate and view a plan with/without executing it.
- **Portable**: Helmsman can be used to manage charts deployments on any k8s cluster.
- **Protect Namespaces/Releases**: you can define certain namespaces/releases to be protected against accidental human mistakes.
- **Define the order of managing releases**: you can define the priorities at which releases are managed by helmsman (useful for dependencies).
- **Idempotency**: As long your desired state file does not change, you can execute Helmsman several times and get the same result.
- **Continue from failures**: In the case of partial deployment due to a specific chart deployment failure, fix your helm chart and execute Helmsman again without needing to rollback the partial successes first.

# Install

## From binary

Please make sure the following are installed prior to using `helmsman` as a binary (the docker image contains all of them):

- [kubectl](https://github.com/kubernetes/kubectl)
- [helm](https://github.com/helm/helm) (for `helmsman` >= 1.6.0, use helm >= 2.10.0. this is due to a dependency bug #87 )
- [helm-diff](https://github.com/databus23/helm-diff) (`helmsman` >= 1.6.0)

If you use private helm repos, you will need either `helm-gcs` or `helm-s3` plugin or you can use basic auth to authenticate to your repos. See the [docs](https://github.com/Praqma/helmsman/blob/master/docs/how_to/helm_repos) for details.


Check the [releases page](https://github.com/Praqma/Helmsman/releases) for the different versions.
```
# on Linux
curl -L https://github.com/Praqma/helmsman/releases/download/v1.10.1/helmsman_1.10.1_linux_amd64.tar.gz | tar zx
# on MacOS
curl -L https://github.com/Praqma/helmsman/releases/download/v1.10.1/helmsman_1.10.1_darwin_amd64.tar.gz | tar zx

mv helmsman /usr/local/bin/helmsman
```

## As a docker image
Check the images on [dockerhub](https://hub.docker.com/r/praqma/helmsman/tags/)

## As a package
Helmsman has been packaged in Archlinux under `helmsman-bin` for the latest binary release, and `helmsman-git` for master.

# Documentation

- [How-Tos](https://github.com/Praqma/helmsman/blob/master/docs/how_to/).

- [Desired state specification](https://github.com/Praqma/helmsman/blob/master/docs/desired_state_specification.md).

- [CMD reference](https://github.com/Praqma/helmsman/blob/master/docs/cmd_reference.md)


## Usage

Helmsman can be used in three different settings:

- [As a binary with a hosted cluster](https://github.com/Praqma/helmsman/blob/master/docs/how_to/settings).
- [As a docker image in a CI system or local machine](https://github.com/Praqma/helmsman/blob/master/docs/how_to/deployments/ci.md) Always use a tagged docker image from [dockerhub](https://hub.docker.com/r/praqma/helmsman/) as the `latest` image can (at times) be unstable.
- [As a docker image inside a k8s cluster](https://github.com/Praqma/helmsman/blob/master/docs/how_to/deployments/inside_k8s.md) 


# Contributing

Pull requests, feedback/feature requests are welcome. Please check our [contribution guide](CONTRIBUTION.md).
