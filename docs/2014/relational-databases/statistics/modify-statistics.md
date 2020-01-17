---
title: 統計の変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2da978efd869a748bb48f6d494d59ae2f4cfb019
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211860"
---
# <a name="modify-statistics"></a>統計の変更
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して既存の統計を変更できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **統計を変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 以下の条件が必要です:  
  
-   ユーザーは、テーブルまたはビューに対する ALTER 権限が必要です。  
  
-   ユーザーがテーブルまたはインデックス付きビューの所有者であるか、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、または **db_ddladmin** 固定データベース ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-statistics"></a>統計を変更するには  
  
1.  **オブジェクト エクスプローラー**で、統計を変更するデータベースをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[テーブル]** フォルダーを展開します。  
  
3.  プラス記号をクリックして、統計を変更するテーブルを展開します。  
  
4.  プラス記号をクリックして **[統計]** フォルダーを展開します。  
  
5.  変更する統計オブジェクトを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[統計のプロパティ -** *statistics_name* ] ダイアログ ボックスの **[全般]** ページで **[追加]** , **[削除]** , **[上へ移動]** 、 **[下へ移動]** 、 any combination, to alter the properties of the statistics. **[統計の列]** グリッド内の列の位置は、統計の使いやすさに影響する可能性があることに注意してください。  
  
7.  **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **統計を変更するには**  
  
 Transact-SQL ステートメントを使用して、このタスクを実行することはできません。 Transact-SQL を使用して統計を変更するには、既存の統計を削除してから新しい属性を再作成します。  
  
 詳細については、「[DROP STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql)」および「[CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)」を参照してください。  
  
  
