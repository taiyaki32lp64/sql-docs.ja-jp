---
title: リソース プールの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f4d18ef352c3e5ab6342e573d16bc3deaed5db72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211993"
---
# <a name="create-a-resource-pool"></a>リソース プールの作成
  リソース プールを作成するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **リソース プールの作成に使用するもの:** [SQL Server Management Studio](#CreRPProp)、[Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 CPU の割合の最大値は、CPU の割合の最小値以上にする必要があります。 メモリの割合の最大値は、メモリの割合の最小値以上にする必要があります。  
  
 すべてのリソース プールの CPU の割合の最小値の合計およびメモリの割合の最小値の合計が、それぞれ 100 を超えないようにしてください。  
  
###  <a name="Permissions"></a> Permissions  
 リソース プールを作成するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="CreRPProp"></a> SQL Server Management Studio を使用してリソース プールを作成する  
 **を使用してリソース プールを作成するには [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース ガバナー]** ノードまで再帰的に展開します。  
  
2.  **[リソース ガバナー]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[リソース プール]** グリッドで、空白行の最初の列をクリックします。 この列にアスタリスク (*) がラベルとして付加されます。  
  
4.  **[名前]** 列の空のセルをダブルクリックします。 リソース プールに使用する名前を入力します。  
  
5.  変更する行の他のセルをクリックまたはダブルクリックし、新しい値を入力します。  
  
6.  変更を保存するには、 **[OK]** をクリックします。  
  
##  <a name="CreRPTSQL"></a> Transact-SQL を使用してリソース プールを作成する  
 **を使用してリソース プールを作成するには [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  設定するプロパティ値を指定する `CREATE RESOURCE POOL` ステートメントを実行します。  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、 `poolAdhoc`というリソース プールを作成します。  
  
```  
CREATE RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 20);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [リソース ガバナー](resource-governor.md)   
 [リソース ガバナーの有効化](enable-resource-governor.md)   
 [リソース ガバナー リソース プール](resource-governor-resource-pool.md)   
 [リソース プールの設定の変更](change-resource-pool-settings.md)   
 [リソース プールの削除](delete-a-resource-pool.md)   
 [テンプレートを使用してリソース ガバナーを構成する](configure-resource-governor-using-a-template.md)   
 [リソース ガバナー ワークロード グループ](resource-governor-workload-group.md)   
 [リソース ガバナーの分類子関数](resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
