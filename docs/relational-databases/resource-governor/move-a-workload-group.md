---
title: ワークロード グループの移動 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties_moveworkloadgroup.f1
helpviewer_keywords:
- workload groups [SQL Server], move
- Resource Governor, workload group move
ms.assetid: f2068636-6e53-486a-a6fc-c12de2a38424
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 7f4d77bba168f84b42aab0884369cf834af3779d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099227"
---
# <a name="move-a-workload-group"></a>ワークロード グループの移動
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  リソース ガバナーのワークロード グループを別のリソース プールに移動するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Transact-SQL を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **ワークロード グループの移動に使用するもの:** [SQL Server Management Studio](#MoveWGSSMS)、[Transact-SQL](#MoveWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 リソース ガバナーの保留中の構成操作がある場合、ワークロード グループを移動できません。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 リソース ガバナーの保留中の構成操作がある場合、ワークロード グループを移動できません。 [sys.dm_resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) 動的管理ビューにクエリを実行して is_configuration_pending の現在の状態を取得することにより、構成が保留中かどうかを確認できます。  
  
###  <a name="Permissions"></a> Permissions  
 ワークロード グループを移動するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="MoveWGSSMS"></a> SQL Server Management Studio を使用してワークロード グループを移動する  
 **を使用してワークロード グループを移動するには [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**  
  
1.  オブジェクト エクスプローラーで、 **[管理]** ノードを **[リソース ガバナー]** ノードまで再帰的に展開します。  
  
2.  **[リソース ガバナー]** を右クリックし、 **[プロパティ]** をクリックすると、 **[リソース ガバナーのプロパティ]** ページが開きます。  
  
3.  **[リソース プール]** ウィンドウで、移動するワークロード グループを含むリソース プールをクリックします。 **[ワークロード グループ]** ウィンドウに、対象リソース プール内のワークロード グループが表示されます。  
  
4.  **[ワークロード グループ]** ウィンドウで、移動するワークロード グループの左にある右矢印を右クリックして **[移動先]** をクリックします。 **[ワークロード グループの移動]** ウィンドウが表示されます。  
  
5.  使用可能なリソース プールがウィンドウに表示されます。 ワークロード グループの移動先とするリソース プールの名前をクリックし、 **[OK]** をクリックしてこの操作を実行します。  
  
6.  この操作は、 **[OK]** をクリックするまで完了しません。 **[OK]** をクリックすると、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントが実行されます。  
  
7.  リソース プールまたはワークロード グループの作成操作または再構成操作が失敗した場合は、プロパティ ページのタイトルの下に簡単なエラー メッセージが表示されます。 詳細なエラー メッセージを表示するには、エラー メッセージの下矢印をクリックします。  
  
##  <a name="MoveWGTSQL"></a> Transact-SQL を使用してワークロード グループを移動する  
 **Transact-SQL を使用してワークロード グループを移動するには**  
  
1.  移動するワークロード グループと移動先とするリソース プールの名前を指定する **ALTER WORKLOAD GROUP** ステートメントを実行します。  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、 `groupAdhoc` という名前のワークロード グループを既定のリソース プールに移動します。  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [リソース プールの作成](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [ワークロード グループの作成](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
