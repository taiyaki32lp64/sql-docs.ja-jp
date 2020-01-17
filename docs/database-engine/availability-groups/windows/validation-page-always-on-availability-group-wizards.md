---
title: '可用性グループ ウィザード: [検証] ページ'
description: このトピックでは、Always On 可用性グループ ウィザードの [検証] ページにあるオプションについて説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.validation.f1
- sql13.swb.adddatabasewizard.validation.f1
- sql13.swb.newagwizard.validation.f1
helpviewer_keywords:
- ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f22ac0e249e693b7bcd102f6d9242c601e14331f
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74821841"
---
# <a name="validation-page-always-on-availability-group-wizards"></a>[検証] ページ (Always On 可用性グループ ウィザード)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
  このヘルプ トピックでは、 **[検証]** ページのオプションについて説明します。 このトピックの対象は、 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]の [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]、 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 、および [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]です。 このページでは、ウィザードのこれまでのページで選択したすべての構成が、使用している環境でサポートされているかどうかを検証できます。  
  
##  <a name="PageOptions"></a> [検証] ページのオプション  
 **[可用性グループの検証の結果。]**  
 このグリッドでは、完了した検証手順ごとの結果が表示されます。 グリッドの列は次のとおりです。  
  
 **Name**  
 各手順についての説明が表示されます。  
  
 **結果**  
 以下のハイパーリンク テキストのいずれかが表示されます。 特定の検証手順の結果の詳細については、ハイパーリンクをクリックしてください。  
  
|結果|[説明]|  
|------------|-----------------|  
|**Error**|検証手順が失敗したことを示します。 エラー メッセージを表示するには、リンクをクリックします。|  
|**Skipped**|不要と指定されていたため、検証手順がスキップされたことを示します。 手順がスキップされた理由を表示するには、リンクをクリックします。|  
|**Success**|検証手順が正常に完了したことを示します。|  
|**警告**|可用性グループの構成に関する潜在的な問題を示します。  警告メッセージを表示するには、リンクをクリックします。|  
  
 **[検証の再実行]**  
 検証エラーに対応して、ウィザードの外部で変更を行った場合に、検証手順を繰り返すときにクリックします。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループへのデータベース追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
