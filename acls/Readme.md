## Create a new bucket

aws s3api create-bucket --bucket acl-example-ab-1122 --region us-east-1


## Turn off Block Public Access for ACLs

aws s3api put-public-access-block \
--bucket acl-example-ab-1122 \
--public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=true,RestrictPublicBuckets=true"


## Get public access

aws s3api get-public-access-block --bucket acl-example-ab-1122


## Change bucket ownership

aws s3api put-bucket-ownership-controls \
--bucket acl-example-ab-1122 \
--ownership-controls="Rules=[{ObjectOwnership=BucketOwnerPreferred}]"


## Change ACLs to allow fro a user in another AWS account

aws s3api put-bucket-acl \
--bucket acl-example-ab-1122 \
--access-control-policy file://workspace/AWS-Examples/acls/policy.json


## Access Bucket from other account

touch bootcamp.txt
aws s3 cp bootcamp.txt s3://acl-example-ab-1122
aws s3 ls s3://acl-example-ab-1122

## Cleanup

aws s3 rm s3://acl-example-ab-1122/bootcamp.txt
aws s3 rb s3://acl-example-ab-1122
