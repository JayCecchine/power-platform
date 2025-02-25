---
title: Automatic deletion of inactive Microsoft Dataverse for Teams environments 
description: Admins can configure an automatic cleanup process that removes inactive Dataverse for Teams environments from their tenants.
author: matapg007
ms.component: pa-admin
ms.topic: conceptual
ms.date: 09/30/2022
ms.subservice: admin
ms.author: matgupta 
ms.reviewer: jimholtz
search.audienceType: 
  - admin
search.app:
  - D365CE
  - PowerApps
  - Powerplatform
  - Flow
---

# Automatic deletion of inactive Microsoft Dataverse for Teams environments 

Power Platform provides a cleanup mechanism that automatically removes inactive [Dataverse for Teams environments](about-teams-environment.md) from your tenant. Dataverse for Teams environments that are considered inactive are first disabled. They're deleted after a period of time if no action is taken by the administrators.

The process is automatic. If you no longer need an inactive Dataverse for Teams environment, you don't need to do anything.

Administrators can [set the Teams environment deletion policy](#set-dataverse-for-teams-environment-deletion-policy) to configure how long an environment can be inactive before it's automatically disabled. The permissible range of values are: 15 days, 30 days, 45 days, 60 days, and 90 days of inactivity. The policy also determines how long an environment can be disabled before it's automatically deleted. 

Disabling a Dataverse for Teams environment prevents any meaningful use of the environment and its resources. Apps can't be launched, flows are suspended, chatbots can't be interacted with, and so on.

For information on automatic cleanup of production and sandbox environments, see [Automatic environment cleanup](automatic-environment-cleanup.md).

## Timeline for inactive Dataverse for Teams environments

The following table describes the schedule of notifications and actions for Dataverse for Teams environments that are considered inactive.

| State of Dataverse for Teams | Power Platform action |
| --- | --- |
| 83 days after no [user activity](#definition-of-user-activity) | Send a warning that the environment will be disabled. Update the environment state on the Environments list page<sup>1</sup> and the Environment page<sup>2</sup>. |
| 87 days after no user activity | Send a warning that the environment will be disabled. Update the inactive environment state on the Environments list page<sup>1</sup> and the Environment page<sup>2</sup>. |
| 90 days after no user activity | Disable the environment. Send a notice that the environment has been disabled. Update the disabled environment state on the Environments list page<sup>1</sup> and the Environment page<sup>3</sup>. |
| 113 days after no user activity | Send a warning that the environment will be deleted. Update the disabled environment state on the Environments list page<sup>1</sup> and the Environment page<sup>3</sup>. |
| 117 days after no user activity | Send a warning that the environment will be deleted. Update the disabled environment state on the Environments list page<sup>1</sup> and the Environment page<sup>3</sup>. |
| 120 days after no user activity | Delete the environment. Send a notice that the environment has been deleted. |

<sup>1</sup> **Environment state on the Environments list page in Power Platform admin center**
:::image type="content" source="media/inactive-environment-state.png" alt-text="Screenshot of the Environments list page in Power Platform admin center, with the environment state column highlighted.":::

<sup>2</sup>**Inactive environment alert on the Environment page in Power Platform admin center**
:::image type="content" source="media/inactive-environment-state-box.png" alt-text="Screenshot of the inactive environment alert on the Environment page, with the Trigger environment activity checkbox highlighted.":::

> [!NOTE]
> The **Environment inactive** warning tile only displays if the Dataverse for Teams environment is <= 7 days until disablement.

<sup>3</sup>**Disabled environment alert on the Environment page in Power Platform admin center**
:::image type="content" source="media/disabled-environment-state-box.png" alt-text="Screenshot of the disabled environment alert on the Environment page, with the Re-enable environment checkbox highlighted.":::

> [!NOTE]
> The **Environment disabled** tile displays anytime a Dataverse for Teams environment is disabled due to inactivity.

### Notification recipients

The following users will receive email notifications on the schedule described in the timeline:

- The environment's system administrators

  A Dataverse for Teams environment is paired with a team in Microsoft Teams. The owners of the team are automatically granted the System Administrator role for the environment. They receive email notifications and can [trigger activity, re-enable, and recover the environment](#trigger-activity-re-enable-and-recover-a-dataverse-for-teams-environment) in the Power Platform admin center. Team members and guests don't receive the email notifications.

- The user who created the environment 

Additionally, users and makers are notified on the Environments list page and Environment page when the Dataverse for Teams environment is disabled.

### Definition of user activity

Power Platform calculates a single measure of inactivity for each Dataverse for Teams environment. The measure accounts for all activity by users, makers, and admins across Power Apps, Power Automate, Power Virtual Agents, and Dataverse.

Most create, read, update, and delete operations on the environment and its resources that a user, maker, or admin initiates are considered activity. Most read operations aren't accounted for.

Here are some examples of the types of activities that are included in the measure:

- **User activity**: Launch an app, execute a flow (whether automatic or not), chat with a Power Virtual Agents bot

- **Maker activity**: Create, read, update, or delete an app, flow (desktop and cloud flows), Power Virtual Agents bot, custom connector

- **Admin activity**: Environment operations such as copy, delete, back up, recover, reset  

Activity includes automated behaviors such as scheduled flow runs. For example, if there's no user, maker, or admin activity in an environment, but it contains a cloud flow that runs daily, then the environment is considered active.

## Trigger activity, re-enable, and recover a Dataverse for Teams environment

By default, administrators have 30 days to re-enable an environment. If the environment remains disabled for 30 days, it's automatically deleted. Administrators have seven days to recover a deleted environment. See [Recover a deleted Dataverse for Teams environment](#recover-a-deleted-dataverse-for-teams-environment).

### Trigger activity for an inactive Dataverse for Teams environment 

1. Sign in to the [Power Platform admin center](https://admin.powerplatform.microsoft.com).

2. Select **Environments**, and then select the inactive Dataverse for Teams environment.

3. On the Environment page, select **Trigger environment activity**.

### Re-enable a disabled Dataverse for Teams environment

1. Sign in to the [Power Platform admin center](https://admin.powerplatform.microsoft.com).

2. Select **Environments**, and then select the disabled Dataverse for Teams environment.

3. On the Environment page, select **Re-enable environment**.

### Recover a deleted Dataverse for Teams environment

1. Sign in to the [Power Platform admin center](https://admin.powerplatform.microsoft.com).

2. Select **Environments**, and then select **Recover deleted environments**.

3. Select an environment to recover, and then select **Recover**.

For more information, see [recover environment](recover-environment.md).

## Set Dataverse for Teams environment deletion policy

Administrators can change the length of time Power Platform waits to disable inactive and delete disabled Dataverse for Teams environments.

> [!NOTE]
> This view is not yet available. We will be rolling out this policy in a future release.

1. Sign in to the [Power Platform admin center](https://admin.powerplatform.microsoft.com).

2. Select **Policies** > **Environment policies**.

3. In **Disable the environment after**, select the number of days Power Platform should wait to disable a Dataverse for Teams environment that becomes inactive.

4. In **Delete the disabled environment after**, select the number of days Power Platform should wait to delete a Dataverse for Teams environment that has been disabled.

   > [!NOTE]
   > Ninety days is the maximum number of days you can set for Power Platform to wait to disable a Dataverse for Teams environment due to inactivity. The permissible range of values are: 15 days, 30 days, 45 days, 60 days, and 90 days of inactivity.


5. Select **Save**.

   :::image type="content" source="media/inactive-environment-deletion-policy.png" alt-text="Screenshot of the Teams environment deletion policy settings in Power Platform admin center.":::



### See also
[Microsoft Dataverse for Teams environments](about-teams-environment.md)<br />
[Recover environment](recover-environment.md)  <br />
[Automatic environment cleanup](automatic-environment-cleanup.md)




[!INCLUDE[footer-include](../includes/footer-banner.md)]
