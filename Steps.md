

| **Step**                           | **Description**                                                                                                                                                  | **Commands/Actions**                                                                                                                                                                                                                                                                                          |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Step 1: Prepare Your Documentation Site Locally** |                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                |
| 1.1 **Build the Static Site Locally**   | Set up and build your static site locally using Jekyll or another static site generator like Hugo.                                                               | **Jekyll:**<br> `jekyll build`<br> **Hugo:**<br> `hugo`<br> The generated static files will be in `_site` (Jekyll) or `public` (Hugo).                                                                                                                                                                          |
| **Step 2: Set Up Hosting on Hostinger** |                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                |
| 2.1 **Log In to Hostinger**           | Log in to your Hostinger account.                                                                                                                                | Go to [Hostinger](https://www.hostinger.com/) and log in.                                                                                                                                                                                                                                                      |
| 2.2 **Set Up a Domain or Subdomain**  | Set up a domain or subdomain where your documentation will be hosted.                                                                                            | Navigate to “Domains” in the Hostinger dashboard and manage your domain.                                                                                                                                                                                                                                       |
| 2.3 **Upload Files to Hostinger**    | Upload your static site files to Hostinger's `public_html` directory.                                                                                             | In the Hostinger dashboard, go to “Hosting,” select your website, click “Manage,” then use the “File Manager” under the “Files” section to upload the static site files to `public_html`.                                                                                                                      |
| 2.4 **Configure the Site**           | Ensure that the `index.html` file is in the root of the `public_html` directory and configure it according to your domain or subdomain settings.                  | Verify that `index.html` is correctly placed and your subdomain points to the correct folder.                                                                                                                                                                                                                   |
| **Step 3: Automate Deployment with GitHub Actions (Optional)** |                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                |
| 3.1 **FTP Credentials**             | Find or create FTP credentials on Hostinger.                                                                                                                     | In Hostinger, go to “FTP Accounts” under the “Files” section to find or create FTP credentials.                                                                                                                                                                                                                 |
| 3.2 **GitHub Actions for FTP Deployment** | Set up a GitHub Actions workflow to deploy your site to Hostinger via FTP automatically.                                                                          | Create `.github/workflows/deploy.yml` with the provided workflow script.                                                                                                                                                                                                                                       |
| 3.3 **Set Up Secrets in GitHub**    | Add your Hostinger FTP credentials to GitHub as secrets.                                                                                                         | Go to GitHub repository settings, under "Secrets and variables" > "Actions", add `FTP_USERNAME` and `FTP_PASSWORD` as secrets.                                                                                                                                                                                 |
| 3.4 **Test the Workflow**           | Commit and push your changes to trigger the deployment workflow.                                                                                                 | Push to the `main` branch. The GitHub Action will automatically build and deploy your site to Hostinger.                                                                                                                                                                                                       |
| **Step 4: Verify and Maintain**       |                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                |
| 4.1 **Access Your Site**            | Visit the domain or subdomain to check if the site is correctly deployed.                                                                                         | Access your website via the domain/subdomain to verify the deployment.                                                                                                                                                                                                                                         |
| 4.2 **Troubleshooting**             | If issues arise, check GitHub Actions logs and Hostinger File Manager.                                                                                           | Review the logs in GitHub Actions or check the file placement in the Hostinger File Manager.                                                                                                                                                                                                                   |
| 4.3 **Update Your Site**            | When updates are made to your documentation, push the changes to GitHub, and the automated GitHub Action will redeploy the site.                                 | Make changes locally, commit, and push to GitHub. The GitHub Action will handle the build and redeployment automatically.                                                                                                                                                                                       |



Amazon Web Services (AWS) doesn't need to be part of the process for deploying your site on Hostinger. However, if you want to integrate AWS into the process for additional features or a different setup, here’s how AWS could come into the picture:

### Potential AWS Integration Points

1. **Hosting on AWS Instead of Hostinger**:
   - **Amazon S3 (Simple Storage Service)**: You can host your static site on an S3 bucket, which is designed for storing and serving static content.
   - **Amazon CloudFront**: You can use CloudFront, a content delivery network (CDN), to distribute your content globally, providing faster load times for your documentation site.

2. **Using AWS for CI/CD**:
   - **AWS CodePipeline and CodeBuild**: Instead of using GitHub Actions, you could use AWS CodePipeline for CI/CD, which allows you to build, test, and deploy your documentation site using AWS services.

3. **Storage and Data**:
   - **Amazon RDS or DynamoDB**: If your documentation site needs to store or retrieve data dynamically, you could integrate it with AWS databases.

4. **Lambda Functions**:
   - **AWS Lambda**: If you want to run serverless functions, like processing data or dynamically generating content, AWS Lambda could be used.

### Example: Hosting on AWS S3 and Using CloudFront

If you decide to host your documentation on AWS S3 and use CloudFront, here’s a general overview of the process:

1. **Create an S3 Bucket**:
   - Log in to your AWS account.
   - Create a new S3 bucket and configure it for static website hosting.
   - Upload your static site files (e.g., `_site` for Jekyll or `public` for Hugo) to the S3 bucket.

2. **Set Up CloudFront**:
   - Create a CloudFront distribution, which will serve your S3 bucket content globally with low latency.
   - Point your domain or subdomain to the CloudFront distribution.

3. **CI/CD with GitHub Actions**:
   - Use GitHub Actions to automatically deploy your site to the S3 bucket.
   - A GitHub Actions workflow might look like this:
     ```yaml
     name: Deploy to AWS S3

     on:
       push:
         branches:
           - main

     jobs:
       deploy:
         runs-on: ubuntu-latest

         steps:
           - name: Checkout code
             uses: actions/checkout@v2

           - name: Build site
             run: |
               bundle install
               jekyll build

           - name: Deploy to S3
             run: |
               aws s3 sync ./_site s3://your-bucket-name --delete
             env:
               AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
               AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
     ```

4. **Point Your Domain**:
   - Update your domain’s DNS settings to point to the CloudFront distribution.

By integrating AWS, you can leverage their powerful services for hosting, content delivery, and more. However, if you're comfortable with Hostinger and your requirements are straightforward, AWS might not be necessary for your initial setup. 

Amazon Web Services (AWS) doesn't need to be part of the process for deploying your site on Hostinger. However, if you want to integrate AWS into the process for additional features or a different setup, here’s how AWS could come into the picture:

### Potential AWS Integration Points

1. **Hosting on AWS Instead of Hostinger**:
   - **Amazon S3 (Simple Storage Service)**: You can host your static site on an S3 bucket, which is designed for storing and serving static content.
   - **Amazon CloudFront**: You can use CloudFront, a content delivery network (CDN), to distribute your content globally, providing faster load times for your documentation site.

2. **Using AWS for CI/CD**:
   - **AWS CodePipeline and CodeBuild**: Instead of using GitHub Actions, you could use AWS CodePipeline for CI/CD, which allows you to build, test, and deploy your documentation site using AWS services.

3. **Storage and Data**:
   - **Amazon RDS or DynamoDB**: If your documentation site needs to store or retrieve data dynamically, you could integrate it with AWS databases.

4. **Lambda Functions**:
   - **AWS Lambda**: If you want to run serverless functions, like processing data or dynamically generating content, AWS Lambda could be used.

### Example: Hosting on AWS S3 and Using CloudFront

If you decide to host your documentation on AWS S3 and use CloudFront, here’s a general overview of the process:

1. **Create an S3 Bucket**:
   - Log in to your AWS account.
   - Create a new S3 bucket and configure it for static website hosting.
   - Upload your static site files (e.g., `_site` for Jekyll or `public` for Hugo) to the S3 bucket.

2. **Set Up CloudFront**:
   - Create a CloudFront distribution, which will serve your S3 bucket content globally with low latency.
   - Point your domain or subdomain to the CloudFront distribution.

3. **CI/CD with GitHub Actions**:
   - Use GitHub Actions to automatically deploy your site to the S3 bucket.
   - A GitHub Actions workflow might look like this:
     ```yaml
     name: Deploy to AWS S3

     on:
       push:
         branches:
           - main

     jobs:
       deploy:
         runs-on: ubuntu-latest

         steps:
           - name: Checkout code
             uses: actions/checkout@v2

           - name: Build site
             run: |
               bundle install
               jekyll build

           - name: Deploy to S3
             run: |
               aws s3 sync ./_site s3://your-bucket-name --delete
             env:
               AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
               AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
     ```

4. **Point Your Domain**:
   - Update your domain’s DNS settings to point to the CloudFront distribution.

By integrating AWS, you can leverage their powerful services for hosting, content delivery, and more. However, if you're comfortable with Hostinger and your requirements are straightforward, AWS might not be necessary for your initial setup.