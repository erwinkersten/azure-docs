---
title: Authorize access to blobs using Active Directory
titleSuffix: Azure Storage
description: Authorize access to Azure blobs using Azure Active Directory (Azure AD). Assign Azure roles for access rights. Access data with an Azure AD account.
services: storage
author: jimmart-dev

ms.service: storage
ms.topic: conceptual
ms.date: 10/14/2021
ms.author: jammart
ms.subservice: common
---

# Authorize access to blobs using Azure Active Directory

Azure Storage supports using Azure Active Directory (Azure AD) to authorize requests to blob data. With Azure AD, you can use Azure role-based access control (Azure RBAC) to grant permissions to a security principal, which may be a user, group, or application service principal. The security principal is authenticated by Azure AD to return an OAuth 2.0 token. The token can then be used to authorize a request against the Blob service.

Authorizing requests against Azure Storage with Azure AD provides superior security and ease of use over Shared Key authorization. Microsoft recommends using Azure AD authorization with your blob applications when possible to assure access with minimum required privileges.

Authorization with Azure AD is available for all general-purpose and Blob storage accounts in all public regions and national clouds. Only storage accounts created with the Azure Resource Manager deployment model support Azure AD authorization.

Blob storage additionally supports creating shared access signatures (SAS) that are signed with Azure AD credentials. For more information, see [Grant limited access to data with shared access signatures](../common/storage-sas-overview.md).

## Overview of Azure AD for blobs

When a security principal (a user, group, or application) attempts to access a blob resource, the request must be authorized, unless it is a blob available for anonymous access. With Azure AD, access to a resource is a two-step process. First, the security principal's identity is authenticated and an OAuth 2.0 token is returned. Next, the token is passed as part of a request to the Blob service and used by the service to authorize access to the specified resource.

The authentication step requires that an application request an OAuth 2.0 access token at runtime. If an application is running from within an Azure entity such as an Azure VM, a virtual machine scale set, or an Azure Functions app, it can use a [managed identity](../../active-directory/managed-identities-azure-resources/overview.md) to access blob data. To learn how to authorize requests made by a managed identity to the Azure Blob service, see [Authorize access to blob data with managed identities for Azure resources](authorize-managed-identity.md).

