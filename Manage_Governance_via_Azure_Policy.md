# Manage Governance via Azure Policy

## Introduction

  In response to the rapid expansion of organization’s cloud footprint and the discovery of numerous untagged resources during a audit, this project aims to enhance the management and governance of Azure resources. The key objectives include:

  - **Applying resource tags** to attach essential metadata such as owner, project, and cost centre to Azure resources.
  - **Enforcing the use of resource tags** for all new resources through Azure Policy.
  - **Updating existing resources** with appropriate resource tags.
  - **Implementing resource locks** to safeguard critical resources from accidental modifications or deletions.
    
  This project ensures better resource organization, cost management, and compliance with organizational standards.
  
  We can overcome the challenges included identifying untagged resources, ensuring Azure Policy enforcement without disrupting workflows, retagging existing resources without downtime, and balancing resource locks with management flexibility by following above mentioned key objectives.

  ### What is tags in Azure?

  Tags in Azure are metadata elements consisting of key-value pairs that help organize and manage resources. They allow you to categorize resources by various criteria like environment, department, or project, making it easier to track and manage costs and usage.

  ### What is resource lock in Azure?

  A resource lock in Azure is a setting that prevents accidental deletion or modification of resources. There are two types: ReadOnly (resources can be read but not modified or deleted) and CanNotDelete (resources can be modified but not deleted).
  
  ### What is Azure policy?

  Azure Policy is a service that helps enforce organizational standards and assess compliance at scale. It allows you to create, assign, and manage policies that govern resource properties, ensuring they meet business rules and regulatory requirements.

  ### What is the differences between Azure policy and Azure RBAC?

  Azure Policy and Azure Role-Based Access Control (RBAC) serve different purposes in managing Azure resources:
    -	**Azure Policy:** Ensures resources comply with organizational standards. It governs resource properties and enforces rules like allowed VM sizes or mandatory tags.
    -	**Azure RBAC:** Manages user permissions and access to resources. It controls who can perform actions like creating or deleting resources.
    
  **Key Difference:** Azure Policy focuses on resource compliance, while Azure RBAC focuses on user access.

  ![image](https://github.com/user-attachments/assets/6c72b3f6-2c57-41ab-b09e-790ca66683c6)

-	Task 1: Create and assign tags via the Azure portal.
-	Task 2: Enforce tagging via an Azure Policy.
-	Task 3: Apply tagging via an Azure Policy.
-	Task 4: Configure and test resource locks.
  
## Assign tags via the Azure portal

  In this task, I have created and assigned a tag to an Azure resource group via the Azure portal. Tags can allow you to quickly identify resource owners, sunset dates, group contacts, and other name/value pairs that your organization deems important. For this task, I assigned a tag identifying the resource role.

  ![image](https://github.com/user-attachments/assets/cae59c46-604e-4caa-9a7a-e603cb89541b)

## Enforce tagging via an Azure Policy

  In this task, I assigned the built-in **`“Require a tag and its value on resources”`** policy to the resource group and evaluated the outcome. Azure Policy can be used to enforce configuration and governance on your Azure resources.

  ![image](https://github.com/user-attachments/assets/14e70ea7-dcac-49d8-a6cf-09c38965be0f)

  The Assignment name is automatically populated with the policy name we selected, but we can change it. I have changed it to **`“Require Cost Center tag with Default value”`** for my convenience.

  ![image](https://github.com/user-attachments/assets/94333155-45c7-4de8-82a7-563e48607e34)

  By default, this assignment will only take effect on newly created resources. Existing resources can be updated via a remediation task after the policy is assigned. For ***`deployIfNotExists`*** policies, the remediation task will deploy the specified template. For modify policies, the remediation task will edit tags on the existing resources.

> [!NOTE]
> We can assign policies on the management group, subscription, or resource group level. We also have the option of specifying exclusions, such as individual subscriptions, resource groups, or resources. In this scenario, I want the tag on all the resources in the resource group.

**Testing:**

I verified the new policy assignment by attempting to create an Azure Storage account within the resource group without adding the required tag.

 ![image](https://github.com/user-attachments/assets/549eca2d-ebf0-427b-bbfc-bea7c4d0ffc7)

The deployment failed because the storage account I attempted to create did not have a tag named Cost Centre with its value set to Default.

## Apply tagging via an Azure policy

  In this task, I used the new policy definition to remediate any non-compliant resources. Specifically, I ensured that any child resources within a resource group inherited the Cost Center tag defined on the resource group.

  ![image](https://github.com/user-attachments/assets/1c8df081-831a-4a13-9d07-acf719222a13)

  This policy definition includes the Modify effect, which requires a managed identity. Additionally, a remediation task needs to be enabled so that existing resources can be updated via the remediation task after the policy is assigned. For ***`deployIfNotExists`*** policies, the remediation task will deploy the specified template. For modify policies, the remediation task will edit tags on the existing resources.

  ![image](https://github.com/user-attachments/assets/acc8ba81-8835-4538-8d52-24f638c56a5d)

**Testing:**

To verify that the new policy assignment is in effect, I created another Azure storage account in the same resource group without explicitly adding the required tag.
 
![image](https://github.com/user-attachments/assets/380cca61-2390-4946-8351-173b394e9a98)

On the Tags blade, note that the tag Cost Centre with the value 000 has been automatically assigned to the resource.

## Configure and test resource locks

  In this task, I configured and test a resource lock. Locks prevent either deletions or modifications of a resource.

  ![image](https://github.com/user-attachments/assets/873640bd-95bf-4c92-8c81-ed69f28b7ffe)

**Testing:**

While attempting to delete the resource group **`“az104-rg2-Sumit-Mawal”`**, I received a notification indicating that the deletion was denied. To proceed with the deletion, I need to remove the lock on the resource group.

![image](https://github.com/user-attachments/assets/190dc36f-7ddd-46d4-b2a3-0a0153fad91b)

After removing the lock I was able to delete resource group successfully.
 
![image](https://github.com/user-attachments/assets/96bd3cf6-f7d5-4ca3-825a-16f6aece490c)

## Key takeaways

  Here are the main takeaways.
  -	**Azure tags** are metadata that consists of a key-value pair. Tags describe a particular resource in your environment. In particular, tagging in Azure enables you to label your resources in a logical manner.
  -	**Azure Policy** establishes conventions for resources. Policy definitions describe resource compliance conditions and the effect to take if a condition is met. A condition compares a resource property field or a value to a required value. There are many built-in policy definitions and you can customize the policies.
  -	The **Azure Policy remediation task** feature is used to bring resources into compliance based on a definition and assignment. Resources that are non-compliant to modify or ***`deployIfNotExist`*** definition assignment, can be brought into compliance using a remediation task.
  -	You can configure a **resource lock** on a subscription, resource group, or resource. The lock can protect a resource from accidental user deletions and modifications. The lock overrides any user permissions.
  -	Azure Policy is pre-deployment security practice. RBAC and resource locks are post-deployment security practice.
