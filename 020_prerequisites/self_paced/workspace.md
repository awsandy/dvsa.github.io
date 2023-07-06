---
title: "Create a Workspace"
chapter: false
weight: 14
---



::alert[This workshop was designed to run in the **Ireland (eu-west-1)** region. **Please don't run in any other region.** Future versions of this workshop will expand region availability, and this message will be removed.]


::alert[Ad blockers, javascript disabler, and tracking blockers should be disabled for the cloud9 domain, or connecting to the workspace might be impacted. Cloud9 requires third-party-cookies. You can whitelist the [specific domains](https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-env-loading).]

### Launch Cloud9 in your closest region:

Create a Cloud9 Environment using this link: [https://console.aws.amazon.com/cloud9/home](https://console.aws.amazon.com/cloud9/home)



- Click `Create environment`

On the next page:

- Name it **eks-terraform**
- Click `Next`.

![c9after](/static/images/andyt/c9-create1.png)

On the next screen choose these options:


- **"Create a new no-ingress EC2 instance for environment (access via Systems Manager)"**
- **"t3.small (2GiB RAM + 2CPU)"** 
- **"Amazon Linux 2 (recommended)"**
- Set the Cost-saving setting to **"After one hour"**
- And click `Next Step`

![c9after](/static/images/andyt/c9-create2.png)


On the Review page double check the Name is set to "eks-terraform" and then click `Create environment`

----

When it comes up, customize the environment by closing the **welcome tab**
and **lower work area**, and opening a new **terminal** tab in the main work area:
![c9before](/static/images/c9before.png)

- Your workspace should now look like this:
![c9after](/static/images/c9after.png)

- If you like this theme, you can choose it yourself by selecting **View / Themes / Solarized / Solarized Dark**
in the Cloud9 workspace menu.
