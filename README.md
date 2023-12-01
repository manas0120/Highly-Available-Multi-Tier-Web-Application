<h1> <b><pre># Highly-Available, Fault tolerant, Multi-Tier Web-Application</pre></b></h1>
 <h2><pre>
Specifically, we will walk through the following topics:
1. Network – Amazon VPC
2. Compute – Amazon EC2
3. Database – Amazon Aurora
4. Storage – Amazon S3
5. Clean up resource.
</pre>
</h2>


 <h3>D. Storage - Amazon S3</h3>
 <h4>Amazon Simple Storage Service (S3) provides a web service-based interface that simplifies data processing anytime, anywhere.
Outline - This lab is designed to help users learn how to save, check, move, and delete data using S3. 
You can also see the ability to host simple static web pages using S3's static website hosting functionality.
</h4>
<h3>Architecture</h3>
<img width="522" alt="S3 Architecture" src="https://github.com/manas0120/Highly-Available-Multi-Tier-Web-Application/assets/60257363/e67849bb-4ea3-4c75-8c67-a336830fdbd1">

 <h4>Create Bucket on S3</h4>
 <ol>
  <li>From the AWS Management Console, connect to S3 . Press Create bucket to create a bucket.</li>
 <li>Enter a unique bucket name in the Bucket name field. For this lab, type immersion-day-user_name, 
  substituiting user-name with your name. All bucket names in Amazon S3 have to be unique and cannot be duplicated. 
  In the Region drop-down box, specify the region to create the bucket. In this lab, select the region closest to you. 
  The images will show the Asia Pacific (Seoul) region. Object Ownership change to ACLs enabled. 
  Bucket settings for Block Public Access use default values, and select Create bucket in the lower right corner.</li>

<h4>Note - Bucket names must comply with these rules:
Can contain lowercase letters, numbers, dots (.), and dashes (-).
Must start with a number or letter.
Can be specified from a minimum of 3 to a maximum of 255 characters in length.
Cannot be specified in the format like the IP address (e.g., 265.255.5.4).</h4>
<li>A bucket has been created on Amazon S3.</li>
</ol>

NOTE - There are no costs incurred for creating bucket. You pay for storing objects in your S3 buckets. 
 The rate you’re charged depends on the region you are using, your objects' size, how long you stored the 
 objects during the month, and the storage class. There are also per-request fees. Click for more information 

 <h4>Adding Objects to Bucket</h4>
This lab hosts static websites through S3. The static website serves as a redirect to an instance 
created by the VPC Lab when you click on a particular image. Therefore, prepare one image file, 
one HTML file, and an ALB DNS name.
 <ol>
  <li>Download the image file <a href="https://static.us-east-1.prod.workshops.aws/public/dd38a0a0-ae47-43f1-9065-f0bbcb15f684/static/common/s3_advanced_lab/aws.png">aws.png</a>and save it as aws.png.</li>
 <li>Write index.html using the source code below.</li>

  <img width="602" alt="S3 index file" src="https://github.com/manas0120/Highly-Available-Multi-Tier-Web-Application/assets/60257363/1bf194fd-180d-4224-a7da-964d992376af">
 
 <li>Upload the aws.png file to S3. Click S3 Bucket that you just created</li>
 <li>Click the Upload button. Then click the Add files button. Select the pre-downloaded aws.png 
  file through File Explorer. Alternatively, place the file in Drag and Drop to the screen.</li>
  <li>Check the file information named aws.png to upload, 
   then click the Upload button at the bottom.</li>
   <li>Check the URL information to fill in the image URL in index.html file. 
    Select the uploaded aws.png file and copy the Object URL information from the details on the right.</li>
   <li>Paste Object URL into the image URL part of the index.html. 
     Then specify the ALB DNS Name of the load balancer created by Deploy auto scaling web service 
     to redirect to ALB when you click on the image.</li>
   <li>Upload the index.html file to S3 following the same instructions as you did to upload the image.</li> 
 </ol>

 NOTE - By default, all objects in the S3 bucket are owner-only(Private). To determine the object through 
 a URL of the same format as https://{Bucket}.s3.{region}.amazonaws.com/{Object}, you must grant Read permission for external users to read it. Alternatively, you can create a signature-based Signed URL that contains credentials for that object, allowing unauthorized users to access it temporarily.

<ol>
 VIEW OBJECTS
 <li>select the Permissions tab in the bucket. To modify the application of Block public access (bucket settings), press the right Edit button.</li>
 <li>Uncheck box and press the Save changes button</li>
 <li>Enter confirm in the bucket's Edit Block public access pop up window and press the Confirm button.</li>
 <li>Click the Objects tab, select the uploaded files, click the Action drop-down button, and press the Make public button to set them to public.</li>
 <li>When the confirmation window pops up, press the Make public button again to confirm.</li>
 <li>Return to the bucket page, select index.html, and click the Object URL link in the Show Details entry.</li>
 <li>When you access the HTML object file object URL, the following screen is printed.</li>
