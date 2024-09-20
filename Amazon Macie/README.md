<h1>Using Amazon Macie to find PII on S3 Buckets</h1>

<h2>Description</h2>

Amazon Macie is a valuable tool for identifying and protecting Personally Identifiable Information (PII) in your Amazon S3 buckets. Here’s why it’s important to use Macie for this purpose:

Automated Data Discovery: Macie automatically discovers and classifies sensitive data stored in your S3 buckets. This helps in identifying PII like social security numbers, credit card information, and other sensitive data without manual intervention.

Compliance and Data Privacy: Many regulations, such as GDPR, CCPA, and HIPAA, require organizations to protect PII and ensure data privacy. Macie helps you comply with these regulations by providing detailed insights into where your sensitive data is stored and how it is being used.

Risk Management: By detecting PII and other sensitive data, Macie helps you understand and manage the risks associated with data breaches or unauthorized access. This proactive approach enables you to take necessary actions to protect your data and minimize potential damage.

By leveraging AWS Macie to scan for PII in S3 buckets, you enhance your organization’s ability to protect sensitive data, comply with regulations, and effectively manage data security risks.
<br />
<h2>Example Data:</h2>

****************************************Drivers License Numbers - license.txt****************************************

```python
John Doe
Pennsylvania
99-999-999

Jane Doe
Texas
210-555-555
```

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

****************************************USA Social Security Numbers - socials.txt****************************************
```
Josh
123-45-6789

Jake
000-00-000
```
<h2>Lab walk-through:</h2>

<h3>Step 1 - Create an S3 bucket and add example data </h3> 
Save the example data above as text files and then head to the S3 console: https://s3.console.aws.amazon.com/s3/buckets

Click "Create Bucket"

The S3 bucket name must be unique. All configurations can be left as default. Click "Create Bucket"

Access your bucket and upload the text files that you saved earlier.


