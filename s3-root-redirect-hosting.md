# Two s3 buckets hosting a static page on cloudfront
## Details
* A registered domain: `www.synth-stage.com`.
* Public certificates: One for the root and one for the subdomain. One way to obtain certificates is to create a CNAME record in route53 that points back to ACM. The other way to do it is to validate via email.
* **Root** domain: `synth-stage.com`. Add s3 bucket with this name.
* **Sub** domain: `www.synth-stage.com`. Add s3 bucket with this name.
* Add a redirect from root to subdomain in the s3 bucket config.
* Add the `index.html` in the subdomain bucket.


Acronyms:
ACM: AWS Certificate Manager
CNAME: Canonical Name record (A redirect in DNS).
