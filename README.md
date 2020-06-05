# BOSH release for config-server-forge

A Spring Cloud Config Server Forge for Blacksmith


This BOSH release and deployment manifest deploy a cluster of config-server-forge.

## Usage

This repository includes base manifests and operator files. They can be used for initial deployments and subsequently used for updating your deployments:

```plain
export BOSH_ENVIRONMENT=<bosh-alias>
export BOSH_DEPLOYMENT=config-server-forge
git clone https://github.com/cloudfoundry-community/config-server-forge-boshrelease.git
bosh deploy config-server-forge-boshrelease/manifests/config-server-forge.yml
```

If your BOSH does not have Credhub/Config Server, then remember `--vars-store` to allow generation of passwords and certificates.

### Update

When new versions of `config-server-forge-boshrelease` are released the `manifests/config-server-forge.yml` file will be updated. This means you can easily `git pull` and `bosh deploy` to upgrade.

```plain
export BOSH_ENVIRONMENT=<bosh-alias>
export BOSH_DEPLOYMENT=config-server-forge
cd config-server-forge-boshrelease
git pull
cd -
bosh deploy config-server-forge-boshrelease/manifests/config-server-forge.yml
```

# Parameterized

nginx.conf (operator)


# Development Notes
Kevin's blacksmith jumpbox  
ssh -A team@10.134.0.32

cd src # to get to the git directories

Need to push bosh release twice in the development environment.

bosh -e intrado-vsphere-base upload-release  
bosh -e intrado-vsphere-base-blacksmith upload-release  
genesis deploy intrado-vsphere-base.yml -y  
genesis do intrado-vsphere-base.yml -- boss catalog  
  
bosh -e intrado-vsphere-base -d intrado-vsphere-base-blacksmith ssh  
  
genesis do intrado-vsphere-base.yml -- boss create config-server standard  
genesis do intrado-vsphere-base.yml -- boss create config-server/standard  
bosh -e intrado-vsphere-base -d intrado-vsphere-base-blacksmith ssh  
genesis do intrado-vsphere-base.yml -- boss create config-server/standard  
bosh -e intrado-vsphere-base -d intrado-vsphere-base-blacksmith ssh  
bosh -e intrado-vsphere-base -d intrado-vsphere-base-blacksmith ssh  
