# Publishing The Book

This is for individuals that need to publish the contents to S3. We use the tool `s3_website` to publish the contents to S3. It handles ensuring all the content types are set correctly, redirects and more. 

**Note:** The website gets published to a subdirectory at `books.nowsecure.com` which is all configured in `s3_website.yml` file.

## Requirements

1. Node.JS
2. `s3_website` tool installed (https://github.com/laurilehmijoki/s3_website) (you need at least version 2.16.0)
3. Vault Access
4. AWS Credentials valid for S3.

## Steps to Publish

1. npm install
2. gitbook build
3. vault read aws/creds/s3-books-secure-mobile-development
4. - Set ENV Vars -
  * S3_ID=(AWS ACCESS KEY -- from vault read)
  * S3_SECRET=(AWS SECRET KEY -- from vault read)
  * S3_BUCKET=books.nowsecure.com
4. s3_website push

## Adding Redirects

To add a redirect just add it to the bottom of the s3_website.yml file in this repo. 

Redirects are based on the relative directory to `https://books.nowsecure.com/secure-mobile-development/` and the destination is absolute to `https://books.nowsecure.com/`

For example if you want to redirect `https://books.nowsecure.com/secure-mobile-development/handling-sensitive-data/implement-secure-data-storage/` to `https://books.nowsecure.com/secure-mobile-development/en/sensitive-data/implement-secure-data-storage.html` then you'd need to add an entry like the following.

```yaml
 handling-sensitive-data/implement-secure-data-storage/index.html: /secure-mobile-development/en/sensitive-data/implement-secure-data-storage.html
```
