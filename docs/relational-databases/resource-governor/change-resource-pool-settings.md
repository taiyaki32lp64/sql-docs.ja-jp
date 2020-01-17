---
title: リソース プールの設定の変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 8549b5a3a1675353ad0adce42fc63a460f893cae
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905018"
---
# <a name="change-resource-pool-settings"></a>リソース プールの設定の変更
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  リソース プールの設定を変更するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **リソース プールの設定変更に使用するもの:** [SQL Server Management Studio](#ChgRPProp)、[Transact-SQL](#ChgRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 CPU の割合の最大値は、CPU の割合の最小値以上にする必要があります。 メモリの割合の最大値は、メモリの割合の最小値以上にする必要があります。  
  
 すべてのリソース プールの CPU の割合の最小値の合計およびメモリの割合の最小値の合計が、それぞれ 100 を超えないようにしてください。  
  
###  <a name="Permissions"></a> Permissions  
 リソース プールの設定を変更するには、CONTROL SERVER 権限が必要です。  
  
##  <a name="ChgRPProp"></a> SQL Server Management Studio を使用してリソース プールの設定を変更する  
 **リソース プールの設定を変更するには - [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース プール]** ノードまで再帰的に展開します。  
  
2.  変更するリソース プールを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[リソース ガバナーのプロパティ]** ページで、自動的に **[リソース プール]** グリッドの対象リソース プールの行が選択されない場合は、その行を選択します。  
  
4.  変更する行のセルをクリックまたはダブルクリックし、新しい値を入力します。  
  
5.  変更を保存するには、 **[OK]** をクリックします。  

##  <a name="ChgRPTSQL"></a> Transact-SQL を使用してリソース プールの設定を変更する  
 **リソース プールの設定を変更するには - [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  変更するプロパティ値を指定する **ALTER RESOURCE POOL** または **ALTER EXTERNAL RESOURCE POOL** ステートメントを実行します。  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 次の例では、 `poolAdhoc`という名前のリソース プールの CPU の割合の最大値を変更します。  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [リソース プールの作成](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [リソース プールの削除](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [リソース ガバナー ワークロード グループ](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [リソース ガバナーの分類子関数](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
