# aws-wordpress
Here’s a step-by-step tutorial on how to deploy WordPress on AWS using CloudFormation with the YAML template provided above. This guide assumes that you already have an AWS account and a basic understanding of AWS services. If not, you can sign up and follow the necessary setup procedures before proceeding.

### Step 1: Prerequisites

Before you deploy the CloudFormation template, ensure you have:

1. **AWS Account**: You’ll need access to an AWS account. Sign up [here](https://aws.amazon.com/) if you don’t have one.
2. **Key Pair**: Create an EC2 Key Pair for SSH access to the instance. This will allow you to connect to your EC2 instance for troubleshooting, if necessary.
   - Navigate to the **EC2 Dashboard** -> **Key Pairs** -> **Create Key Pair**.
   - Save the private key file (`.pem`) securely as it will be used to access the EC2 instance.

### Step 2: Prepare the CloudFormation YAML Template

Create a YAML file called `wordpress-test.yml` and add the following CloudFormation template code. This will define the infrastructure required for your WordPress application, including EC2, RDS, and security groups:

```yaml
# Paste the YAML code provided earlier here
```

### Step 3: Upload and Deploy the CloudFormation Template

1. **Sign in to the AWS Management Console**.
2. **Navigate to CloudFormation**:
   - In the AWS Management Console, search for **CloudFormation** in the search bar and click on **CloudFormation**.
3. **Create a Stack**:
   - Click on **Create Stack** and choose **With new resources (standard)**.
   - Select **Upload a template file**, and then upload the `wordpress-test.yml` file you created.
4. **Configure Stack Details**:
   - **Stack Name**: Enter a name like `wordpress-test`.
   - **Parameters**: Fill in the required parameters:
     - **KeyName**: Enter the name of the EC2 Key Pair you created earlier.
     - **DBUsername**: Enter a username for the MySQL database (e.g., `admin`).
     - **DBPassword**: Enter a strong password for the MySQL database.
5. **Configure Stack Options**: Leave the options as default unless you need to modify them.
6. **Create Stack**:
   - Click on **Create Stack**. CloudFormation will now begin creating your resources. This process may take a few minutes.

### Step 4: Monitor the Stack Creation

1. **View Events**:
   - On the CloudFormation page, you can monitor the progress of the stack by clicking on the **Events** tab.
   - CloudFormation will show the creation status of each resource (e.g., EC2, RDS, Security Groups).
2. **Wait for Completion**:
   - Wait until the stack status changes to `CREATE_COMPLETE`.

### Step 5: Access Your WordPress Site

1. **Get the Website URL**:
   - After the stack creation is complete, go to the **Outputs** tab of your CloudFormation stack.
   - You will find a field labeled **WebsiteURL**. This URL points to your new WordPress site.
   - Copy the URL and paste it into your browser to complete the WordPress installation.

2. **Complete WordPress Setup**:
   - When you navigate to the URL, you will be prompted to configure your WordPress installation. Choose a language, site title, and set an admin account for WordPress.
   - Once configured, you will have a fully functional WordPress site!

### Step 6: (Optional) Connect to EC2 Instance

If you need to connect to the EC2 instance (for troubleshooting or customization):

1. **Find the EC2 Instance**:
   - Go to the **EC2 Dashboard** -> **Instances**.
   - Find the instance associated with the WordPress deployment (you can identify it by its security group or name).
2. **SSH into the EC2 Instance**:
   - Copy the public IP of the instance.
   - Use the following command (on Linux or Mac) to connect, replacing `your-key.pem` and `public-ip` with your values:

   ```bash
   ssh -i "your-key.pem" ec2-user@public-ip
   ```

   On Windows, use tools like PuTTY to connect using your `.pem` key.

### Step 7: Clean Up Resources (When Finished Testing)

To avoid ongoing charges after your testing, you can delete the CloudFormation stack, which will remove all resources associated with the deployment:

1. **Delete the Stack**:
   - In the CloudFormation dashboard, find your stack (e.g., `wordpress-test`), select it, and click **Delete**.
   - Confirm the deletion, and AWS will automatically clean up the EC2 instance, RDS database, and security groups.

---

### Next Steps

- **Scaling and Auto Healing**: You can explore AWS Auto Scaling groups and Elastic Load Balancing to ensure your WordPress site can scale and handle failure gracefully.
- **S3 and CloudFront**: For better performance, consider offloading static content to Amazon S3 and caching using CloudFront.
- **SSL/TLS Setup**: Use AWS Certificate Manager (ACM) and attach an SSL certificate to your WordPress site for secure HTTPS access.
