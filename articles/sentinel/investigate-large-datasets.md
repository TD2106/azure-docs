---
title: Start an investigation by searching large datasets - Microsoft Sentinel
description: Learn about search jobs and restoring data from long-term retention in Microsoft Sentinel.
author: cwatson-cat
ms.topic: conceptual
ms.date: 03/03/2024
ms.author: cwatson
appliesto:
    - Microsoft Sentinel in the Microsoft Defender portal
    - Microsoft Sentinel in the Azure portal
ms.collection: usx-security


#Customer intent: As a security analyst, I want to search and restore log data from long-term retention so that I can conduct thorough investigations on historical events.

---

# Start an investigation by searching for events in large datasets

One of the primary activities of a security team is to search logs for specific events. For example, you might search logs for the activities of a specific user within a given time-frame.

In Microsoft Sentinel, you can search across long time periods in extremely large datasets by using a search job.  While you can run a search job on any type of log, search jobs are ideally suited to search logs in a long-term retention (formerly known as archive) state. If you need to do a full investigation on such data, you can restore that data into an interactive retention state&mdash;like your regular Log Analytics tables&mdash; to run high performing queries and deeper analysis.

[!INCLUDE [unified-soc-preview](includes/unified-soc-preview.md)]

## Search large datasets

Use a search job when you start an investigation to find specific events in logs within a given time frame. You can search all your logs to find events that match your criteria and filter through the results.

Search in Microsoft Sentinel is built on top of search jobs. Search jobs are asynchronous queries that fetch records. The results are returned to a search table that's created in your Log Analytics workspace after you start the search job. The search job uses parallel processing to run the search across long time spans, in extremely large datasets. So search jobs don't impact the workspace's performance or availability.

Search results are stored in a table named with a `_SRCH` suffix.

The following image shows example search criteria for a search job.

:::image type="content" source="media/investigate-large-datasets/search-job-criteria.png" alt-text="Screenshot of search page with search criteria of administrator, time range last 1 year, and a table selected.":::

### Supported log types

Use search to find events in any of the following log types:

- [Analytics logs](/azure/azure-monitor/logs/data-platform-logs)
- [Basic logs](/azure/azure-monitor/logs/data-platform-logs)
- [Auxiliary logs](/azure/azure-monitor/logs/data-platform-logs)

You can also search analytics or basic log data stored in [long-term retention](/azure/azure-monitor/logs/data-retention-configure#interactive-long-term-and-total-retention).

### Limitations of a search job

See [Search job limitations](/azure/azure-monitor/logs/search-jobs#limitations) in the Azure Monitor documentation.

## Restore log data from long-term retention

When you need to do a full investigation on log data in long-term retention, restore a table from the **Search** page in Microsoft Sentinel. Specify a target table and time range for the data you want to restore. Within a few minutes, the log data is restored and available within the Log Analytics workspace. Then you can use the data in high-performance queries that support full KQL.

A restored log table is available in a new table that has a *_RST suffix. The restored data is available as long as the underlying source data is available. But you can delete restored tables at any time without deleting the underlying source data. To save costs, we recommend you delete the restored table when you no longer need it.

The following image shows the restore option on a saved search.

:::image type="content" source="media/investigate-large-datasets/search-results-restore.png" alt-text="Screenshot of the restore link on a saved search.":::

### Limitations of log restore

See [Restore limitations](/azure/azure-monitor/logs/restore#limitations) in the Azure Monitor documentation.

## Bookmark search results or restored data rows

Similar to the [threat hunting dashboard](hunting.md#use-the-hunting-dashboard), bookmark rows that contain information you find interesting so you can attach them to an incident or refer to them later. For more information, see [Create bookmarks](hunting.md#create-bookmarks).

## Next steps

- [Search across long time spans in large datasets](search-jobs.md)
- [Restore logs from long-term retention](restore.md)
