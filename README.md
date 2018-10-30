# aws-prefixes
Interogate aws ip prefixes - routing in aws

### get prefix list from aws
`wget https://ip-ranges.amazonaws.com/ip-ranges.json`
### filter down on the interesting services
`jq '.prefixes[] | select(.region=="eu-central-1" and .service=="S3").ip_prefix' < ip-ranges.json`
### exclude ec2 instances in a region
`jq -r '[.prefixes[] | select(.region=="us-east-1" and .service=="AMAZON").ip_prefix] - [.prefixes[] | select(.region=="us-east-1" and .service=="S3").ip_prefix] | .[]' < ip-ranges.json`
