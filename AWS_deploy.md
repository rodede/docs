# Plan (codex)
- Pick deployment target details (EB platform/region, app & env names, instance size) and confirm build artifact (Spring Boot jar).
- Add a GitHub Actions workflow to build the app (Maven + Vaadin) and generate the JAR.
- Add a deploy step in the workflow (EB CLI or AWS deploy action) and store AWS credentials in GitHub Secrets.
- Configure EB environment settings (port, health check path, JVM opts) and validate the first deployment.

## Step 1: define the EB target.
  - AWS region                                -> `eu-north-1`
  - EB app name                               -> `mpbridge`
  - EB environment name                       -> `mpbridge-dev`
  - Instance size                             -> `t3.micro` 
  - Health check path                         -> `/actuator/health`

## Step2: add GitHub Actions workflow 
- build production JAR on pushes/PRs to main & uploads artifacts -> 
`github/workflows/build.yml`

## Step3: AWS access keys from an IAM user (or role). Quick path:
- In AWS Console → IAM → Users → Create user -> mpbridge-deploy
- Attach policies: 
        - AWSElasticBeanstalkWebTier
        - AmazonS3FullAccess
        - CloudWatchLogsFullAccess
** You’ll also need “who is running what” roles in EB
Even if your deploy user has these policies, Elastic Beanstalk itself needs:
an instance profile role for the EC2 instances (to push logs, read S3 bundle, etc.)
a service role for EB (some accounts auto-create these)
If your first deploy fails with a message about missing roles like aws-elasticbeanstalk-ec2-role or aws-elasticbeanstalk-service-role, that’s the reason — and it’s fixed in the EB console by creating/assigning the default roles.
- Create Access key for that user and copy:
      - Access key ID → AKIA2PX4YZDYWJUXOJOP
      - Secret access key → dx

## Step4: Store the keys in GitHub Secrets
Go to Settings → Secrets and variables → Actions
Click New repository secret - create these secrets exactly with these names:
AWS_ACCESS_KEY_ID	(Access key ID)
AWS_SECRET_ACCESS_KEY	(Secret access key)
AWS_REGION	eu-north-1

## Step5: create the EB app + environment in the AWS Console once
This is the “do it once, then CI/CD just deploys versions” approach.
Go to Elastic Beanstalk → Create application
- Application name: e.g. mpbridge
- Environment: Web server environment
- Platform: Java (pick your Java version)
- For “Application code”: you can choose Sample application (fine for bootstrap)
- Click Create

Result: EB will also create its regional storage bucket named like
elasticbeanstalk-eu-north-1-<account-id> automatically.

## Step5: add a deploy workflow to Elastic Beanstalk using GitHub Secrets.
`github/workflows/deploy-eb.yml`:
- Builds the JAR
- Uploads it to the EB S3 bucket
- Creates an EB application version
- Updates the mpbridge-dev environment

 * Add a JAVA_OPTS section in the Procfile for memory tuning.
 java $JAVA_OPTS -jar application.jar
 * make the app/env names configurable via workflow inputs.
• That would let you choose the EB app/environment when you manually run the workflow, instead of hardcoding them.
  Example: when you click “Run workflow,” you can pick mpbridge-dev or mpbridge-prod. It’s optional—useful later if
  you add multiple environments.

* set the EB environment health check to /actuator/health in the EB console. 

## Step6: Trigger the Deploy workflow from GitHub Actions (manual run).
  1. Open your repo → Actions tab.
  2. In the left sidebar, click Deploy to Elastic Beanstalk.
  3. Click Run workflow (top right).
  4. Choose branch (usually main) and confirm.

