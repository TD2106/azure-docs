---
title: Backup Classic Alerts using Azure Backup
description: Learn how to back up Classic Alerts in the Azure Recovery Services vault.
ms.topic: how-to
ms.date: 03/17/2025
ms.service: azure-backup
author: jyothisuri
ms.author: jsuri
ms.custom: engagement-fy24
# Customer intent: As a cloud administrator, I want to back up classic alerts in the Azure Recovery Services vault, so that I can maintain alerting functionality while transitioning to Azure Monitor for improved alert management and monitoring capabilities.
---

# Backup Classic Alerts

This article describes how to back up Classic Alerts in the Azure Recovery Services vault.

>[!Important]
>Azure Backup now provides new and improved alerting capabilities via Azure Monitor. If you're using the older [classic alerts solution](#backup-alerts-in-recovery-services-vault) for Recovery Services vaults, we recommend you [move to Azure Monitor alerts](backup-azure-monitoring-alerts.md#migrate-from-classic-alerts-to-built-in-azure-monitor-alerts).

## Backup alerts in Recovery Services vault

> [!IMPORTANT]
> This section describes an older alerting solution (referred to as classic alerts). We recommend you to switch to using Azure Monitor based alerts as it offers multiple benefits. Learn [how to migrate to  Azure Monitor Based alerts](backup-azure-monitoring-alerts.md?tabs=recovery-services-vaults#migrate-from-classic-alerts-to-built-in-azure-monitor-alerts).

Alerts are primarily the scenarios where you're notified to take relevant action. The **Backup Alerts** section shows alerts that the Azure Backup service generates. These alerts are defined by the service and you can't custom create any alerts.

### Alert scenarios

The following scenarios are defined by service as alert-able scenarios:

- Backup/Restore failures
- Backup succeeded with warnings for Microsoft Azure Recovery Services (MARS) agent
- Stop protection with delete data
- Soft-delete functionality disabled for vault
- [Unsupported backup type for database workloads](./backup-sql-server-azure-troubleshoot.md#backup-type-unsupported)
- Workload extension health issues for database backup

### Alerts from the various Azure Backup solutions

The following are alerts from Azure Backup solutions are:

- Azure VM backups
- Azure File backups
- Azure workload backups such as SQL, SAP HANA
- Microsoft Azure Recovery Services (MARS) agent

> [!NOTE]
>- Alerts from System Center Data Protection Manager (SC-DPM), Microsoft Azure Backup Server (MABS) aren't displayed here.
>- Stop protection with delete data alerts are currently not sent for Azure Files backup.
>- Stop protection with delete data alert is only generated if sot-delete functionality is enabled for the vault, that is, if soft-delete feature is disabled for a vault, then a single alert is sent to notify you that soft-delete has been disabled. Subsequent deletion of the backup data of any item doesn't raise an alert.

### Consolidated alerts

For Azure workload backup solutions, such as SQL and SAP HANA, log backups can be generated frequently (up to every 15 minutes according to the policy). So, you might encounter frequent log backup failures (up to every 15 minutes). In this scenario, the end user will be overwhelmed if an alert is raised for each failure occurrence.

So, an alert is sent for the first occurrence, and if the later failures are because of the same root cause, then further alerts aren't generated. The first alert is updated with the failure count. But if you've deactivated the alert, the next occurrence will trigger another alert and this will be treated as the first alert for that occurrence. This is how Azure Backup performs alert consolidation for SQL and SAP HANA backups.

On-demand backup jobs aren't consolidated.

### Exceptions when an alert isn't raised

There are a few exceptions when an alert isn't raised on a failure. They are:

- You've explicitly canceled the running job.
- The job fails because another backup job is in progress (no actions to be taken as we've to wait for the previous job to finish).
- The VM backup job fails because the backed-up Azure VM no longer exists.
- [Consolidated Alerts](#consolidated-alerts)

The exceptions above are designed from the understanding that the result of these operations (primarily user triggered) shows up immediately on portal/PowerShell/the CLI clients. So, you're immediately aware and doesn't need a notification.

### Alert types

Based on alert severity, you can define three types of alerts:

- **Critical**: In principle, any backup or recovery failure (scheduled or user triggered) would lead to generation of an alert and would be shown as a *Critical* alert. The alert is also generated for destructive operations, such as delete backup.
- **Warning**: If the backup operation succeeds, but with few warnings, they're listed as *Warning* alerts. Warning alerts are currently available only for Azure Backup Agent backups.
- **Informational**: Currently, no informational alerts are generated by the Azure Backup service.

## Notification for backup alerts

> [!NOTE]
> Configuration of notification can be done only through the Azure portal. PS/CLI/REST API/Azure Resource Manager Template client is currently not supported.

Once an alert is raised, you're notified. Azure Backup provides a built-in notification mechanism via email. You can specify individual email addresses or distribution lists to be notified when an alert is generated. You can also choose if you need to receive notified for each individual alert or to group them in an hourly digest and then get notified.

:::image type="content" source="./media/backup-azure-monitoring-laworkspace/recovery-services-vault-built-in-notification-inline.png" alt-text="Screenshot of the Recovery Services vault built-in email notification." lightbox="./media/backup-azure-monitoring-laworkspace/recovery-services-vault-built-in-notification-expanded.png":::

When notification is configured, you'll receive a welcome or introductory email. This confirms that Azure Backup can send emails to these addresses when an alert is raised.

If the frequency was set to an hourly digest, and an alert was raised and resolved within an hour, it won't be a part of the upcoming hourly digest.

> [!NOTE]
>- If a destructive operation, such as **stop protection with delete data** is performed, an alert is raised and an email is sent to subscription owners, admins, and co-admins even if notifications aren't configured for the Recovery Services vault.
>- To configure notification for successful jobs, use [Log Analytics](backup-azure-monitoring-use-azuremonitor.md#using-log-analytics-workspace).

## Inactivating alerts

To deactivate/resolve an active alert, you can select the list item corresponding to the alert you wish to deactivate. This opens up a screen that shows detailed information about the alert, with an **Inactivate** button at the top. Selecting this button will change the status of the alert to **Inactive**. You may also deactivate an alert by right-clicking the list item corresponding to that alert and selecting **Inactivate**.

:::image type="content" source="./media/backup-azure-monitoring-laworkspace/vault-alert-inactivate.png" alt-text="Screenshot showing how to deactivate alerts via Backup center.":::



## Next steps
Learn more about [Azure Backup monitoring and reporting](monitoring-and-alerts-overview.md).