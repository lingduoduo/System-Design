#### Create IAM Trust Policy for an EC2 Role

1. Create a file called `trust_policy_ec2.json`:

   ```
   [cloud_user@bastion]$ vim trust_policy_ec2.json
   ```

2. To avoid adding unnecessary spaces or hashes, type `:set paste` and then `i` to enter `insert` mode.

3. Paste in the following content:

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {"Service": "ec2.amazonaws.com"},
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

4. Save and quit the file by pressing **Escape** followed by `:wq!`.

#### Create IAM Trust Policy for an EC2 Role

1. Create a file called `trust_policy_ec2.json`:

   ```
   [cloud_user@bastion]$ vim trust_policy_ec2.json
   ```

2. To avoid adding unnecessary spaces or hashes, type `:set paste` and then `i` to enter `insert` mode.

3. Paste in the following content:

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {"Service": "ec2.amazonaws.com"},
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

4. Save and quit the file by pressing **Escape** followed by `:wq!`.

#### Create the `DEV_ROLE` IAM Role

1. Run the following AWS CLI command:

   ```
   [cloud_user@bastion]$ aws iam create-role --role-name DEV_ROLE --assume-role-policy-document file://trust_policy_ec2.json
   ```

#### Create an IAM Policy Defining Read-Only Access Permissions to an S3 Bucket

1. Create a file called `dev_s3_read_access.json`:

   ```
   [cloud_user@bastion]$ vim dev_s3_read_access.json
   ```

2. To avoid adding unnecessary spaces or hashes, type `:set paste` and then `i` to enter `insert` mode.

3. Enter the following content, replacing `<DEV_S3_BUCKET_NAME>` with the bucket name provided in the `labreferences.txt` file:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
             "Sid": "AllowUserToSeeBucketListInTheConsole",
             "Action": ["s3:ListAllMyBuckets", "s3:GetBucketLocation"],
             "Effect": "Allow",
             "Resource": ["arn:aws:s3:::*"]
           },
           {
               "Effect": "Allow",
               "Action": [
                   "s3:Get*",
                   "s3:List*"
               ],
               "Resource": [
                   "arn:aws:s3:::<DEV_S3_BUCKET_NAME>/*",
                   "arn:aws:s3:::<DEV_S3_BUCKET_NAME>"
               ]
           }
       ]
   }
   ```

4. Save and quit the file by pressing **Escape** followed by `:wq!`.

5. Create the managed policy called `DevS3ReadAccess`:

   ```
   [cloud_user@bastion]$ aws iam create-policy --policy-name DevS3ReadAccess --policy-document file://dev_s3_read_access.json
   ```

6. Copy the policy ARN in the output, and paste it into the `labreferences.txt` file — we'll need it in a minute.

### Create Instance Profile and Attach Role to an EC2 Instance

#### Attach Managed Policy to Role

1. Attach the managed policy to the role, replacing `<DevS3ReadAccess_POLICY_ARN>` with the ARN you just copied:

   ```
   [cloud_user@bastion]$ aws iam attach-role-policy --role-name DEV_ROLE --policy-arn "<DevS3ReadAccess_POLICY_ARN>"
   ```

2. Verify the managed policy was attached:

   ```
   [cloud_user@bastion]$ aws iam list-attached-role-policies --role-name DEV_ROLE
   ```

#### Create the Instance Profile and Add the `DEV_ROLE` via the AWS CLI

1. Create instance profile named `DEV_PROFILE`:

   ```
   [cloud_user@bastion]$ aws iam create-instance-profile --instance-profile-name DEV_PROFILE
   ```

2. Add role to the `DEV_PROFILE` called `DEV_ROLE`:

   ```
   [cloud_user@bastion]$ aws iam add-role-to-instance-profile --instance-profile-name DEV_PROFILE --role-name DEV_ROLE
   ```

3. Verify the configuration:

   ```
   [cloud_user@bastion]$ aws iam get-instance-profile --instance-profile-name DEV_PROFILE
   ```

#### Attach the `DEV_PROFILE` Role to an Instance

1. In the AWS console, navigate to **EC2** > **Instances**.

2. Copy the instance ID of the instance named *Web Server* instance and paste it into the `labreferences.txt` file — we'll need it in a second.

3. In the terminal, attach the `DEV_PROFILE` to an EC2 instance, replacing `<LAB_WEB_SERVER_INSTANCE_ID>` with the *Web Server* instance ID you just copied:

   ```
   [cloud_user@bastion]$ aws ec2 associate-iam-instance-profile --instance-id <LAB_WEB_SERVER_INSTANCE_ID> --iam-instance-profile Name="DEV_PROFILE"
   ```

4. Verify the configuration (be sure to replace `<LAB_WEB_SERVER_INSTANCE_ID>` with the *Web Server* instance ID again):

   ```
   [cloud_user@bastion]$ aws ec2 describe-instances --instance-ids <LAB_WEB_SERVER_INSTANCE_ID>
   ```

   This command's output should show this instance is using `DEV_PROFILE` as an `IamInstanceProfile`. Verify this by locating the `IamInstanceProfile` section in the output, and look below to make sure the `"Arn"` ends in `/DEV_PROFILE`.

### Test S3 Permissions via the AWS CLI

1. In the AWS console, copy the public IP of the *Web Server* instance.

2. Open a new terminal.

3. Log in to the web server instance via SSH:

   ```
   ssh cloud_user@<WEB_SERVER_PUBLIC_IP>
   ```

4. Use the same password for the bastion host provided on the lab page.

5. Verify the instance is assuming the `DEV_ROLE` role:

   ```
   [cloud_user@webserver]$ aws sts get-caller-identity
   ```

   We should see `DEV_ROLE` in the `Arn`.

6. List the buckets in the account:

   ```
   [cloud_user@webserver]$ aws s3 ls
   ```

   Copy the entire name (starting with `cfst`) of the bucket with `s3bucketdev` in its name.

7. Attempt to view the files in the `s3bucketdev-` bucket, replacing `<s3bucketdev-123>` with the bucket name you just copied:

   ```
   [cloud_user@webserver]$ aws s3 ls s3://<s3bucketdev-123>
   ```

   We should see a list of files.

### Create an IAM Policy and Role Using the AWS Management Console

#### Create Policy

1. In the AWS console, navigate to **IAM** > **Policies**.

2. Click **Create policy**.

3. Click the **JSON** tab.

4. Paste the following text as the policy, replacing `<PROD_S3_BUCKET_NAME>` with the bucket name provided in the `labreferences.txt` file:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
             "Sid": "AllowUserToSeeBucketListInTheConsole",
             "Action": ["s3:ListAllMyBuckets", "s3:GetBucketLocation"],
             "Effect": "Allow",
             "Resource": ["arn:aws:s3:::*"]
           },
           {
               "Effect": "Allow",
               "Action": [
                   "s3:Get*",
                   "s3:List*"
               ],
               "Resource": [
                   "arn:aws:s3:::<PROD_S3_BUCKET_NAME>/*",
                   "arn:aws:s3:::<PROD_S3_BUCKET_NAME>"
               ]
           }
       ]
   }
   ```

