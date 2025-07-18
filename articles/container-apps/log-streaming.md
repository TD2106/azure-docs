---
title: View log streams in Azure Container Apps
description: View your container app's log stream.
services: container-apps
author: craigshoemaker
ms.service: azure-container-apps
ms.custom: devx-track-azurecli
ms.topic: how-to
ms.date: 06/25/2025
ms.author: cshoe
---

# View log streams in Azure Container Apps

While developing and troubleshooting your container app, it's essential to see the [logs](logging.md) for your container app in real time. Azure Container Apps lets you stream:

- [system logs](logging.md#system-logs) from the Container Apps environment and your container app.
- container [console logs](logging.md#container-console-logs) from your container app.

Log streams are accessible through the Azure portal or the Azure CLI.

## View log streams via the Azure portal

You can view system logs and console logs in the Azure portal. The container app's runtime generates system logs, and your container app generates console logs.

### Environment system log stream

To troubleshoot issues in your container app environment, you can view the system log stream from your environment page. The log stream displays the system logs for the Container Apps service and the apps actively running in the environment:

1. Go to your environment in the Azure portal.
1. Select **Log stream** under the *Monitoring* section on the sidebar menu.

### Container app log stream

You can view a log stream of your container app's system or console logs from your container app page.

1. Go to your container app in the Azure portal.
1. Select **Log stream** under the *Monitoring* section on the sidebar menu.
1. To view the console log stream, select **Console**.

    1. If you have multiple revisions, replicas, or containers, you can select from the drop-down menus to choose a container. If your app has only one container, you can skip this step.

1. To view the system log stream, select **System**. The system log stream displays the system logs for all running containers in your container app.

## View log streams via the Azure CLI

You can view your container app's log streams from the Azure CLI with the `az containerapp logs show` command or your container app's environment system log stream with the `az containerapp env logs show` command.

Control the log stream with the following arguments:

- `--tail` (Default) View the last n log messages. Values are 0-300 messages. The default is 20.
- `--follow` View a continuous live stream of the log messages.

### Stream Container app logs

You can stream the system or console logs for your container app. To stream the container app system logs, use the `--type` argument with the value `system`. To stream the container console logs, use the `--type` argument with the value `console`. The default is `console`.

#### View container app system log stream

This example uses the `--tail` argument to display the last 50 system log messages from the container app. Replace the `<PLACEHOLDERS>` with your container app's values.

# [Bash](#tab/bash)

```azurecli
az containerapp logs show \
  --name <CONTAINER_APP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --type system \
  --tail 50
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp logs show `
  --name <CONTAINER_APP_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --type system `
  --tail 50
```

---

This example displays a continuous live stream of system log messages from the container app using the `--follow` argument. Replace the `<PLACEHOLDERS>` with your container app's values.

# [Bash](#tab/bash)

```azurecli
az containerapp logs show \
  --name <CONTAINER_APP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --type system \
  --follow
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp logs show `
  --name <CONTAINER_APP_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --type system `
  --follow
```

---

Use `Ctrl-C` or `Cmd-C` to stop the live stream.

### View container console log stream

To connect to a container's console log stream in a container app with multiple revisions, replicas, and containers, include the following parameters in the `az containerapp logs show` command.

| Argument | Description |
|----------|-------------|
| `--revision` | The revision name. |
| `--replica` | The replica name in the revision. |
| `--container` | The container name to connect to. |

You can get the revision names with the `az containerapp revision list` command. Replace the `<PLACEHOLDERS>` with your container app's values.

# [Bash](#tab/bash)

```azurecli
az containerapp revision list \
  --name <CONTAINER_APP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --query "[].name"
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp revision list `
  --name <CONTAINER_APP_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --query "[].name"
```

---

Use the `az containerapp replica list` command to get the replica and container names. Replace the `<PLACEHOLDERS>` with your container app's values.

# [Bash](#tab/bash)

```azurecli
az containerapp replica list \
  --name <CONTAINER_APP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --revision <REVISION_NAME> \
  --query "[].{Containers:properties.containers[].name, Name:name}"
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp replica list `
  --name <CONTAINER_APP_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --revision <REVISION_NAME> `
  --query "[].{Containers:properties.containers[].name, Name:name}"
```

---

Live stream the container console using the `az container app show` command with the `--follow` argument. Replace the `<PLACEHOLDERS>` with your container app's values.

# [Bash](#tab/bash)

```azurecli
az containerapp logs show \
  --name <CONTAINER_APP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --revision <REVISION_NAME> \
  --replica <REPLICA_NAME> \
  --container <CONTAINER_NAME> \
  --type console \
  --follow
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp logs show  `
  --name <CONTAINER_APP_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --revision <REVISION_NAME> `
  --replica <REPLICA_NAME> `
  --container <CONTAINER_NAME> `
  --type console `
  --follow
```

---

Use `Ctrl-C` or `Cmd-C` to stop the live stream.

View the last 50 console log messages using the `az containerapp logs show` command with the `--tail` argument. Replace the `<PLACEHOLDERS>` with your container app's values.

# [Bash](#tab/bash)

```azurecli
az containerapp logs show \
  --name <CONTAINER_APP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --revision <REVISION_NAME> \
  --replica <REPLICA_NAME> \
  --container <CONTAINER_NAME> \
  --type console \
  --tail 50
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp logs show  `
  --name <CONTAINER_APP_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --revision <REVISION_NAME> `
  --replica <REPLICA_NAME> `
  --container <CONTAINER_NAME> `
  --type console `
  --tail 50
```

---

### View environment system log stream

Use the following command with the `--follow` argument to view the live system log stream from the Container Apps environment. Replace the `<PLACEHOLDERS>` with your environment values.

# [Bash](#tab/bash)

```azurecli
az containerapp env logs show \
  --name <ENVIRONMENT_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --follow
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp env logs show  `
  --name <ENVIRONMENT_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --follow
```

---

Use `Ctrl-C` or `Cmd-C` to stop the live stream.

This example uses the `--tail` argument to display the last 50 environment system log messages. Replace the `<PLACEHOLDERS>` with your environment values.

# [Bash](#tab/bash)

```azurecli
az containerapp env logs show \
  --name <CONTAINER_APP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --tail 50
```

# [PowerShell](#tab/powershell)

```powershell
az containerapp env logs show `
  --name <CONTAINER_APP_NAME> `
  --resource-group <RESOURCE_GROUP> `
  --tail 50
```

---

> [!div class="nextstepaction"]
> [Log storage and monitoring options in Azure Container Apps](log-monitoring.md)
