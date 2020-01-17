---
title: リソース ガバナーの有効化 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, enabling
ms.assetid: 4d17af53-cf11-4ce4-aab4-deda94a49836
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 23ff55d4fcb9e9cf398e732376a01ab5495b2a4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099248"
---
# <a name="enable-resource-governor"></a>リソース ガバナーの有効化
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  リソース ガバナーは、既定ではオフになっています。 リソース ガバナーを有効にするには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Transact-SQL を使用します。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#LimitationsRestrictions)、[権限](#Permissions)  
  
-   **リソース ガバナーの有効化に使用するもの:** [オブジェクト エクスプローラー](#RGOnObjEx)、[リソース ガバナーのプロパティ](#RGOnProp)、[Transact-SQL](#RGOnTSQL)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 リソース ガバナーを有効にすると、結果は次のようになります。  
  
-   新しい接続に対して分類子関数が実行され、それらのワークロードがワークロード グループに割り当てられます。  
  
-   リソース ガバナー構成で指定されているリソース制限が有効になり適用されます。  
  
-   リソース ガバナーを有効にする前に存在していた要求に、リソース ガバナーが無効であったときに加えた構成の変更が反映されます。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 ユーザー トランザクション内でリソース ガバナーを有効にする場合、 **ALTER RESOURCE GOVERNOR** ステートメントを使用できません。  
  
###  <a name="Permissions"></a> Permissions  
 リソース ガバナーを有効にするには、CONTROL SERVER 権限が必要です。  
  
##  <a name="RGOnObjEx"></a> オブジェクト エクスプローラーを使用してリソース ガバナーを有効にする  
 **オブジェクト エクスプローラーを使用してリソース ガバナーを有効にするには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース ガバナー]** ノードまで再帰的に展開します。  
  
2.  **[リソース ガバナー]** を右クリックし、 **[有効化]** をクリックします。  
  
##  <a name="RGOnProp"></a> リソース ガバナーのプロパティを使用してリソース ガバナーを有効にする  
 **[リソース ガバナーのプロパティ] ページでリソース ガバナーを有効にするには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを開き、 **[管理]** ノードを **[リソース ガバナー]** ノードまで再帰的に展開します。  
  
2.  **[リソース ガバナー]** を右クリックし、 **[プロパティ]** をクリックすると、 **[リソース ガバナーのプロパティ]** ページが開きます。  
  
3.  **[リソース ガバナーの有効化]** チェック ボックスをオンにしてから、 **[OK]** をクリックします。  
  
##  <a name="RGOnTSQL"></a> Transact-SQL を使用してリソース ガバナーを有効にする  
 **Transact-SQL を使用してリソース ガバナーを有効にするには**  
  
1.  **ALTER RESOURCE GOVERNOR RECONFIGURE** ステートメントを実行します。  
  
### <a name="example-transact-sql"></a>例 (Transact-SQL)  
 リソース ガバナーを有効にする例を次に示します。  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [リソース ガバナーを無効にしたとき](../../relational-databases/resource-governor/disable-resource-governor.md)   
 [リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [リソース ガバナー ワークロード グループ](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [リソース ガバナーの分類子関数](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
