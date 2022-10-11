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




