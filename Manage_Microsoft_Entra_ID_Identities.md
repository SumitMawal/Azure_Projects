# Manage Microsoft Entra ID Identities

## Introduction

- ### What is Entra ID?

    Microsoft Entra ID is a cloud-based identity and access management service provided by Microsoft. Microsoft Entra ID is a comprehensive solution for managing identities, enforcing access policies, and securing your applications and data in the cloud and on-premises.
    With Microsoft Entra ID, you also have access to a set of features that aren’t natively available in AD DS, such as support for multi-factor authentication, identity protection, and self-service password reset.

- ### What is tenant?

    The term tenant in this context typically represents a company or organization that signed up for a subscription to a Microsoft cloud-based service such as Microsoft 365, Intune, or Azure, each of which uses Microsoft Entra ID. However, from a technical standpoint, the term tenant represents an individual Microsoft Entra instance.
    At any given time, an Azure subscription must be associated with one, and only one, Microsoft Entra tenant. This association allows you to grant permissions to resources in the Azure subscription (via RBAC) to users, groups, and applications that exist in that particular Microsoft Entra tenant.
 
> [!NOTE]
> You can associate the same Microsoft Entra tenant with multiple Azure subscriptions. This allows you to use the same users, groups, and applications to manage resources across multiple Azure subscriptions.
 
## Architecture diagram

 ![image](https://github.com/user-attachments/assets/cfcd2bae-8ddb-47b9-a12f-b35652c359b1)

  - **Task 1:** Create and configure user accounts.
  - **Task 2:** Create groups and add members.

- ### Task 1: Create and configure user accounts:
    - Create a new user
    - Invite an external user

   ![image](https://github.com/user-attachments/assets/a7198880-0ded-4c77-b123-5404a1e283c1)

- ### Task 2: Create groups and add members

    ![image](https://github.com/user-attachments/assets/854f02be-a950-421a-89f4-b4fbaa70ee8e)

    ![image](https://github.com/user-attachments/assets/6e3d4002-da7e-4bb1-b2be-5d92f1ba2820)

    ![image](https://github.com/user-attachments/assets/3f1b4e6d-30cc-4d51-82e9-0ba5103f7562)

    When you delete a user, the account remains in a suspended state for 30 days. During that 30-day window, you can restore the user account.

 

## Access management in Microsoft Entra ID
  - **Microsoft Entra roles:** Use Microsoft Entra roles to manage Microsoft Entra ID-related resources like users, groups, billing, licensing, application registration, and more.
  - **Role-based access control (RBAC) for Azure resources:** Use RBAC roles to manage access to Azure resources like virtual machines, SQL databases, or storage. For example, you could assign an RBAC role to a user to manage and delete SQL databases in a specific resource group or subscription.

## Access rights through single user or group assignment

  There are different ways you can assign access rights:
  
  - **Direct assignment:** Assign a user the required access rights by directly assigning a role that has those access rights.
  - **Group assignment:** Assign a group the required access rights, and the group members will inherit those rights.
  - **Rule-based assignment:** Use rules to determine a group membership based on user or device properties. For a user account or device's group membership to be valid, the user or device must meet the rules. If the rules aren't met, the user account or device's group membership is no longer valid. The rules can be simple. You can select prewritten rules or write your own advanced rules.

