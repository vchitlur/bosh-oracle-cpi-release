# BOSH Oracle CPI Release Repository
What's the purpose of this project? 
any architecture diagram / rough conceptual diagram? How can i use it?

## Before you begin

* Make sure that you have access to Oracle Cloud Infrastructure. See [OCI Concepts Documentation](https://docs.us-phoenix-1.oraclecloud.com/Content/GSG/Concepts/concepts.htm) to learn about these concepts.
* Install Terraform and deploy BOSH Bastion using Terraform. This is required for deploying BOSH director and Cloud Foundry. See [Initializing a Cloud Foundry / BOSH deployment](https://github.com/oracle/terraform-oci-cf-install).
* Deploy  [BOSH Director](deploy_director.md) on OCI
* Install [BOSH CLI v2](https://bosh.io/docs/cli-v2.html#install) to run BOSH commands. (----check bosh director, there are install instructions for CLI. We may have to remove or update both the places. Check with Dhiraj.)

### Build a development release tarball 

Requirements? 

#### Setup 
##### Clone this repo with the CPI submodule
```bash
$ git clone --recursive git@github.com:oracle/bosh-oracle-cpi-release.git
```

Note: CPI implementation source code lives in a different repository that is included as a git submodule under ./src of this 
repository 
##### Download Golang SDK into the local blobstore
````bash
$ ./populate-blobstore.sh
````
#### Build 
```bash
$ ./build-release.sh
```
build-release.sh will bump the dev release version and produce 

**bosh-oracle-cpi-0+dev.latest.tgz** 

under ./dev_releases/bosh-oracle-cpi directory

#### Clean up
```bash
$ bosh reset-release 
```
to remove all the versions of this release under ./dev_releases 

## Community? Support? or how they can contribute?

## CF or Bosh code of conduct?