</ol>
<img width="464" alt="AWS EC2 S3 image" src="https://github.com/manas0120/Highly-Available-Multi-Tier-Web-Application/assets/60257363/cb630570-6c7d-475e-bfea-7d43c9d66304">

 <h3>Enable Static Hosting</h3>
 <h4>A static website refers to a website that contains static content (HTML, image, video) 
  or client-side scripts (Javascript) on a web page. In contrast, dynamic websites require 
  server-side processing, including server-side scripts such as PHP, JSP, or ASP.NET. 
  Server-side scripting is not supported on Amazon S3. If you want to host a dynamic website, 
  you can use other services such as EC2 on AWS.
</h4>

<ol>
 <li>In the S3 console, select the bucket you just created, and 
  click the Properties tab. Scroll down and click the Edit button on 
  Static website hosting.</li>
 <li>Activate the static website hosting function and select the hosting type and 
  enter the index.html value in the Index document value, then click the save changes button.</li>
 <li>Click Bucket website endpoint created in the Static website hosting entry to access the static website.</li>
</ol> 

 <h3> Move Objects</h3>
 <ol>
  <li>Create a temporary bucket for moving objects between buckets 
  (Bucket name: immersion-day-myname-target). Substitute myname with your name. 
   Rememeber the naming rules for the bucket. Block all public access 
   Uncheckbox for quick configuration.</li>
 <li>Check the notification window below and select Create bucket.</li>
 <li>In the Amazon S3 Console, select the bucket that contains the object 
  (the first bucket you created) and click the checkbox for the object you want to move. 
  Select the Actions menu at the top to see the various functions you can perform on that object.
  Select Move from the listed features.</li>
<li>Select the destination as bucket, then click the Browse S3 button to find the new bucket you just created.</li>
<li>Click the bucket name in the pop-up window, then select the destination (arrival) bucket. 
 Click the Choose destination button.</li>
<li>Check that the object has moved to the target bucket.</li>
 </ol>

 <h4>Enable Versioning</h4>
 <ol>
  <li>In the Amazon S3 Console, select the first S3 bucket we created. Select the Properties menu. 
   Click the Edit button in Bucket Versioning.</li>
<li>Click the enable radio button on Bucket Versioning, then click Save changes.</li>
<li>In this lab, the index.html file will be modified and re-uploaded with the same name. 
 Make some changes to the index.html file. Then upload the modified file to the same S3 bucket.</li>
<li>When the changed file is completely uploaded, click the object in the S3 Console. 
 You can view current version information by clicking the Versions tab on the page that contains object details.</li>
</ol>

 <h4>Delecting Objects and Buckets</h4>
 <ol>
  <li>In the Amazon S3 Console, select the Bucket that you want to delete. Then click Delete. 
  A dialog box appears for deletion.</li>
  <li>There is a warning that buckets cannot be deleted because they are not empty. 
   Select empty bucket configuration to empty buckets.</li>
 <li>Empty bucket performs a one-time deletion of all objects in the bucket. 
  Confirm by typing permanently delete in the box. Then click the Empty button.</li>
<li>Now the bucket is empty. Perform task 1 again. Enter a bucket name and press the Delete bucket button.</li>
 </ol>
</pre>

<pre>
 <h3>Clean up Resources</h3>
 <h4>NOTE-  If Completed this workshop with your own account, it is strongly recommend to delete the resources and avoid incurring costs</h4>

 <h3> Delete Database</h3>
 <p>
  1.After accessing to the Amazon RDS console, select DB Instances.
  2.By default, an Amazon RDS cluster has delete protection enabled to prevent accidental deletions. 
  To disable it, select the Cluster and click the Modify button.
  3.Uncheck the Enable deletion protection button and click the Continue button. 
  4.For immediate deletion, select Apply immediately and click the Modify cluster button.
  5.In order to delete a DB Cluster, you must first delete the DB instances included in the cluster. 
  They can be deleted in any order, but we will delete the Writer instance first.
  Select the Writer instance, and click the Delete button on the Actions menu.
  6.Type delete me in the blank and click the Delete button.
  7.This time, we will delete the Reader instance. Select the Reader instance and
  click the Delete button on the Actions menu.
  8.Type delete me in the blank and click the Delete button.
  9.Lastly, we will delete the DB Cluster. Click the Delete button on the Actions menu.
  10.Uncheck the Take a final snapshot button, check the I acknowledge that automatic backups, 
  including system snapshots and point-in-time recovery, are no longer available when I delete an 
  instance button, and type delete me in the blank. Click Delete DB Cluster and the DB cluster will be deleted.
 </p>
