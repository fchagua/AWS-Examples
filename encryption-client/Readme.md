## Create a bucket
aws s3 mb s3://encrypt-client-fun-ab-1122


## Run our SDK ruby script

bundle exec ruby encrypt.rb


## Cleanup
aws s3 rm s3://encrypt-client-fun-ab-1122/hello.txt
aws s3 rb s3://encrypt-client-fun-ab-1122