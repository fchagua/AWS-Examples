## Create a bucket
aws s3 mb s3://encryption-fun-ab-1122

## Create a file
echo "Hello World" > hello.txt
aws s3 cp hello.txt s3://encryption-fun-ab-1122

## Create SSE-KMS key
aws s3api create-key 

## Put Object with encryption of KMS
aws s3api put-object \
--bucket encryption-fun-ab-1122 \
--key hello.txt \
--body hello.txt \
--server-side-encryption aws:kms \
--ssekms-key-id cbc6ae6d-21fa-4c7f-8b3d-abc4d004879e

## Download hello.txt file
aws s3 cp s3://encryption-fun-ab-1122/hello.txt hello.txt

## Put Object with encryption of SSE-C
## The following does not work
export BASE64_ENCODED_KEY=$(openssl rand -base64 32)

export MD5_VALUE=$(echo $BASE64_ENCODED_KEY | md5sum | awk '{print $1}' | base64 -w0)

aws s3api put-object \
--bucket encryption-fun-ab-1122 \
--key hello.txt \
--body hello.txt \
--sse-customer-algorithm AES256 \
--sse-customer-key $BASE64_ENCODED_KEY
//--sse-customer-key-md5 $MD5_VALUE


## The following does work
## Put Object with SSE-C via aws s3
openssl rand -out ssec.key 32

aws s3 cp hello.txt s3://encryption-fun-ab-1122/hello.txt \
--sse-c AES256 \
--sse-c-key fileb://ssec.key

## Download encrypted file with key otherwise you will get an error
aws s3 cp s3://encryption-fun-ab-1122/hello.txt hello.txt --sse-c AES256 --sse-c-key fileb://ssec.key

## Cleanup
aws s3 rm s3://encryption-fun-ab-1122/hello.txt
aws s3 rb s3://encryption-fun-ab-1122