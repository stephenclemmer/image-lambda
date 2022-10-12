# image-lambda

[x] Create an S3 Bucket with “open” read permissions, so that anyone can see the images/files in their browser

[] A user should be able to upload an image at any size, and update a dictionary of all images that have been uploaded so far

[] When an image is uploaded to your S3 bucket, it should trigger a Lambda function which must:
  [] Download a file called “images.json” from the S3 Bucket if it exists
  [] The images.json should be an array of objects, each representing an image. Create an empty array if this file is not present
  [] Create a metadata object describing the image Name, Size, Type, etc.
 [] Append the data for this image to the array
 [] Note: If the image is a duplicate name, update the object in the array, don’t just add it
  [] Upload the images.json file back to the S3 bucket

## PseudoCode for next steps:
https://docs.aws.amazon.com/lambda/latest/dg/with-s3-example.html

Get the bucket name from the event object
Get the key from the event object
Create a new parameter object that contains both the bucket and the key
 Use the Amazon S3 getObject API to retrieve the content type of the object. (getObject API can be replaced with any other getObject method in the AWS S3 client library)
Save the response from above into a variable

https://docs.aws.amazon.com/AmazonS3/latest/API/API_GetObject.html

Use GetObject to retrieve the images.json file from the s3 bucket
Push the retrieved info into an array (may need to convert this to a JSON object)
Push the new object into the array if the new object does not already exist, 
If it does already exist, update/overwrite the data

Write it to a JSON file and name it the same as the original file. 

https://docs.aws.amazon.com/AmazonS3/latest/API/API_PutObject.html

Put the JSON file into the bucket, and overwrite the old JSON file.





<!-- End of PseudoCode -->




#### a description of how to use your lambda.


#### a description of any issues you encountered during deployment of this lambda.

#### a link to your images.json file

#### Setting up a bucket and permissions

1. Create bucket.
2. Put something in the bucket.

- Click on the bucket's link to get inside of it.
- Select "Upload"
- Select Add files/add folder (Added a .json file called images.json which had an object with two samples written in it)
- Select "Upload"
- Navigate to, and click, the link for the .json file uploaded.
- click on the Object URL. (At this time you will see that the information is not ble to be accessed. This was basically a "get" request. This can be fixed by defining some permissions.)

3. Define Permissions
(Principal, Action, Resource)

- navigate to the bucket, and select the permissions tab.
- add a bucket policy by selecting "Edit" in the "Bucket policy" section
- Select "Add new statement"
- In the righthand side, under "add actions", type in s3 (because in this instance, we're dealing with an s3 bucket), and select s3. Select the permissions needed. In this case, it will be 'getObject' (because we will be getting a .json file) and 'putObject' (because we will be changing a .json file).
- change the "Principal" value from {} to "*" (include the quotes.
)
- copy the bucket's arn from the upper lefthand corner above this json file. Paste it in between the brackets in the "Resource" part of the .json file. In this case, as it was in the policy example at the top of the page, place a slash and star at the end of the string, i.e., '/*'.
- Save changes. (Unless there is a mistake in the .json file's format, this should save and return a green bar at the top of the page.)
-Navigate to the "Objects" tab. Click on the .json file, and then click on the object URL. You should now see that you have access to the contents of the file. 

#### Lambda

- Open another tab and navigate to AWS Lambda

1. Create a function

- Select the "Create function" button
- name the function (in this case it is called 'addImages')
- Select "Create function". This will take you to the code.

2. Create a test event

- Select the "Test" tab
- input test json data
- name the event (I chose imageTest for this project)
- save the test

***Video 2 of 2***

3. Configure the test event

- on the code tab, select the arrow dropdown and enable the test event
- 


4. Add a trigger

- From the Code tab, select "Add a Trigger"
- From the dropdown, select S3
- Select the bucket
- Fir this project, since it will be uploading images, selkect a suffix for the image file (I chose .png).
- Select the checkbox indicating that you understand that using a single bucket can cause recursive issues that can increase costs.
- Select "Add".

5. Test that the bucket and Lambda are connected

- In Lambda, select the "Monitor" tab, and then select "View Logs in Cloudwatch". Under "Log streams" a list of logs will be present. Leave thie tab open, because it will be checked after an image is uploaded to confirm that the bucket and the Lambda are connected.
- Navigate to the bucket.
- Navigate to the Objects tab
- Select "Upload"
- Select "Add Files"
- Make sure the Type matches the type specified within the trigger's required suffix.
- Select "Upload"
- Navigate to the open tab that is displaying the Log Streams, and refresh the page. If the bucket and Lambda are connected, then the newly uploaded image should be logged.
- Drill into the object to get to the name of the uploaded file. In this case it is:
event.Records\[0].s3\['object']['key']





**Notes**
- Navigate to the test tab and select the test button to test. Logs can be accessed with the blue "log" link, and then by following the logstream link

- Make sure there is a conenction between the bucket and the Lambda, then start coding.