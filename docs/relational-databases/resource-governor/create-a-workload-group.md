---
title: ワークロード グループの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 237ec09347ab139aabcc9f475f5e3b64aba0f054
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633003"
---
# <a name="create-a-workload-group"></a>ワークロード グループの作成

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ワークロード グループを作成するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **ワークロード グループの作成に使用するもの:** [SQL Server Management Studio](#CreRPProp)、[Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項

 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 非固定パーティション テーブルのインデックス作成によって消費されるメモリは、含まれるパーティションの数に比例します。 必要なメモリの合計が、ワークロード グループの設定によって課せられているクエリごとの制限 (REQUEST_MAX_MEMORY_GRANT_PERCENT) を超えると、インデックス作成の実行に失敗します。 default ワークロード グループでは、SQL Server 2005 との互換性のために、クエリごとの制限を超えてもクエリの開始に必要な最低限のメモリを使用できるようになっているので、そのようなクエリを実行するのに十分な量のメモリが default リソース プールに対して構成されていれば、同じインデックス作成を default ワークロード グループで実行できる可能性があります。  
  
 インデックス作成では、パフォーマンスを向上させるため、最初に許可されたメモリ量を超えるメモリ ワークスペースの使用が許可されます。 この特別な処理はリソース ガバナーでサポートされていますが、最初のメモリ許可も追加のメモリ許可も、ワークロード グループ設定およびリソース プール設定によって制限されます。  
  
###  <a name="Permissions"></a> Permissions

 ワークロード グループを作成するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="CreRPProp"></a> SQL Server Management Studio を使用してワークロード グループを作成する

 **ワークロード グループを作成するには [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  オブジェクト エクスプローラーで、変更するワークロード グループを含むリソース プールまで **[管理]** ノードを再帰的に展開します。  
  
2.  **[ワークロード グループ]** フォルダーを右クリックし、 **[新しいワークロード グループ]** をクリックします。  
  
3.  **[リソース プール]** グリッドに、ワークロード グループを追加するリソース プールが強調表示されていることを確認します。  
  
4.  **[リソース プールのワークロード グループ]** グリッドに新規行が追加され、他の列には空の名前と既定値が表示されます。  
  
5.  **[名前]** セルをクリックし、ワークロード グループの名前を入力します。  
  
6.  既定値から変更する場合は、その対象となる行の他のセルをクリックまたはダブルクリックし、新しい値を入力します。  
  
7.  変更を保存するには、 **[OK]** をクリックします。  

##  <a name="CreRPTSQL"></a> Transact-SQL を使用してワークロード グループを作成する  
 **ワークロード グループを作成するには [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  設定するプロパティ値を指定する CREATE WORKLOAD GROUP ステートメントを実行します。  
  
2.  ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)

 次の例では、 `groupAdhoc` という名前のリソース プール内に `poolAdhoc`という名前のワークロード グループを作成します。  
  
```sql
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照

 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [リソース プールの作成](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [ワークロード グループの設定の変更](../../relational-databases/resource-governor/change-workload-group-settings.md)   
 [ユーザー定義の分類子関数の作成とテスト](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
  
