# Deploy

## Build

- Creating a state optimized for deployment by removing unnecessary data and integrating/compressing data spread across multiple branches
- Compared to before the build process, there are advantages of **reduced data capacity** and **faster website loading speed**
- Build in the general sense means the **compilation process of converting source code into executable bundles**
- It's slightly different for web apps deployed in HTML, CSS, JS format, and web apps must be made into **static files** that can be deployed

<br/>

## Deployment

- A series of processes to make developed services available to users
- In deployment, it's important to understand environmental differences and **separate environment configuration from code**

### 4 Stages of Deployment

- **Development**

  - Process of writing and testing code on each person's computer
  - Since it's the development stage, testing is done with dummy data instead of real data

- **Integration**

  - Process of combining code written on each person's computer
  - Checking whether my written code doesn't interfere with other code causing errors, and checking for conflicts between codes

- **Staging**

  - Testing in an environment most similar to the Production stage, which is the actual release stage
  - Testing in various environments by copying real data to check for problems
  - May also go through verification processes by relevant departments or personnel

- **Production**
  - Stage of releasing the developed service
  - Running code in the Production environment where users can access and providing the service
  - Since the service operates with real data, this is a stage where problems should not occur

<br/>

## How to Make Written Code Work Properly in Different Environments?

- Use relative paths instead of absolute paths
- Set environment variables (env) to branch ports according to environment
  - Environment variables can be easily changed for each deployment without code changes
  - Unlike configuration files, there's also a lower possibility of accidentally uploading to the code repository
- Use solutions like Docker to unify the development environment itself