<h3>Delete RDS Snapshot</h3>
  <p>
   11.To delete the snapshot of the DB Cluster created during the lab, select immersionday-snapshot and click the Delete snapshot button on the Actions menu.
   12.Click Delete Button.
  </p>
 <h3>Delete AWS Secret Manager</h3>
 <p>
  1.We're going to delete the secret that stored a RDS credential during the lab. 
  Type Secrets Manager in the AWS console search bar and then select it.
  2.Select mysecret.
  3.Click Delete Secret on the Action menu.
  4.To prevent accidental deletion of secrets, AWS Secrets Manager has a deletion wait time of minimum 
  7 days and maximum 30 days. Enter the minimum time of 7 days and press the Schedule deletion button.
 </p>

 <h3>Compute</h3>
 <p>
  1.We're going to delete the Auto Scaling Group that we used during the lab. 
  Type EC2 in the AWS Console search bar and select it. Select Auto Scaling Groups from the left menu. 
  Select the Web-ASG that we created in the lab and click the Delete button on the Actions menu.
  2.Type Delete, click Delete Button.
  </p>
 <h4>Delete Application Load Balancer</h4>
 <p>
  3.Next, we're going to delete the Application Load Balancers. 
  Select Load Balancers from the left menu. Then select the Web-ALB that we created in the lab and 
  click the Delete load balancer button in the Actions menu.
  4.Type confirm in the blank and click the Delete button.
 <h4>Delete a Target Group</h4>
  5.We're going to delete the Target Group we created when we created the Application Load Balancer. 
  Select Target Groups from the left menu. Select the Target Group we created in the lab, web-TG, and 
  click the Delete button on the Actions menu.
  6.Click the Yes, delete button.
  <h4>Delete EC2 AMIs</h4>
  7.Select AMIs from the left menu. Select the AMI named Web Server v1 that you created in the lab. 
  Click the Deregister AMI button on the Actions
  8.Click the Deregister AMI button.
  <h4>Delete EC2 Snapshots</h4>
  9.You've just deleted an AMI, but this action doesn't automatically remove the associated snapshot. 
  So you need to remove it manually. From the left menu, choose Snapshots. 
  Be sure to note the snapshot's creation date. Then, select the snapshot you created in the lab, 
  and click the Delete snapshot button on the Actions menu.
  10.Click Delete Button.
  11.Select Launch Templates from the left menu. Select the template named Web that you created in the lab. 
  Click the Delete template button on the Actions menu.
  12.Type Delete in the blank and click the Delete button.

  <h4>Delete an EC2 instance</h4>
  13.If you went through the (Optional) Connect RDS Aurora section during the database lab, 
  you need to delete the EC2 instance you created in the lab. Select Instances from the left menu. 
  Select the EC2 instance you created during the lab, and 
  click the Terminate instance button on the Instance state menu.
  14. Click Terminate.
 </p>

 <h3>Network</h3>
 <p>
  <h4>Delete VPC</h4>
  1. Type VPC in the AWS Console search bar and select it. 
  Select Endpoints from the left menu. Select S3 endpoint, 
  the endpoint you created in the lab, and click the 
  Delete VPC endpoints button on the Action Menu.
  2.Type delete in the blank, and click the Delete button.
  <h4>Delete NAT Gateway</h4>
  3.Select NAT gateways from the left menu and select VPC-Lab-nat-public you created during the lab. Click the Delete NAT gateway button on the Actions menu.
  4.Type delete in the blank and click the Delete button.
  <h4>Delete an Elastic IP</h4>
  5.You've just deleted the NAT gateway, but this action doesn't automatically 
  delete the Elastic IP that the NAT gateway used, so you need to remove it manually. 
  Select Elastic IPs from the left menu, and select VPC-Lab-eip-ap-northeast-2a. 
  (The name after VPC-Lab-eip may vary depending on your region.) 
  Click the Release Elastic IP addresses button on the Actions menu. 
  If it says it is still associated with the NAT gateway and cannot be deleted, refresh the webpage and try again.
  6.Click Release Button.
  <h4>Delete Security Group</h4>
  7.We're going to delete the Security Group you created during the lab. 
  Select Security Groups from the left menu. Select Immersion Day - Web Server and DB-SG first, 
  and then click the Delete security groups button on the Actions menu. 
  The reason for not deleting all security groups at once is that some security groups 
  reference other security groups in their inbound rules. A security group that is being 
  referenced cannot be deleted until the security group that is referencing it is deleted. 
  Therefore, delete the security groups in the following order: 
  Immersion Day - Web Server, DB-SG -> ASG-Web-Inst-SG -> web-ALB-SG.
  8.Type delete in the blank and click the Delete button.
  9.Select ASG-Web-Inst-SG and click the Delete security groups button on the Actions menu.
  10.Click the Delete button
  11.Select web-ALB-SG and click the Delete security groups button on the Actions menu.
  12.Click the Delete button.
  <h4>Delete a VPC</h4>
  13.Finally, select Your VPCs from the left menu, and 
  select the VPC-Lab-vpc that you created during the lab. 
  Click the Delete VPC button in the Actions menu.
  14.Type delete in the blank and click the Delete button.
 </p>
</pre>
