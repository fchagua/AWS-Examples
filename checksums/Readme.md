## Create a new s3 bucket

```md
aws s3 mb s3://checksums-example-ab-1122
```

## Create a file that we will do a checksum on

```
echo "Hello Mars" > myfile.txt
```

## get a checksum of a file for md5

md5sum myfile.txt
#8ed2d86f12620cdba4c976ff6651637f  myfile.txt

## Upload our file and look at its etag
aws s3 cp myfile.txt s3://checksums-examples-ab-1122
aws s3api head-object --bucket checksums-examples-ab-1122 --key myfile.txt

#8ed2d86f12620cdba4c976ff6651637f


## Lets upload a file with a different kind of checksum


sudo apt-get install rhash

rhash --crc32 --simple myfile.txt

bundle exec ruby crc.rb

aws s3api put-object \
--bucket="checksums-examples-ab-1122" \
--key="myfilesha1.txt" \
--body="myfile.txt" \
--checksum-algorithm="SHA1" \
--checksum-sha1="c28ccc2c5e214036806014df9fb43634f3e770b2"