5. Click **Next: Tags**.

6. Click **Next: Review**.

7. Enter **ProdS3ReadAccess** as the policy name.

8. Click **Create policy**.

#### Create Role

1. Click **Roles** in the left-hand menu.
2. Click **Create role**.
3. Under *Choose a use case*, select **EC2**.
4. Click **Next: Permissions**.
5. In the *Filter policies* search box, enter **ProdS3ReadAccess**.
6. Click the checkbox to select **ProdS3ReadAccess**.
7. Click **Next: Tags**.
8. Click **Next: Review**.
9. Give it a *Role name* of **PROD_ROLE**.
10. Click **Create role**.

### Attach IAM Role to an EC2 Instance Using the AWS Management Console

1. Navigate to **EC2** > **Instances**.
2. Select the *Web Server* instance.
3. Click **Actions** > **Security** > **Modify IAM role**.
4. In the *IAM role* dropdown, select **PROD_ROLE**.
5. Click **Save**.

#### Test the Configuration

1. Open the existing terminal connected to the *Web Server* instance. (You may need to reconnect if you've been disconnected.)

2. Determine the identity currently being used:

   ```
   [cloud_user@webserver]$ aws sts get-caller-identity
   ```

   This time, we should see `PROD_ROLE` in the `Arn`.

3. List the buckets:

   ```
   [cloud_user@webserver]$ aws s3 ls
   ```

4. Copy the entire name (starting with `cfst`) of the bucket with `s3bucketprod` in its name.

5. Attempt to view the files in the `s3bucketprod-` bucket, replacing `<s3bucketprod-123>` with the bucket name you just copied:

   ```
   [cloud_user@webserver]$ aws s3 ls s3://<s3bucketprod-123>
   ```

   It should list the files.

6. In the `aws s3 ls` command output, copy the entire name (starting with `cfst`) of the bucket with `s3bucketsecret` in its name.

7. Attempt to view the files in the `<s3bucketsecret-123>` bucket, replacing `<s3bucketsecret-123>` with the bucket name you just copied:

   ```
   [cloud_user@webserver]$ aws s3 ls s3://<s3bucketsecret-123>
   ```

   This time, our access will be denied — which means our configuration is properly set up.