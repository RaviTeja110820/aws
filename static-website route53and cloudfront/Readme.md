# Static Website with CloudFront and Route53

You can use Amazon CloudFront to improve the performance of your Amazon S3 website. CloudFront makes your website files (such as HTML, images, and video) available from data centers around the world (known as edge locations). When a visitor requests a file from your website, CloudFront automatically redirects the request to a copy of the file at the nearest edge location. This results in faster download times than if the visitor had requested the content from a data center that is located farther away.

CloudFront caches content at edge locations for a period of time that you specify. If a visitor requests content that has been cached for longer than the expiration date, CloudFront checks the origin server to see if a newer version of the content is available. If a newer version is available, CloudFront copies the new version to the edge location. Changes that you make to the original content are replicated to edge locations as visitors request the content.

# steps

1. Create a bucket
2. Create a CloudFront distribution
3. Update the record sets for your domain and subdomain
4. Check the log files

# setup
**To Create a Bucket**

* Create a bucket with unique name. 
- Uploaded a website folder
* Enabling static website host in properties section
- Entering 'index.html' in index document.
* Paste aws s3 public bucket policy.
- Copy the url and paste it in the browser.
  
**To create a CloudFront Distribution**
