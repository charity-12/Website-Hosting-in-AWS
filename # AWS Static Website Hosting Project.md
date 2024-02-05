# AWS Static Website Hosting Project

This repository contains the code and configuration for hosting a static website on Amazon S3.

## Task 1: Creating a Bucket in Amazon S3

### Step 1: Access AWS Management Console

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to the **Services** menu and choose **S3**.

### Step 2: Create S3 Bucket

3. Click on **Create bucket**.


4. Enter a globally unique bucket name. For this lab we use website-1008.

5. Configure the following settings:
   - For **Object Ownership**, choose **ACLs enabled**.
   - Choose **Bucket owner preferred**.
   - Under **Block Public Access settings for this bucket**, clear the check box for **Block all public access**, and acknowledge the warning.
   - For **Bucket Versioning**, choose **Enable**.

6. Add a tag:
   - Key: `Department`
   - Value: `Marketing`

7. Click **Create bucket**.

### Step 3: Access the New Bucket

8. In the Buckets section, choose the name of your new bucket.

9. Select the **Properties** tab.

### Important Notes:

- S3 bucket names are globally unique, and once created, the name cannot be used by other AWS accounts.
- Enabling bucket versioning is irreversible. Once turned on, it cannot be turned off.
- Ensure to configure public access settings as needed for a static website.


### Step 4: Configuring a Static Website on Amazon S3

10. In the S3 bucket, navigate to the **Properties** tab.

11. Scroll down to the **Static website hosting** panel.

12. Click **Edit**.

13. Configure the following settings:
    - **Static web hosting:** Choose **Enable**.
    - **Hosting type:** Choose **Host a static website**.
    - **Index document:** Enter `index.html`.
    - **Error document:** Enter `error.html`.

14. Click **Save changes**.

15. In the **Static website hosting** panel, under **Bucket website endpoint**, choose the provided link.

16. You will receive a 403 Forbidden message as bucket permissions are not yet configured. Keep this tab open for the next steps.

17. Congratulations! You have now configured your S3 bucket to host a static website.



## Task 3: Uploading Content to Your Bucket

18. In the S3 bucket, choose **Upload**.

19. Choose **Add files**.

20. Select the three files that you downloaded.

21. Choose **Upload**.

22. Your files are now uploaded to the bucket.

23. Choose **Close**.

## Task 4: Turning on Public Access to the Objects

Objects in Amazon S3 are private by default. To make your website publicly accessible, follow these steps:

24. Return to the browser tab that showed the 403 Forbidden message.

25. Refresh the webpage. If you accidentally closed this tab, go to the Properties tab, and in the Static website hosting panel, choose the Bucket website endpoint link again.

26. You should still see a 403 Forbidden message. This is expected as your static website content is currently private.

27. Configure individual objects to be publicly accessible:
   - Keep the website tab open and return to the Amazon S3 console.
   - Choose all three objects.
   - In the Actions menu, choose **Make public using ACL**.
   - Confirm and choose **Make public**.

28. Your static website is now publicly accessible.

29. Choose **Close


## Task 4: Turning on Public Access to the Objects

1. Return to the browser tab that showed the 403 Forbidden message.

2. Refresh the webpage. If you accidentally closed this tab, go to the **Properties** tab, and in the **Static website hosting** panel, choose the **Bucket website endpoint** link again.

3. You should still see a 403 Forbidden message. This response is expected, indicating that your static website is hosted by Amazon S3, but the content is private.

4. To make Amazon S3 objects public, you have two options:
   - To make either a whole bucket public or a specific directory in a bucket public, use a bucket policy.
   - To make individual objects in a bucket public, use an access control list (ACL).

5. It is generally safer to make individual objects public to avoid accidentally making other objects public. However, if you are sure that the entire bucket contains no sensitive information, you can use a bucket policy.

6. Keep the website tab open and return to the web browser tab with the Amazon S3 console.

7. Choose all three objects.

8. In the **Actions** menu, choose **Make public using ACL**.

9. A list of the three objects is displayed.

10. Choose **Make public**.

11. Your static website is now publicly accessible.

12. Choose **Close**.

13. Return to the web browser tab that has the 403 Forbidden message.

14. Refresh the webpage.

15. You should now see the static website hosted by Amazon S3.

Now you know how to share objects with everyone by making them public. However, there may be times when you need to share an individual object for a limited amount of time. In the next task, you will learn how to temporarily share an object.


## Task 5: Securely Sharing an Object Using a Presigned URL

1. When you need to temporarily and securely share an object with others, you can create a presigned URL. This URL has a limited validity period.

2. As long as the presigned URL is valid, anyone with it can access the object. Avoid keeping the URL active longer than necessary and share it only with trusted individuals.

3. **Download the File:**
   - Choose (right-click) the following link and download the file to your computer: [new-report.png](#)
   - Ensure that the file keeps the same file name, including the extension.

4. **Upload the File to Amazon S3:**
   - Return to the Amazon S3 console and choose the **Objects** tab.
   - Choose **Upload**, then **Add files**.
   - Upload the file that you downloaded.
   - Choose **Upload**.
   - Choose **Close**.

5. Like when you first uploaded the website files, the `new-report.png` file is private by default. Instead of making the object public, you create a presigned URL to access the file.

6. In the **Objects** tab, choose `new-report.png`.

7. From the **Actions** menu, select **Share with a Presigned URL**.

8. In the pop-up window, configure the time interval until the presigned URL expires:
   - Choose **Minutes**.
   - For **Number of minutes**, enter **2**.
   - Choose **Create presigned URL**.

9. From the banner at the top of the page, choose **Copy presigned URL**.

10. Open a new browser tab and paste the URL you copied into the address bar.

11. A report is displayed in the web browser.

12. If you wait 5 minutes and use the link again, you will find that the URL has expired and no longer works.


## Task 6: Using a Bucket Policy to Secure Your Bucket

1. You want to protect your website files and ensure that no one can delete them. Apply a bucket policy to deny delete privileges on your website files.

2. **Configure Bucket Policy:**
   - Return to the Amazon S3 console and choose the **Permissions** tab.
   - Under **Bucket policy**, choose **Edit**.
   - In the Policy text editor, use the provided in the bucket policy file.
   - Choose **Save changes**.

3. **Test the Policy:**
   - Return to the **Objects** tab.
   - Select `index.html`.
   - Choose **Delete**.
   - In the **Delete objects** panel, enter `delete` to confirm the removal.
   - Choose **Delete objects**.
   - Notice that the `index.html` file is listed in the **Failed to delete** pane, confirming that the policy is working.

4. Choose **Close** to return to the **Objects** tab.

## Task 7: Updating the Website

5. Although you have configured a policy to prevent deletion of website files, you can still update the website by editing the HTML file and uploading it to the S3 bucket again.

6. **Edit and Upload HTML File:**
   - On your computer, load the `index.html` file into a text editor (e.g., Notepad or TextEdit).
   - Find the text "Served from Amazon S3" and replace it with "Created by <YOUR-NAME>", substituting your name (e.g., Created by Jane).
   - Save the file.
   - Return to the Amazon S3 console and upload the `index.html` file that you just edited.
   - Choose `index.html`, and in the **Actions** menu, choose the **Make public using ACL** option again.
   - Choose **Make public**.

7. Return to the web browser tab with the static website and refresh the page.
   - Your name should now be on the page.











