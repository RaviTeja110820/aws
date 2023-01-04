# S3 Static Webiste hosting

You can use Amazon S3 to host a static website. On a static website, individual webpages include static content. They might also contain client-side scripts.

# steps

1. Create a bucket
2. Uploaded a website folder
3. Enabling static website host in properties section
4. Entering 'index.html' in index document.
5. Paste aws s3 public bucket policy.
6. Copy the url and paste it in the browser.
   
# setup

## Create S3 Bucket

**To create S3 Bucket**
1. Open the S3 Bucket in AWS Management Console
2. Click on Create Bucket
   ![Create Bucket](./images/create-bucket.png)
3. Enter the Bucket name that should be unique globally.
   
   ![Bucket Name](./images/bucket-name.png)
4. Bucket Created Successfully
   ![Successful Creation](./images/successful.jpg)

**To Uploaded a website folder**

1. Click Upload in the Bucket.
2. Select Add Folder and upload the website folder from your Desktop. Wait for some time to successfully complete the upload.
![Upolad Folder](./images/upload-folder.jpg)

**To Enable static website host in properties section**

1. In properties scrool down and click on edit static website hosting.
   ![Properties](./images/properties.jpg)
2. Enable the static website hosting and mention index.html as the default page of the website in index document. Save the changes.
   ![Enable-Hosting](./images/enable-hosting.jpg)