## Initializing a Cloud Foundry / BOSH deployment

This project exists to simplify the configuration and deployment of Cloud Foundry and BOSH on
Oracle Cloud Infrastructure. It will configure the following:
* VCN and Subnets
    * Public, Private and Bastion Subnets in 3 Availability Domains
* A Bastion server with BOSH CLI for deploying BOSH Director and Cloud Foundry.

### Install and Configure Terraform to work with OCI

Q Do they need to sign up for Cloud account before they start?

	1. Install and configure terraform.
		a. Install Terraform v0.10.6 or later. For example, on Mac OS X, you can use Homebrew.
		```
		$ brew install terraform
		```
		b. Download the [Terraform OCI binary]( https://github.com/oracle/terraform-provider-oci/releases) from GitHub and save it in your local/bin file. For example, /user/local/bin.
		c. Update the environment variables - what're the updates?
			i. Source environment variables
				$ .env-var
	2. Configure the OCI API key. You need an API key to use Terraform with OCI, so generate a public key in the PEM format and obtain its fingerprint. See https://docs.us-phoenix-1.oraclecloud.com/Content/API/Concepts/apisigningkey.htm.
	3. Deploy BOSH using the Terraform:
		a. Run the bosh-key-gen.sh script to generate the keys that BOSH use to communicate with OCI, SSH key pair for shell access to the bastion instance, and SSL certificates for the load balancers. (should try this out and write the detailed steps. Why do we need both API key and ssh?)
		b. When you're creating SSL certificates, you will be prompted for passphrase. Remember the password that you type here as you may need this password again later in the process. 
		c. Deploy the environment using Terraform:
			```
			terraform apply
			```
		d. Note down the IP address of the instance.
		e. To access the instance, use the IP address and the SSH key pair :
			```
			ssh -i keys/bosh-ssh ubuntu@<your IP address>
			```
				
#### Post Provisioning ---to revise

The bastion VM will come a script to install the BOSH v2 CLI, and will also manage the iSCSI connection for the
block device.  In order to preserve data in case of a failure and subsequent `terraform apply` run, no effort
is taken to format the attached block device, which is at `/dev/sdb`.  Upon successful deployment of the bastion
VM, you may format and mount the block device manually.

```bash
$ ./install_deps.sh
$ sudo mkfs.ext4 /dev/sdb
$ sudo mount -a
```

In the home directory, the `bosh` folder points to the mounted block device, so you may keep your releases,
stemcells and deployments there for safe keeping.