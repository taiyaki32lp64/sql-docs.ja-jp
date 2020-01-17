---
title: テーブルの複製 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- tables [SQL Server], duplicating
- duplicating tables
- table copying [SQL Server]
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 45fabf20b18fb0f3227f99ab2a6b5270e245562a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907305"
---
# <a name="duplicate-tables"></a>テーブルの複製
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、新しいテーブルを作成して既存のテーブルから列情報をコピーすることで既存のテーブルを複製できます。  
  
> [!IMPORTANT]  
>  この操作によって複製されるのはテーブルの構造のみです。テーブル行は複製されません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [セキュリティ](#Security)  
  
-   **テーブルを複製するための方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 対象となるデータベースの CREATE TABLE 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-duplicate-a-table"></a>テーブルを複製するには  
  
1.  テーブルを作成するデータベースに接続していること、およびそのデータベースがオブジェクト エクスプローラーで選択されていることを確認します。  
  
2.  オブジェクト エクスプローラーで、 **[テーブル]** を右クリックし、 **[新しいテーブル]** をクリックします。  
  
3.  オブジェクト エクスプローラーで、コピーするテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
4.  既存のテーブルの列を選択し、 **[編集]** メニューの **[コピー]** をクリックします。  
  
5.  新しいテーブルに戻り、1 行目を選択します。  
  
6.  **[編集]** メニューの **[貼り付け]** をクリックします。  
  
7.  **[ファイル]** メニューの **[<_テーブル名_> を保存]** をクリックします。  
  
8.  **[名前の選択]** ダイアログ ボックスで、新しいテーブルの名前を入力し、 **[OK]** をクリックします。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-duplicate-a-table-in-query-editor"></a>クエリ エディターでテーブルを複製するには  
  
1.  テーブルを作成するデータベースに接続していること、およびそのデータベースがオブジェクト エクスプローラーで選択されていることを確認します。  
  
2.  複製するテーブルを右クリックし、 **[テーブルをスクリプト化]** をポイントして、 **[CREATE]** をポイントします。次に、 **[新しいクエリ エディター ウィンドウ]** をクリックします。  
  
3.  テーブルの名前を変更します。  
  
4.  新しいテーブルに必要でない列をすべて削除します。  
  
5.  **[実行]** をクリックします。  
  
  
