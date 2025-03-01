---
title: Debug your apps remotely in Azure Spring Apps
description: Learn how to debug your apps remotely in Azure Spring Apps.
ms.service: spring-apps
ms.topic: how-to
author: KarlErickson
ms.author: jialuogan
ms.date: 12/01/2022
ms.custom: devx-track-java, event-tier1-build-2022
---

# Debug your apps remotely in Azure Spring Apps

This feature describes how to enable remote debugging of your applications in Azure Spring Apps.

## Prerequisites

- [Azure CLI](/cli/azure/install-azure-cli) with the Azure Spring Apps extension. Use the following command to remove previous versions and install the latest extension. If you previously installed the spring-cloud extension, uninstall it to avoid configuration and version mismatches.

  ```azurecli
  az extension remove --name spring
  az extension add --name spring
  az extension remove --name spring-cloud
  ```

- A deployed application in Azure Spring Apps.

## Enable or disable remote debugging

For security reasons, Azure Spring Apps disables remote debugging by default. Based on your company policy, you can enable remote debugging for your app yourself or see an admin to enable it for you. You can enable or disable remote debugging using Azure CLI, Azure portal, or the VS Code extension.

### [Azure portal](#tab/portal)

Use the following steps to enable remote debugging for your application using the Azure portal:

1. Navigate to your application page.
1. Under **Settings** in the left navigation pane, select **Remote debugging**.
1. On the **Remote debugging** page, enable remote debugging and specify the debugging port.

   :::image type="content" source="media/how-to-remote-debugging-app-instance/portal-enable-remote-debugging.png" alt-text="Screenshot of the Remote debugging page showing the Remote debugging option selected." lightbox="media/how-to-remote-debugging-app-instance/portal-enable-remote-debugging.png":::

### [Azure CLI](#tab/cli)

Use the following command to enable remote debugging for your application using the Azure CLI:

```azurecli
az spring app enable-remote-debugging \
    --name <application-name> \
    --deployment <deployment-name> \
    --resource-group <resource-group-name> \
    --service <service-name> \
    --port <port>
```

Use the following command to disable remote debugging for your application:

```azurecli
az spring app disable-remote-debugging \
    --name <application-name> \
    --deployment <deployment-name> \
    --resource-group <resource-group-name> \
    --service <service-name> \
```

Use the following command to display the remote debugging configuration:

```azurecli
az spring app get-remote-debugging-config \
    --name <application-name> \
    --deployment <deployment-name> \
    --resource-group <resource-group-name> \
    --service <service-name> \
```

---

## Debug an app instance remotely

You can debug an app instance remotely using the Azure Toolkit for IntelliJ or the Azure Spring Apps for VS Code extension.

### [Azure Toolkit for IntelliJ](#tab/Intellij-extension)

This section describes how to debug an app instance remotely using the Azure Toolkit for IntelliJ.

### Prerequisites

