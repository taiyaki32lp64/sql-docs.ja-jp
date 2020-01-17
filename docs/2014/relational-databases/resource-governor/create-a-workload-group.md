---
title: ワークロード グループの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
ms.assetid: 072868ec-ceff-4db6-941b-281af731a067
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1cd3b72418d0791d70d28d2dca0a434190a2d4a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198920"
---
# <a name="create-a-workload-group"></a>ワークロード グループの作成
  ワークロード グループを作成するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **ワークロード グループの作成に使用するもの:** [SQL Server Management Studio](#CreWGProp)、[Transact-SQL](#CreWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 非固定パーティション テーブルのインデックス作成によって消費されるメモリは、含まれるパーティションの数に比例します。 必要なメモリの合計が、ワークロード グループの設定によって課せられているクエリごとの制限 (REQUEST_MAX_MEMORY_GRANT_PERCENT) を超えると、インデックス作成の実行に失敗します。 default ワークロード グループでは、SQL Server 2005 との互換性のために、クエリごとの制限を超えてもクエリの開始に必要な最低限のメモリを使用できるようになっているので、そのようなクエリを実行するのに十分な量のメモリが default リソース プールに対して構成されていれば、同じインデックス作成を default ワークロード グループで実行できる可能性があります。  
  
 インデックス作成では、パフォーマンスを向上させるため、最初に許可されたメモリ量を超えるメモリ ワークスペースの使用が許可されます。 この特別な処理はリソース ガバナーでサポートされていますが、最初のメモリ許可も追加のメモリ許可も、ワークロード グループ設定およびリソース プール設定によって制限されます。  
  
###  <a name="Permissions"></a> Permissions  
 ワークロード グループを作成するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="CreWGProp"></a> SQL Server Management Studio を使用してワークロード グループを作成する  
 **ワークロード グループを作成するには [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  オブジェクト エクスプローラーで、変更するワークロード グループを含むリソース プールまで **[管理]** ノードを再帰的に展開します。  
  
2.  **[ワークロード グループ]** フォルダーを右クリックし、 **[新しいワークロード グループ]** をクリックします。  
  
3.  **[リソース プール]** グリッドに、ワークロード グループを追加するリソース プールが強調表示されていることを確認します。  
  
4.  **[リソース プールのワークロード グループ]** グリッドに新規行が追加され、他の列には空の名前と既定値が表示されます。  
  
5.  **[名前]** セルをクリックし、ワークロード グループの名前を入力します。  
  
6.  既定値から変更する場合は、その対象となる行の他のセルをクリックまたはダブルクリックし、新しい値を入力します。  
  
7.  変更を保存するには、 **[OK]** をクリックします。  
  
##  <a name="CreWGTSQL"></a> Transact-SQL を使用してワークロード グループを作成する  
 **ワークロード グループを作成するには [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  設定するプロパティ値を指定する CREATE WORKLOAD GROUP ステートメントを実行します。  
  
2.  ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、 `groupAdhoc` という名前のリソース プール内に `poolAdhoc`という名前のワークロード グループを作成します。  
  
```  
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [リソース ガバナー](resource-governor.md)   
 [リソース ガバナーの有効化](enable-resource-governor.md)   
 [リソース プールの作成](create-a-resource-pool.md)   
 [ワークロード グループの設定の変更](change-workload-group-settings.md)   
 [ユーザー定義の分類子関数の作成とテスト](create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
