<h1>Using Amazon Macie to find PII on S3 Buckets</h1>

<h2>Description</h2>

Amazon Macie is a valuable tool for identifying and protecting Personally Identifiable Information (PII) in your Amazon S3 buckets. Here’s why it’s important to use Macie for this purpose:

Automated Data Discovery: Macie automatically discovers and classifies sensitive data stored in your S3 buckets. This helps in identifying PII like social security numbers, credit card information, and other sensitive data without manual intervention.

Compliance and Data Privacy: Many regulations, such as GDPR, CCPA, and HIPAA, require organizations to protect PII and ensure data privacy. Macie helps you comply with these regulations by providing detailed insights into where your sensitive data is stored and how it is being used.

Risk Management: By detecting PII and other sensitive data, Macie helps you understand and manage the risks associated with data breaches or unauthorized access. This proactive approach enables you to take necessary actions to protect your data and minimize potential damage.

By leveraging AWS Macie to scan for PII in S3 buckets, you enhance your organization’s ability to protect sensitive data, comply with regulations, and effectively manage data security risks.
<br />
<h2>Example Data:</h2>

****************************************Credit Card Details - creditcards.txt****************************************
```python
American Express
358471835184008 05/27
CVE: 450

American Express
754583025756934 07/29
CCV: 4785

Mastercard
051051051501510
Exp: 04/28
Security code: 001
```

<h3>Step 1 - Create an S3 bucket and add example data </h3> 
Save the example data above as text files and then head to the S3 console: https://s3.console.aws.amazon.com/s3/buckets

Click "Create Bucket"

The S3 bucket name must be unique. All configurations can be left as default. Click "Create Bucket"

Access your bucket and upload the text files that you saved earlier.

![369508056-eff7e60e-5cba-4743-a650-a7a134c547af](https://github.com/user-attachments/assets/3a648eab-25eb-41a9-ad6e-7a8244016c93)

<h3>Step 1 - Enabling Amazon Macie </h3> 

Head to the Amazon Macie console and make sure that you are in the same region as the S3 bucket.

Select "Get Started" and then "Enable Macie"

Once Macie is enabled, it will take a couple minutes for it to be ready. Once it is, you will see a screen similar to this:

![Macie](/Amazon-Macie/Images/macie.png)

Head to the "S3 Buckets" section and select "Create Job"

Select the S3 bucket that you created and press "Next" until you reach the "Refine the scope" section.

Select "One time job" and continue pressing "Next" until you reach the "General settings" section.

Name the job anything you'd like and submit the job when finished.

It may take 10-20 minutes for the job to complete. To find the results, select the job, press "Show Results" and then "Show Findings"

<h3>Step 3 - Setting up SNS </h3> 

Head to the SNS Console.

Click on "Create Topic"

Set the type to "Standard"

Set the name to "Macie-Alerts"

Set the Publishers and subscribers to "Only the specified AWS accounts" and add your account ID, found on the top right.

Leave everything else as default and click "Create Topic"

Click "Create Subscription" and change the Protocol to Email.

In the Endpoint section, add your personal email.

Click on "Create Subscription. You will soon recieve an email with a link confirming that SNS can continue sending you emails.

Your subscription will now be in a confirmed state.

![SNS](/Amazon-Macie/Images/SNS.png)

<h3>Step 3 - Setting up EventBridge </h3> 

Head to the EventBridge Console.

Select "EventBridge Rule" and click "Create Rule"

Set the name to "Macie-Events" and click "Next"

Scroll down to Create Method and select "Pattern Form"

Set the AWS Service to "Macie" and Event Type to "Macie Finding"

Click "Next"

Choose "SNS Topic" as your target and then select your SNS topic.

Click "Next" and then "Create Rule"

<h3>Step 3 - Adding a Cutom Macie Data Identifier </h3> 


