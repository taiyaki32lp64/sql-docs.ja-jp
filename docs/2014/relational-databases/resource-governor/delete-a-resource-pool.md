---
title: リソース プールの削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool delete
- resource pools [SQL Server], delete
ms.assetid: 3bdd348b-6582-4ffa-80ef-d49e50596ce5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6e2e9582e8a279be37e05e9ee13a858abb431987
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205835"
---
# <a name="delete-a-resource-pool"></a>リソース プールの削除
  リソース プールを削除にするには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Transact-SQL を使用します。  
  
-   **作業を開始する準備:**[制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **リソース プールの削除に使用するもの:**[SQL Server Management Studio](#DelRPSSMS)、[Transact-SQL](#DelRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 ワークロード グループが含まれている場合は、リソース プールを削除できません。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 リソース ガバナーの既定のリソース プールや内部リソース プールを削除することはできません。 ワークロード グループが含まれている場合は、リソース プールを削除できません。 詳細については、「 [Delete a Workload Group](delete-a-workload-group.md)」を参照してください。  
  
###  <a name="Permissions"></a> Permissions  
 リソース プールを削除するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="DelRPSSMS"></a> オブジェクト エクスプ ローラーを使用してリソース プールを削除する  
 **SQL Server Management Studio を使用してリソース プールを削除するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース ガバナー]** ノードまで再帰的に展開します。  
  
2.  削除するリソース プールを右クリックし、 **[削除]** をクリックします。  
  
3.  **[オブジェクトの削除]** ウィンドウの **[削除されるオブジェクト]** ボックスの一覧に、リソース プールが表示されます。 リソース プールを削除するには、 **[OK]** をクリックします。  
  
    > [!NOTE]  
    >  ワークロード グループが含まれているリソース プールを削除しようとすると失敗します。  
  
##  <a name="DelRPTSQL"></a> Transact-SQL を使用してリソース プールを削除する  
 **Transact-SQL を使用してリソース プールを削除するには**  
  
1.  削除するリソース プールの名前を示す `DROP RESOURCE POOL` ステートメントを実行します。  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、 `poolAdhoc`というワークロード グループを削除します。  
  
```  
DROP RESOURCE POOL poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](resource-governor.md)   
 [リソース ガバナー リソース プール](resource-governor-resource-pool.md)   
 [リソース プールの作成](create-a-resource-pool.md)   
 [リソース プールの設定の変更](change-resource-pool-settings.md)   
 [リソース ガバナー ワークロード グループ](resource-governor-workload-group.md)   
 [リソース ガバナーの分類子関数](resource-governor-classifier-function.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-workload-group-transact-sql)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
