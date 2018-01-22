# Deploy BOSH Director on OCI

In Oracle Cloud Infrastructure (OCI), BOSH will be installed on one of the subnets and the BOSH director will be deployed to manage other deployments. The BOSH director is deployed from a bastion instance. The bastion and the director instances are created on different subnets. The security rules for these subnets are configured such that the director is not exposed to public IP (accessible only from the bastion subnet) and only ssh traffic is allowed into the bastion subnet.

Pictorially this can be represented as

---

![Network topology](bastion_director_topology.png)

---

You can use the [Terraform OCI CF/BOSH installer](https://github.com/oracle/terraform-oci-cf-install) to create VCN, Subnets, Security Lists, and Bastion instance.

Creating a BOSH director environment (****Do we need to push this to the end?? I thought we will install first and then set the env.)

    SSH into the bastion instance created by the Terraform OCI CF/BOSH installer
    The installer places two files under $HOME
        install_deps.sh -- Executable script for installing the bosh cli v2 and its dependencies (make, ruby)
        director-env-vars.yml -- A BOSH variables file containing the values for variables referred to by various ops files


(Need to add this somewhere - Using [BOSH CLI v2 create-env](https://bosh.io/docs/cli-v2#create-env)  create-env command to create a director environment)



Not sure if this is the right place for these two:
## Install bosh cli
```
  $ ./install_deps.sh
```

Clone this repo to get OCI specific ops files and bosh cli wrapper scripts
```
  $ git clone https://github.com/oracle/bosh-oracle-cpi-release.git
```

### Deploy the director and set the environment
```
   $ cd bosh-oracle-cpi-release/bosh-deployment
   
   $ ./create-env.sh 
```