- [Azure Toolkit for IntelliJ](/azure/developer/java/toolkit-for-intellij/install-toolkit).
- [IntelliJ IDEA](https://www.jetbrains.com/idea/download), Ultimate or Community edition.

### Enable or disable remote debugging

Use the following steps to enable or disable remote debugging:

1. Sign in to your Azure account in Azure Explorer.
1. Select an app instance, and then select **Enable Remote Debugging**.

   :::image type="content" source="media/how-to-remote-debugging-app-instance/intellij-enable-remote.png" alt-text="Screenshot showing the Enable Remote Debugging option." lightbox="media/how-to-remote-debugging-app-instance/intellij-enable-remote.png":::

### Attach debugger

Use the following steps to attach debugger.

1. Use the following Azure CLI command to obtain the **Azure Spring Apps Remote Debugging Role** role, which includes the `Microsoft.AppPlatform/Spring/apps/deployments/remotedebugging/action` data action permission.

   ```azurecli
   az role assignment create \
       --role "Azure Spring Apps Remote Debugging Role" \
       --scope "<service-instance-resource-id>" \
       --assignee "<your-identity>"
   ```

1. Select an app instance, and then select **Attach Debugger**. IntelliJ connects to the app instance and starts remote debugging.

   :::image type="content" source="media/how-to-remote-debugging-app-instance/intellij-remote-debugging-instance.png" alt-text="Screenshot showing the Attach Debugger option." lightbox="media/how-to-remote-debugging-app-instance/intellij-remote-debugging-instance.png":::

1. Azure Toolkit for IntelliJ creates the remote debugging configuration. You can find it under **Remote Jvm Debug"** Configure the module class path to the source code that you use for remote debugging.

   :::image type="content" source="media/how-to-remote-debugging-app-instance/intellij-remote-debugging-configuration.png" alt-text="Screenshot of the Run/Debug Configurations page." lightbox="media/how-to-remote-debugging-app-instance/intellij-remote-debugging-configuration.png":::

### Troubleshooting

This section provides troubleshooting information.

- Take the following actions if you fail to attach debugger and receive an error similar to `java.net.SocketException, connection reset` or `Failed to attach to remote debugger, ClosedConnectionException`:

  - Check the RBAC role to make sure that you're authorized to remotely debug an app instance.
  - Make sure that you're connecting to a valid instance. Refresh the deployment to get the latest instances.

    :::image type="content" source="media/how-to-remote-debugging-app-instance/refresh-instance.png" alt-text="Screenshot showing the Refresh command." lightbox="media/how-to-remote-debugging-app-instance/refresh-instance.png":::

- Take the following actions if you successfully attach debugger but can't remotely debug the app instance:

  - Make sure that your IDE contains the source code you want to debug.
  - Make sure that the debug configuration has the correct module class path.

### [VS Code extension](#tab/Vscode-extension)

This section describes how to debug an app instance remotely using the VS Code extension.

### Prerequisites

- [Azure Spring Apps for VS Code Plugin](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-azurespringcloud).
- [Visual Studio Code](https://code.visualstudio.com).

### Enable or disable remote debugging

Use the following steps to enable or disable remote debugging:

1. Sign in to your Azure subscription.
1. Select an app instance, and then select **Enable Remote Debugging**.

   :::image type="content" source="media/how-to-remote-debugging-app-instance/visual-studio-code-enable-remote-debugging.png" alt-text="Screenshot showing the Enable Remote Debugging option." lightbox="media/how-to-remote-debugging-app-instance/visual-studio-code-enable-remote-debugging.png":::

### Attach debugger

Use the following steps to attach debugger.

1. Use the following Azure CLI command to obtain the **Azure Spring Apps Remote Debugging Role** role, which includes the `Microsoft.AppPlatform/Spring/apps/deployments/remotedebugging/action` data action permission.

   ```azurecli
   az role assignment create \
       --role "Azure Spring Apps Remote Debugging Role" \
       --scope "<service-instance-resource-id>" \
       --assignee "<your-identity>"
   ```

1. Select an app instance, and then select **Attach Debugger**. VS Code connects to the app instance and starts remote debugging.

   :::image type="content" source="media/how-to-remote-debugging-app-instance/visual-studio-code-remote-debugging-instance.png" alt-text="Screenshot showing the Attach Debugger option." lightbox="media/how-to-remote-debugging-app-instance/visual-studio-code-remote-debugging-instance.png":::

### Troubleshooting

This section provides troubleshooting information.

- Take the following actions if you fail to attach debugger and receive an error similar to `java.net.SocketException, connection reset` or `Failed to attach to remote debugger, ClosedConnectionException`:

  - Check the RBAC role to make sure that you're authorized to remotely debug an app instance.
  - Make sure that you're connecting to a valid instance. Refresh the deployment to get the latest instances.

    :::image type="content" source="media/how-to-remote-debugging-app-instance/refresh-instance.png" alt-text="Screenshot showing the Refresh command." lightbox="media/how-to-remote-debugging-app-instance/refresh-instance.png":::

- Take the following action if you successfully attach debugger but can't remotely debug the app instance:

  - Make sure that your IDE contains the source code you want to debug.

---

## Limitations

Remote debugging is only supported for Java applications.

| Tier                    | Deployment type   | Supported |
|-------------------------|-------------------|-----------|
| Standard and basic tier | Jar               | Yes       |
| Standard and basic tier | Source code(Java) | Yes       |
| Standard and basic tier | Custom Image      | No        |
| Enterprise tier         | Java Application  | Yes       |
| Enterprise tier         | Source code(Java) | Yes       |
| Enterprise tier         | Custom Image      | No        |

## Tips

- Java remote debugging is dangerous because it allows remote code execution. Azure Spring Apps helps you secure the communication between your client IDE and the remote application. However, you should disable remote debugging and remove the RBAC role after you're finished.
- You should scale in the app instance to one to ensure that traffic can go to the instance.

## Next steps

- [Azure Spring Apps](index.yml)
