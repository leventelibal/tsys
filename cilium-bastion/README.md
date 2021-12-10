# Bastion host deployment

This page contains how to deploy bastion host to rearc account. If you follow each steps you should be able to deploy successfully.

## Before you begin 
1. Make sure you have gihub token 
2. Make sure that dns zone exist on GCP
3. Also you will need `rearc-service-account.json` file to be able to deploy


## Deployment 
Fist you will need to clone the repository 
```
git clone	 https://github.com/leventelibal/Rearc.git
```

After you have cloned the repo you will need to go to `Rearc-bastion` folder 
```
cd fuchicorp-bastion
```

in this folder make sure you have `rearc-service-account.json` file 
```
ls rearc-service-account.json                                                                                                   
cluster-infrastructure/rearc-bastion/rearc-service-account.json
```

After  you have copied rearc service account you will need to generate tfvars.

```
cat <<EOF > rearc-bastion.tfvars
google_bucket_name = "BUCKET_NAME"
google_project_id = "PROJECT_ID"
google_domain_name = "DOMAIN_NAME"
git_common_token = "Github token"
deployment_environment = "tools"
deployment_name = "bastion"
credentials = "rearc-service-account.json"
EOF 
```

After you have generated tfvars you will need to set environments variables
```
source set-env.sh rearc-bastion.tfvars
```

After you have set environment variables you should be able to deploy to GCP 

```
terraform apply -var-file=$DATAFILE
```
