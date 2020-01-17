---
title: セマンティック検索による類似および関連したドキュメントの取得 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], document similarity queries
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1b2e30534fb5e0232ff2046e30e2e14075dfb807
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011317"
---
# <a name="find-similar-and-related-documents-with-semantic-search"></a>セマンティック検索による類似および関連したドキュメントの取得
  統計的セマンティック インデックス作成用に構成されている列での、類似性または関連性のあるドキュメントやテキスト値の検索方法と、どのように類似または関連しているかという情報の検索方法について説明します。  
  
##  <a name="BasicsQuerySimilar"></a> 類似または関連ドキュメントの検索  
  
###  <a name="HowToQuerySimilar"></a> 方法:類似または関連ドキュメントを SEMANTICSIMILARITYTABLE で見つける  
 特定の列で類似または関連したドキュメントを識別するには、[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql) 関数を使用してクエリを実行します。  
  
 **SEMANTICSIMILARITYTABLE** は、指定されたドキュメントに意味が似ているコンテンツを指定された列に持っている行 (0 行、1 行、または複数の行) から成るテーブルを返します。 この行セット関数は、標準のテーブル名のように、SELECT ステートメントの FROM 句で参照できます。  
  
 複数の列にわたって類似したドキュメントに対するクエリを実行することはできません。 **SEMANTICSIMILARITYTABLE** 関数は、**source_key** 引数によって識別されるソース列と同じ列からのみ結果を取得します。  
  
 **SEMANTICSIMILARITYTABLE** 関数に必要なパラメーターの詳細や関数から返される結果のテーブルについては、「[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)」を参照してください。  
  
> [!IMPORTANT]  
>  対象の列では、フルテキスト インデックスとセマンティック インデックスが有効になっている必要があります。  
  
###  <a name="HowToIdentifySimilar"></a> 例: 別のドキュメントに類似する上位のドキュメントを検索します。  
 次の例では、AdventureWorks2012 サンプル データベースの HumanResources.JobCandidate テーブルから、 *@CandidateID* で指定した候補に類似する上位 10 件の候補を取得します。  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROM SEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
##  <a name="BasicsQuerySimilarity"></a> ドキュメントが類似または関連する方法に関する情報の入手  
  
###  <a name="HowToQuerySimilarity"></a> 方法:ドキュメントは、類似または関連 semanticsimilaritydetailstable の各使用方法に関する情報を確認します。  
 ドキュメントが類似または関連する原因となっているキー フレーズに関する情報を表示するには、[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql) 関数を使用してクエリを実行します。  
  
 **SEMANTICSIMILARITYDETAILSTABLE** は、意味が似たコンテンツを持つ 2 つのドキュメント (ソース ドキュメントと一致するドキュメント) に共通するキー フレーズの 0 行、1 行、または複数の行から成るテーブルを返します。 この行セット関数は、標準のテーブル名のように、SELECT ステートメントの FROM 句で参照できます。  
  
 **SEMANTICSIMILARITYDETAILTABLE** 関数に必要なパラメーターの詳細や関数から返される結果のテーブルについては、「[semanticsimilaritydetailtable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)」を参照してください。  
  
> [!IMPORTANT]  
>  対象の列では、フルテキスト インデックスとセマンティック インデックスが有効になっている必要があります。  
  
###  <a name="HowToSimilarPhrases"></a> 例: ドキュメント間で類似する上位のキー フレーズを検索します。  
 次の例では、AdventureWorks2012 サンプル データベースの **HumanResources.JobCandidate** テーブル内の指定された候補間で最も類似スコアが高い 5 つのキー フレーズを取得します。  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROM SEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
  
