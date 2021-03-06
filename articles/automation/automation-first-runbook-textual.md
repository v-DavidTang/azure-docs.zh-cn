---
title: "我在 Azure 自动化中的第一个 PowerShell 工作流 Runbook | Microsoft Docs"
description: "本教程指导你使用 PowerShell 工作流创建、测试和发布一个简单的文本 Runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "powershell 工作流, powershell 工作流示例, 工作流 powershell"
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2016
ms.author: magoedte;bwren
translationtype: Human Translation
ms.sourcegitcommit: 00b217a4cddac0a893564db27ffb4f460973c246
ms.openlocfilehash: a244443b14b139544c224d9c57fc6e78b8432584


---
# <a name="my-first-powershell-workflow-runbook"></a>我的第一个 PowerShell 工作流 Runbook
> [AZURE.SELECTOR] - [图形](automation-first-runbook-graphical.md) - [PowerShell](automation-first-runbook-textual-powershell.md) - [PowerShell 工作流](automation-first-runbook-textual.md)
>
>

本教程指导用户在 Azure 自动化中创建 [PowerShell 工作流 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。 我们将从一个简单的 Runbook 开始，我们将测试和发布该 Runbook，同时介绍如何跟踪 Runbook 作业的状态。 然后我们将通过修改 Runbook 来实际管理 Azure 资源，这种情况下将启动 Azure 虚拟机。 然后我们将通过添加 Runbook 参数来使该 Runbook 更稳健。

## <a name="prerequisites"></a>先决条件
为了完成本教程，你需要满足以下条件。

* Azure 订阅。 如果你还没有帐户，则可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或<a href="/pricing/free-account/" target="_blank">[注册免费帐户](https://azure.microsoft.com/free/)。
* [自动化帐户](automation-security-overview.md) ，用来保存 Runbook 以及向 Azure 资源进行身份验证。  此帐户必须有权启动和停止虚拟机。
* Azure 虚拟机。 我们将停止并启动该计算机，因此其不应为生产用计算机。

## <a name="step-1-create-new-runbook"></a>步骤 1 - 创建新的 Runbook
我们首先创建一个输出文本 *Hello World*的简单 Runbook 。

1. 在 Azure 门户中，打开你的自动化帐户。  
   通过自动化帐户页面可快速查看此帐户中的资源。 你应该已拥有某些资产。 大多数资产都是自动包括在新的自动化帐户中的模块。 你还应具有在“先决条件”中提到的凭证资产 [](#prerequisites)。
2. 单击“Runbook”  磁贴打开 Runbook 的列表。<br> ![Runbook 控制](media/automation-first-runbook-textual/runbooks-control.png)
3. 通过单击“添加 Runbook”按钮，然后单击“创建新 Runbook”，创建一个新 Runbook。
4. 将该 Runbook 命名为 *MyFirstRunbook-Workflow*。
5. 在本例中，我们将要创建一个 [PowerShell 工作流 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)，因此请选择“Powershell 工作流”作为“Runbook 类型”。<br> ![新建 Runbook](media/automation-first-runbook-textual/new-runbook.png)
6. 单击“创建”以创建 Runbook 并打开文本编辑器  。

## <a name="step-2-add-code-to-the-runbook"></a>步骤 2 - 将代码添加到 Runbook
你可以直接将代码键入 Runbook 中，或者通过“库”控件选择 cmdlet、Runbook 和资产，并使用任何相关的参数将它们添加到 Runbook。 在本演练中，我们将直接键入 Runbook。

1. 我们的 Runbook 目前为空，只有必需的 *workflow* 关键字、Runbook 名称以及括住整个工作流的大括号。

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. 在大括号之间键入 *Write-Output "Hello World"* 。

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. 通过单击“保存” 保存 Runbook。<br> ![保存 Runbook](media/automation-first-runbook-textual/runbook-edit-toolbar-save.png)

## <a name="step-3-test-the-runbook"></a>步骤 3 - 测试 Runbook
在我们发布 Runbook 使其可在生产中使用之前，我们要对其进行测试以确保其能正常工作。 测试 Runbook 时，你可以运行其“草稿”版本并以交互方式查看其输出  。

1. 单击“测试窗格”  打开测试窗格。<br> ![](media/automation-first-runbook-textual/runbook-edit-toolbar-test-pane.png)
2. 单击“启动”以启动测试  。 这应该是唯一的已启用选项。
3. 将创建一个 [Runbook 作业](automation-runbook-execution.md) 并显示其状态。  
   作业状态初始为“排队”，该值指示它正在等待云中的 Runbook 辅助角色可用  。 在某个辅助角色认领该作业后，该作业状态将变为“正在启动”，然后当 Runbook 实际开始运行时，该作业状态将变为“正在运行”。  
4. Runbook 作业完成后，会显示其输出。 在本例中，我们应该看到 *Hello World*。<br> ![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)
5. 关闭测试窗格以返回到画布。

## <a name="step-4-publish-and-start-the-runbook"></a>步骤 4 - 发布和启动 Runbook
我们刚刚创建的 Runbook 仍处于草稿模式。 我们需要发布该 Runbook，然后才可将其用于生产。 当发布 Runbook 时，你可以用草稿版本覆盖现有的已发布版本。 在本例中，我们还没有已发布版本，因为我们刚刚创建 Runbook。

1. 单击“发布”以发布该 Runbook，然后在出现提示时单击“是”。<br> ![](media/automation-first-runbook-textual/runbook-edit-toolbar-publish.png)
2. 如果现在向左滚动以在“Runbooks”窗格中查看该 Runbook，它将显示“已发布”的“创作状态”。
3. 向右滚动查看 **MyFirstRunbook-Workflow**的窗格。  
   顶部的选项允许我们启动 Runbook，计划其在将来的某个时刻启动，或创建 [webhook](automation-webhooks.md) 以使其可以通过 HTTP 调用启动。
4. 我们只想要启动 Runbook，因此单击“启动”，然后在出现提示时单击“是”。<br> ![启动 Runbook](media/automation-first-runbook-textual/runbook-toolbar-start.png)
5. 会为我们刚刚创建的 Runbook 作业打开作业窗格。 我们可以关闭此窗格，但在这种情况下我们将其保持打开，以便可以查看该作业的进度。
6. 作业状态显示在“作业摘要”  中并且与我们在测试该 Runbook 时看到的状态相匹配。<br> ![作业摘要](media/automation-first-runbook-textual/job-pane-summary.png)
7. 一旦此 Runbook 状态显示“已完成”，单击“输出”。  *Hello World*。<br> ![作业摘要](media/automation-first-runbook-textual/job-pane-output.png)  
8. 关闭“输出”窗格。
9. 单击“流”打开 Runbook 作业的“流”窗格。 应该只会在输出流中看到 *Hello World*，但此窗格也可以显示 Runbook 作业的其他流，例如，“详细”和“错误”（如果 Runbook 向其写入)。<br> ![作业摘要](media/automation-first-runbook-textual/job-pane-streams.png)
10. 关闭“流”窗格和“作业”窗格中以返回到 MyFirstRunbook 窗格。
11. 单击“作业”打开此 Runbook 的“作业”窗格  。 这将列出此 Runbook 创建的所有作业。 由于我们只运行该作业一次，应该只会看到一个列出的作业。<br> ![作业](media/automation-first-runbook-textual/runbook-control-jobs.png)
12. 你可以在此作业上单击以打开我们启动 Runbook 时查看的相同的作业窗格。 这样你就可以回溯并查看为特定 Runbook 创建的任何作业的详细信息。

## <a name="step-5-add-authentication-to-manage-azure-resources"></a>步骤 5 - 添加身份验证来管理 Azure 资源
我们已经测试并发布 Runbook，但到目前为止它不执行任何有用的操作。 我们想要让其管理 Azure 资源。 然而，除非使用“先决条件”中引用的凭据对其进行身份验证，否则它将无法进行管理 [](#prerequisites)。 我们使用 **Add-AzureRMAccount** cmdlet 实现此目的。

1. 通过单击 MyFirstRunbook-Workflow 窗格上的“编辑”打开文本编辑器。<br> ![编辑 Runbook](media/automation-first-runbook-textual/runbook-toolbar-edit.png)
2. 我们不再需要 **Write-Output** 行，因此请直接删除它。
3. 将光标放在大括号之间的空白行上。
4. 键入或复制并粘贴以下代码，此代码会使用自动化运行方式帐户处理身份验证：

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. 单击“测试”窗格，以便我们可以测试 Runbook  。
6. 单击“启动”以启动测试  。 测试完成后，应收到类似以下显示你帐户中基本信息的输出。 这可确认凭据有效。<br> ![身份验证](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6-add-code-to-start-a-virtual-machine"></a>步骤 6 – 添加用于启动虚拟机的代码
现在我们的 Runbook 要对 Azure 订阅进行身份验证，我们可以管理资源。 我们将添加一个命令用于启动虚拟机。 可以在你的 Azure 订阅中选取任何虚拟机，现在将该名称硬编码到该 cmdlet。

1. 在 *Add-AzureRmAccount* 后面键入 *Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'NameofResourceGroup'*（提供要启动的虚拟机的名称和资源组名称）。  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. 保存 Runbook，然后单击“测试”窗格，以便我们可以测试 Runbook  。
3. 单击“启动”以启动测试  。 一旦测试完成后，检查已启动的虚拟机。

## <a name="step-7-add-an-input-parameter-to-the-runbook"></a>步骤 7 - 将输入参数添加到 Runbook
我们的 Runbook 目前会启动我们在 Runbook 中硬编码的虚拟机，但如果可以在启动 Runbook 时指定虚拟机，它会更有用。 我们现在将输入参数添加到 Runbook，以提供该功能。

1. 将 *VMName* 和 *ResourceGroupName* 的参数添加到 Runbook，并将这些变量与 **Start-AzureRmVM** cmdlet 配合使用，如以下示例所示。

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. 保存 Runbook 并打开“测试”窗格。 请注意，现在可以为将在测试中使用的两个输入变量提供值。
3. 关闭“测试”窗格。
4. 单击“发布”以发布 Runbook 的新版本  。
5. 停止在上一步中启动的虚拟机。
6. 单击“启动”以启动 Runbook **ResourceGroupName** 。 键入要启动的虚拟机的 **VMName** 和 **ResourceGroupName**。<br> ![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)
7. 一旦 Runbook 完成后，检查已启动的虚拟机。

## <a name="next-steps"></a>后续步骤
* 若要开始使用图形 Runbook，请参阅 [我的第一个图形 Runbook](automation-first-runbook-graphical.md)
* 若要开始使用 PowerShell Runbook，请参阅 [我的第一个 PowerShell Runbook](automation-first-runbook-textual-powershell.md)
* 若要了解有关 Runbook 类型、其优点和限制的详细信息，请参阅 [Azure 自动化 Runbook 类型](automation-runbook-types.md)
* 有关 PowerShell 脚本支持功能的详细信息，请参阅 [Azure 自动化中的本机 PowerShell 脚本支持](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)



<!--HONumber=Nov16_HO2-->


