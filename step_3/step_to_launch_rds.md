# Step-by-Step Guide to RDS

## Step 1: Choose a Relational Database Engine

1. Log in to the AWS Management Console.
2. Navigate to **RDS** under the **Database** section.
3. Click on **Create database**.
4. Choose a database creation method:
   - **Standard Create** is recommended for more configuration options.
5. Select your desired **Database Engine** (PostgreSQL).

### Database Configuration

- **DB Instance Class**: `db.t3.micro` (for development/testing)
- **Allocated Storage**: `20 GB`
- **Storage Type**: `General Purpose SSD (gp2)`
- **Storage Auto Scaling**: Enabled
- **DB Instance Identifier**: `chocfactory-db`
- **Master Username**: `chocfactory_user`
- **Master Password**: `YourStrongPassword!123`

## storage
- keep the storage the same enabling auto scaling

## connectivity 
- select connect to an EC2 compute resource
- select the ec2
- select automatic setup

## security group
- select create new vpc secuirty group
- **name**:ChocFactory-RDS-SG
