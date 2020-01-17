---
title: データベースのサイズを大きくする | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], size
- increasing database size
- database size [SQL Server], increasing
- size [SQL Server], databases
ms.assetid: 14f4206d-3afa-4ba9-9849-23e81d63306d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02a34ba1e0f441b665c239d60f6398afa4247102
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917236"
---
# <a name="increase-the-size-of-a-database"></a>データベースのサイズを大きくする
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、データベースのサイズを大きくする方法について説明します。 既存のデータ ファイルまたはログ ファイルのサイズを大きくするか、データベースに新しいファイルを追加することで、データベースを拡張します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してデータベースのサイズを大きくするには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   BACKUP ステートメントの実行中にファイルを追加したり削除したりすることはできません。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-increase-the-size-of-a-database"></a>データベースのサイズを大きくするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、サイズを大きくするデータベースを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[データベースのプロパティ]** ダイアログ ボックスで、 **[ファイル]** ページをクリックします。  
  
4.  既存のファイルのサイズを大きくするには、目的のファイルの **[初期サイズ (MB)]** 列の値を大きくします。 データベースのサイズは、少なくとも 1 MB ずつ大きくする必要があります。  
  
5.  新しいファイルを追加してデータベースのサイズを大きくするには、 **[追加]** をクリックして、新しいファイルの値を入力します。 詳細については、「 [データベースに対するデータ ファイルまたはログ ファイルの追加](add-data-or-log-files-to-a-database.md)」をご覧ください。  
  
6.  **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-increase-the-size-of-a-database"></a>データベースのサイズを大きくするには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、`test1dat3` ファイルのサイズを拡張します。  
  
 [!code-sql[DatabaseDDL#AlterDatabase5](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase5)]  
  
 その他の例については、「[ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [データベースに対するデータ ファイルまたはログ ファイルの追加](add-data-or-log-files-to-a-database.md)   
 [データベースの圧縮](shrink-a-database.md)  
  
  
