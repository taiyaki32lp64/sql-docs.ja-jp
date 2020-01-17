---
title: ワークロード グループの設定の変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], alter
- Resource Governor, workload group alter
ms.assetid: 73b6109c-2ad0-4915-b11b-d40d5a0fdc25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2bcb3cfa20948e6bb0964d29331ca1d426b8916
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199915"
---
# <a name="change-workload-group-settings"></a>ワークロード グループの設定の変更
  ワークロード グループの設定を変更するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **ワークロード グループの設定変更に使用するもの:** [SQL Server Management Studio](#ChgWGProp)、[Transact-SQL](#ChgWGTSQL)  
  
## <a name="before-you-begin"></a>はじめに  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 既定のワークロード グループとユーザー定義のワークロード グループの設定を変更することができます。  
  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 非固定パーティション テーブルのインデックス作成によって消費されるメモリは、含まれるパーティションの数に比例します。 必要なメモリの合計が、ワークロード グループの設定によって課せられているクエリごとの制限 (REQUEST_MAX_MEMORY_GRANT_PERCENT) を超えると、インデックス作成の実行に失敗します。 default ワークロード グループでは、SQL Server 2005 との互換性のために、クエリごとの制限を超えてもクエリの開始に必要な最低限のメモリを使用できるようになっているので、そのようなクエリを実行するのに十分な量のメモリが default リソース プールに対して構成されていれば、同じインデックス作成を default ワークロード グループで実行できる可能性があります。  
  
 インデックス作成では、パフォーマンスを向上させるため、最初に許可されたメモリ量を超えるメモリ ワークスペースの使用が許可されます。 この特別な処理はリソース ガバナーでサポートされていますが、最初のメモリ許可も追加のメモリ許可も、ワークロード グループ設定およびリソース プール設定によって制限されます。  
  
###  <a name="Permissions"></a> Permissions  
 ワークロード グループの設定を変更するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="ChgWGProp"></a> SQL Server Management Studio を使用してワークロード グループの設定を変更する  
 **ワークロード グループの設定を変更するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  オブジェクト エクスプローラーで、変更するワークロード グループを含む **ワークロード グループ** フォルダーまで **[管理]** ノードを再帰的に展開します。  
  
2.  変更するワークロード グループを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[リソース ガバナーのプロパティ]** ページで、自動的に **[リソース プールのワークロード グループ]** グリッドの対象ワークロード グループの行が選択されない場合は、その行を選択します。  
  
4.  変更する行のセルをクリックまたはダブルクリックし、新しい値を入力します。  
  
5.  変更を保存するには、 **[OK]** をクリックします。  
  
##  <a name="ChgWGTSQL"></a> Transact-SQL を使用してワークロード グループの設定を変更する  
 **Transact-SQL を使用してワークロード グループの設定を変更するには**  
  
1.  変更するプロパティ値を指定する ALTER WORKLOAD GROUP ステートメントを実行します。  
  
2.  ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、 `groupAdhoc`という名前のワークロード グループに割り当てられたメモリ許可の割合の最大値を変更します。  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
WITH (REQUEST_MAX_MEMORY_GRANT_PERCENT = 30);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](resource-governor.md)   
 [ワークロード グループの作成](create-a-workload-group.md)   
 [リソース プールの作成](create-a-resource-pool.md)   
 [リソース プールの設定の変更](change-resource-pool-settings.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-workload-group-transact-sql)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
