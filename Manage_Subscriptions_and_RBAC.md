# Manage Subscriptions and RBAC

## Introduction
  In this project, I focused on managing Azure subscriptions and implementing Role-Based Access Control (RBAC) to enhance security and efficiency within an organization. The project was structured around several key tasks, each aimed at building a comprehensive understanding of Azure’s subscription and access management capabilities.

 ![image](https://github.com/user-attachments/assets/536a05c1-0786-4553-bcda-cd90304a7e79)

  - **Task 1:** Implement management groups.
  -	**Task 2:** Review and assign a built-in Azure role.
  -	**Task 3:** Create a custom RBAC role.
  -	**Task 4:** Monitor role assignments with the Activity Log.

  - ### What is Management Groups?
    Management groups are used to logically organize and segment subscriptions. They allow for RBAC and Azure Policy to be assigned and inherited to other management groups and subscriptions. For example, if your organization has a dedicated support team for Europe, you can organize European subscriptions into a management group to provide the support staff access to those subscriptions (without providing individual access to all subscriptions). 

  - ### What is Built-in Azure role?
    Built-in roles in Azure are predefined roles that provide a set of permissions to perform specific actions. These roles cover common tasks and scenarios, ensuring users have the necessary access to resources without needing custom role definitions.

  - ### What is custom RBAC role?
    A custom RBAC role in Azure allows you to define specific permissions tailored to your organization’s needs. Unlike built-in roles, custom roles provide flexibility to grant only the necessary permissions, adhering to the principle of least privilege.

  - ### What is Activity logs in Azure?
    Activity logs in Azure provide insights into subscription-level events, such as resource modifications or virtual machine startups. They help track changes, monitor activities, and ensure security by logging all actions performed within the Azure environment.

## Management Groups
  The first task involved setting up management groups to organize and manage multiple Azure subscriptions effectively. Management groups provide a hierarchical structure that allows for centralized management and governance. By implementing management groups, I was able to apply policies and access controls across multiple subscriptions, ensuring consistent governance and compliance. In my scenario everyone at the Help Desk will need to create a support request across all subscriptions.
 
  ![image](https://github.com/user-attachments/assets/42a6c3ac-35c0-4bcd-938f-ac3e31bb7fb6)

## Built-in Azure Role
  The second task focused on understanding and utilizing Azure’s built-in roles. Azure provides a variety of built-in roles that cater to different access needs. Subsequently, I assigned the Virtual machine contributor role to Helpdesk group, ensuring that they had the necessary access to perform their tasks without compromising security. Virtual machine contributor role lets you manage virtual machines, but not access their operating system or manage the virtual network and storage account they are connected to. This is a good role for the Helpdesk. 

 ![image](https://github.com/user-attachments/assets/af42d37a-3f5e-4bd7-a628-9454b99cb8d4)

> [!NOTE] 
> As a best practice always assign roles to groups not individuals.

## Custom RBAC Role
  In this task, I have created a custom RBAC role and remove permissions that are not necessary. Custom roles are a core part of implementing the principle of least privilege for an environment. Built-in roles might have too many permissions for our scenario. 

  ![image](https://github.com/user-attachments/assets/254ff821-5ed3-43ca-97e1-487c1170e0b3)

  ![image](https://github.com/user-attachments/assets/6829a74e-86eb-466b-a641-3fd3ab1c3cc2)

> [!NOTE] 
> An Azure resource provider is a set of REST operations that enable functionality for a specific Azure service. I do not want the Help Desk to be able to have this capability, so it is being removed from the cloned role.

![image](https://github.com/user-attachments/assets/e69ef47e-3609-4d88-80e5-2da7ddfc2443)

## Activity Log
  The final task involved monitoring role assignments using Azure’s Activity Log. The Activity Log provides a detailed record of all changes made within the Azure environment, including role assignments. The activity log can be filtered for specific operations. It provides insight into subscription-level events. I have viewed the activity log to determine if anyone has created a new role.
 
  ![image](https://github.com/user-attachments/assets/10c11bfa-fbd0-4a2e-ae9f-e9e431fa3648)

## Azure RBAC roles Vs Microsoft Entra ID roles
  - **Azure RBAC roles** are focused on managing Azure resources, while **Microsoft Entra ID roles** are focused on managing identity and directory services.
  - **Azure RBAC roles** can be assigned at various scopes (subscription, resource group, resource), whereas **Microsoft Entra ID roles** are generally assigned at the tenant level

## Key Takeaways
  Here are the main takeaways.
  -	Management groups are used to logically organize subscriptions.
  -	The built-in root management group includes all the management groups and subscriptions.
  -	Azure has many built-in roles. You can assign these roles to control access to resources.
  -	You can create new roles or customize existing roles.
  -	Roles are defined in a JSON formatted file and include **`Actions`**, **`NotActions`**, and **`AssignableScopes`**.
  -	You can use the Activity Log to monitor role assignments.

 ![image](https://github.com/user-attachments/assets/18643531-392c-4531-b5e7-eb823c72249d)

