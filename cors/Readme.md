## Create a bucket

aws s3 mb s3://cors-fun-ab-1122


## Change block public access

aws s3api put-public-access-block \
--bucket cors-fun-ab-1122 \
--public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"


## Create a bucket policy

aws s3api put-bucket-policy \
--bucket cors-fun-ab-1122 \
--policy file://policy.json


## Turn on static website hosting

aws s3api put-bucket-website --bucket cors-fun-ab-1122 --website-configuration file://website.json


## Upload index.html file and include a resource that would be cross-origin

aws s3 cp index.html s3://cors-fun-ab-1122


## View the website and see if the index.html is there

http://cors-fun-ab-1122.s3-website.us-east-2.amazonaws.com


## Create Website 2

aws s3 mb s3://cors-fun2-ab-1122

aws s3api put-public-access-block --bucket cors-fun2-ab-1122 --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"

aws s3api put-bucket-policy --bucket cors-fun2-ab-1122 --policy file://policy2.json

aws s3api put-bucket-website --bucket cors-fun2-ab-1122 --website-configuration file://website.json

aws s3 cp hello.js s3://cors-fun2-ab-1122


## Create API Gateway with mock response and then test the endpoint

curl -X POST -H "Content-Type: application/json" https://p93tifywae.execute-api.us-east-2.amazonaws.com/prod/hello


## Apply a CORS policy

aws s3 cp index.html s3://cors-fun-ab-1122

aws s3api put-bucket-cors --bucket cors-fun-ab-1122 --cors-configuration file://cors.json


## Cleanup

Did manually because of the amount of different files