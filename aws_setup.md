# AWS Setup Guide
These directions will provide a guide on how to setup a static page on S3. 
https://stories.mlh.io/your-domain-com-amazon-web-services-powered-site-in-30-minutes-or-less-8828f524bb6a

## Create S3 Bucket
### Interactive Steps
1. Navigate to [S3 Console](https://s3.console.aws.amazon.com/s3/home?region=us-east-1)
2. Select "Create Bucket"
3. On Page 1 "Name and region", enter a unique bucket name (e.g. `apm-comics-web-flast` where you replace `flast` with the first letter of your first name and your last name)
4. Click "Next"
5. On Page 2 "Set properties", click on "Default Encryption" and select `AES-256` and click "Save"
6. Click "Next"
7. On Page 3 "Set permissions", under the heading "Manage public permissions", select the drop down "Grant public read access to this bucket"
8. Click "Next"
9. Confirm the properties, and click "Create Bucket"
10. When you are returned to the S3 Console, click on the bucket which you just created
11. Select the "Properties" tab
12. Click on "Static website hosting"
13. Click on the "Use this bucket to host a website" radio button
14. In the "Index document" textbox, enter `index.html`
15. Click Save
16. Launch a terminal window
17. Run the following command to copy the contents of the APM Comics Website to your S3 Bucket:<br/>`aws s3 sync s3://apm-comics-web/web s3://YOUR_BUCKET_HERE --region US-EAST-1 --acl bucket-owner-full-control --acl public-read`<br/>replacing `YOUR_BUCKET_HERE` with the name of the bucket you created in Step 3
18. Attempt to visit `http://YOUR_BUCKET_HERE.s3-website-us-east-1.amazonaws.com` replacing `YOUR_BUCKET_HERE` with the name of the bucket you created in Step 3 and ensure that the page loads. There might not be much there, as the DynamoDB page is not properly set up (yet)

### Programatic Steps
1. Launch terminal window
2. `aws s3api create-bucket --bucket YOUR_BUCKET_HERE --region us-east-1 --create-bucket-configuration LocationConstraint=us-east-1`<br/> replacing `YOUR_BUCKET_HERE` with a unique bucket name (e.g. `apm-comics-web-flast` where you replace `flast` with the first letter of your first name and your last name)
3. `aws s3 cp /Users/ezronis/dev/gnpl-hackathon s3://gnl-hackathon --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers --recursive`
4. `aws s3 website s3://YOUR_BUCKET_HERE/ --index-document index.html --error-document error.html`<br/>replacing `YOUR_BUCKET_HERE` with the name of the bucket you created in Step 2

## Complete
Congratulations! If you now visit `http://YOUR_BUCKET_NAME.s3-website-us-east-1.amazonaws.com`, you should see a functioning Serverless AWS Application!