The authorization step requires that one or more Azure RBAC roles be assigned to the security principal making the request. For more information, see [Assign Azure roles for access rights](#assign-azure-roles-for-access-rights).

Native applications and web applications that make requests to the Azure Blob service can also authorize access with Azure AD. To learn how to request an access token and use it to authorize requests for blob data, see [Authorize access to Azure Storage with Azure AD from an Azure Storage application](../common/storage-auth-aad-app.md).

Authorizing blob data operations with Azure AD is supported only for REST API versions 2017-11-09 and later. For more information, see [Versioning for the Azure Storage services](/rest/api/storageservices/versioning-for-the-azure-storage-services#specifying-service-versions-in-requests).

## Assign Azure roles for access rights

Azure Active Directory (Azure AD) authorizes access rights to secured resources through Azure RBAC. Azure Storage defines a set of  built-in RBAC roles that encompass common sets of permissions used to access blob data. You can also define custom roles for access to blob data. To learn more about assigning Azure roles for blob access, see [Assign an Azure role for access to blob data](../blobs/assign-azure-role-data-access.md).

An Azure AD security principal may be a user, a group, an application service principal, or a [managed identity for Azure resources](../../active-directory/managed-identities-azure-resources/overview.md). The RBAC roles that are assigned to a security principal determine the permissions that the principal will have. To learn more about assigning Azure roles for blob access, see [Assign an Azure role for access to blob data](../blobs/assign-azure-role-data-access.md)

In some cases you may need to enable fine-grained access to blob resources or to simplify permissions when you have a large number of role assignments for a storage resource. You can use Azure attribute-based access control (Azure ABAC) to configure conditions on role assignments. You can use conditions with a [custom role](../../role-based-access-control/custom-roles.md) or select built-in roles. For more information about configuring conditions for Azure storage resources with ABAC, see [Authorize access to blobs using Azure role assignment conditions (preview)](../blobs/storage-auth-abac.md). For details about supported conditions for blob data operations, see [Actions and attributes for Azure role assignment conditions in Azure Storage (preview)](../blobs/storage-auth-abac-attributes.md).

### Resource scope

Before you assign an Azure RBAC role to a security principal, determine the scope of access that the security principal should have. Best practices dictate that it's always best to grant only the narrowest possible scope. Azure RBAC roles defined at a broader scope are inherited by the resources beneath them.

You can scope access to Azure blob resources at the following levels, beginning with the narrowest scope:

- **An individual container.** At this scope, a role assignment applies to all of the blobs in the container, as well as container properties and metadata.
- **The storage account.** At this scope, a role assignment applies to all containers and their blobs.
- **The resource group.** At this scope, a role assignment applies to all of the containers in all of the storage accounts in the resource group.
- **The subscription.** At this scope, a role assignment applies to all of the containers in all of the storage accounts in all of the resource groups in the subscription.
- **A management group.** At this scope, a role assignment applies to all of the containers in all of the storage accounts in all of the resource groups in all of the subscriptions in the management group.

For more information about scope for Azure RBAC role assignments, see [Understand scope for Azure RBAC](../../role-based-access-control/scope-overview.md).

### Azure built-in roles for blobs

Azure RBAC provides a number of built-in roles for authorizing access to blob data using Azure AD and OAuth. Some examples of roles that provide permissions to data resources in Azure Storage include:

- [Storage Blob Data Owner](../../role-based-access-control/built-in-roles.md#storage-blob-data-owner): Use to set ownership and manage POSIX access control for Azure Data Lake Storage Gen2. For more information, see [Access control in Azure Data Lake Storage Gen2](../../storage/blobs/data-lake-storage-access-control.md).
- [Storage Blob Data Contributor](../../role-based-access-control/built-in-roles.md#storage-blob-data-contributor): Use to grant read/write/delete permissions to Blob storage resources.
- [Storage Blob Data Reader](../../role-based-access-control/built-in-roles.md#storage-blob-data-reader): Use to grant read-only permissions to Blob storage resources.
- [Storage Blob Delegator](../../role-based-access-control/built-in-roles.md#storage-blob-delegator): Get a user delegation key to use to create a shared access signature that is signed with Azure AD credentials for a container or blob.

To learn how to assign an Azure built-in role to a security principal, see [Assign an Azure role for access to blob data](../blobs/assign-azure-role-data-access.md). To learn how to list Azure RBAC roles and their permissions, see [List Azure role definitions](../../role-based-access-control/role-definitions-list.md).

For more information about how built-in roles are defined for Azure Storage, see [Understand role definitions](../../role-based-access-control/role-definitions.md#control-and-data-actions). For information about creating Azure custom roles, see [Azure custom roles](../../role-based-access-control/custom-roles.md).

Only roles explicitly defined for data access permit a security principal to access blob data. Built-in roles such as **Owner**, **Contributor**, and **Storage Account Contributor** permit a security principal to manage a storage account, but do not provide access to the blob data within that account via Azure AD. However, if a role includes **Microsoft.Storage/storageAccounts/listKeys/action**, then a user to whom that role is assigned can access data in the storage account via Shared Key authorization with the account access keys. For more information, see [Choose how to authorize access to blob data in the Azure portal](../../storage/blobs/authorize-data-operations-portal.md).

For detailed information about Azure built-in roles for Azure Storage for both the data services and the management service, see the **Storage** section in [Azure built-in roles for Azure RBAC](../../role-based-access-control/built-in-roles.md#storage). Additionally, for information about the different types of roles that provide permissions in Azure, see [Classic subscription administrator roles, Azure roles, and Azure AD roles](../../role-based-access-control/rbac-and-directory-admin-roles.md).

> [!IMPORTANT]
> Azure role assignments may take up to 30 minutes to propagate.

### Access permissions for data operations

For details on the permissions required to call specific Blob service operations, see [Permissions for calling data operations](/rest/api/storageservices/authorize-with-azure-active-directory#permissions-for-calling-data-operations).

## Access data with an Azure AD account

Access to blob data via the Azure portal, PowerShell, or Azure CLI can be authorized either by using the user's Azure AD account or by using the account access keys (Shared Key authorization).

### Data access from the Azure portal

The Azure portal can use either your Azure AD account or the account access keys to access blob data in an Azure storage account. Which authorization scheme the Azure portal uses depends on the Azure roles that are assigned to you.

When you attempt to access blob data, the Azure portal first checks whether you have been assigned an Azure role with **Microsoft.Storage/storageAccounts/listkeys/action**. If you have been assigned a role with this action, then the Azure portal uses the account key for accessing blob data via Shared Key authorization. If you have not been assigned a role with this action, then the Azure portal attempts to access data using your Azure AD account.

To access blob data from the Azure portal using your Azure AD account, you need permissions to access blob data, and you also need permissions to navigate through the storage account resources in the Azure portal. The built-in roles provided by Azure Storage grant access to blob resources, but they don't grant permissions to storage account resources. For this reason, access to the portal also requires the assignment of an Azure Resource Manager role such as the [Reader](../../role-based-access-control/built-in-roles.md#reader) role, scoped to the level of the storage account or higher. The **Reader** role grants the most restricted permissions, but another Azure Resource Manager role that grants access to storage account management resources is also acceptable. To learn more about how to assign permissions to users for data access in the Azure portal with an Azure AD account, see [Assign an Azure role for access to blob data](../blobs/assign-azure-role-data-access.md).

The Azure portal indicates which authorization scheme is in use when you navigate to a container. For more information about data access in the portal, see [Choose how to authorize access to blob data in the Azure portal](../blobs/authorize-data-operations-portal.md).

### Data access from PowerShell or Azure CLI

Azure CLI and PowerShell support signing in with Azure AD credentials. After you sign in, your session runs under those credentials. To learn more, see one of the following articles:

- [Choose how to authorize access to blob data with Azure CLI](authorize-data-operations-cli.md)
- [Run PowerShell commands with Azure AD credentials to access blob data](authorize-data-operations-powershell.md)

## Feature support

[!INCLUDE [Blob Storage feature support in Azure Storage accounts](../../../includes/azure-storage-feature-support.md)]

## Next steps

- [Authorize access to data in Azure Storage](../common/authorize-data-access.md)
- [Assign an Azure role for access to blob data](assign-azure-role-data-access.md)
