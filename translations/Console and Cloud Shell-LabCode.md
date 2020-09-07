
LAB: Console and Cloud Shell

OBJECTIVES
In this lab, you learn how to perform the following tasks:
-		Get access to Google Cloud.
-		Create a Cloud Storage bucket using the Cloud Console.
-		Create a Cloud Storage bucket using Cloud Shell.
-		Become familiar with Cloud Shell features

Task 1: Create a bucket using the Cloud Console

      gsutil mb gs://adewale-bucket1/

Task 2: Create a bucket using Cloud Shell


       gsutil mb  gs://adewale-bucket2/

Task 3: Explore more Cloud Shell features
Upload a file
-              Open Cloud Shell.
-	Click the three dots ( ) icon in the Cloud Shell toolbar to display further options.
-                Click Upload file. Upload any file from your local machine to the Cloud Shell VM. This file will be referred to as [MY_FILE].
- 	In Cloud Shell, type ls to confirm that the file was uploaded.

	      ls (this command display files in the current directory including newly uploaded one)
-	Copy the file into one of the buckets you created earlier in the lab. Replace [MY_FILE] with the file you uploaded and [BUCKET_NAME] with one of your bucket names:

              gsutil cp file.txt gs://adewale-bucket2
       (Note If your filename has whitespaces, ensure to place single quotes around the filename. For example, gsutil cp ‘my file.txt' gs://[BUCKET_NAME])
        You have uploaded a file to the Cloud Shell VM and copied it to a bucket.

Task 4: Create a persistent state in Cloud Shell
Steps;
a.	Identify available regions; 
-	To list available regions, execute the following command. Note that this allocates a new VM for you.
       gcloud compute regions list
-	Select a region from the list and note the value in any text editor. This region will now be referred to as [YOUR_REGION] in the remainder of the lab.
    

b.     Create and verify an environment variable
-	Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:

          INFRACLASS_REGION=us-central1 (us-central1 is my selected region)

-	Verify it with echo:

            echo $INFRACLASS_REGION 
           (Note: You can use environment variables like this in gcloud commands to reduce the opportunities for typos, and so that you won't have to remember a lot of detailed            information.)

c.	Append the environment variable to a file

-       Create a subdirectory for materials used in this class:

            mkdir infraclass
-	Create a file called config in the infraclass directory:

            touch infraclass/config
	    
-	Append the value of your Region environment variable to the config file 

           echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config

-     Create a second environment variable for your Project ID, replacing [YOUR_PROJECT_ID] with your Project ID. You can find the project ID on the Cloud Console Home page.

          INFRACLASS_PROJECT_ID=qwiklabs-gcp-0855e773352d3560 (Note my project-id is qwiklabs-gcp-0855e773352d3560)

-	Append the value of your Project ID environment variable to the config file:

          echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config

-	Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:

           source infraclass/config
	   
           echo $INFRACLASS_PROJECT_ID
	   
         (Note: This gives you a method to create environment variables and to easily recreate them if the Cloud Shell is cycled. However, you will still need to remember to             issue the source command each time Cloud Shell is opened.
	 
  In the next step you will modify the .profile file so that the source command is issued automatically any time a terminal to Cloud Shell is opened.)

-   Close and re-open Cloud Shell. Then issue the echo command again:

         echo $INFRACLASS_PROJECT_ID

d.	Modify the bash profile and create persistence

-	Edit the shell profile with the following command:

        nano .profile
-	Add the following line to the end of the file:

           source infraclass/config


-	Press Ctrl+0, ENTER to save the file, and then press Ctrl+X to exit the nano

-	Close and then re-open Cloud shell to cycle the VM.

-	Use the echo command to verify that the variable is still set:

          echo $INFRACLASS_PROJECT_ID
	  
Result: You should now see the expected value that you set in the config file







