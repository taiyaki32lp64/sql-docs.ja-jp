---
title: レプリケーションの CHECK 制約の無効化 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: af98fc70-24dd-4bd3-a0a3-f701dfa67b2c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66be3c8c81127b107f730fb38b0be10064d72926
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909377"
---
# <a name="disable-check-constraints-for-replication"></a>レプリケーションの CHECK 制約の無効化
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して CHECK 制約を無効にできます。 CHECK 制約はレプリケーションに対して明示的に無効にすることもできます。これは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのデータをパブリッシュする場合に便利です。  
  
> [!NOTE]  
>  レプリケーションを使用してテーブルをパブリッシュした場合、レプリケーション エージェントが実行する操作に対しては CHECK 制約が自動的に無効になります。 レプリケーション エージェントがサブスクライバー側で挿入、更新、または削除を実行した場合、制約のチェックは行われません。ユーザーが挿入、更新、または削除を実行した場合は、制約のチェックが行われます。 制約がレプリケーション エージェントに対して無効になるのは、データが最初に挿入、更新、または削除された際に、発行者側で既に制約がチェックされているためです。 詳細については、「 [スキーマ オプションの指定](../../relational-databases/replication/publish/specify-schema-options.md)」を参照してください。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>レプリケーションに対して CHECK 制約を無効にするには  
  
1.  **オブジェクト エクスプローラー**で、変更する CHECK 制約が設定されているテーブルを展開し、 **[制約]** フォルダーを展開します。  
  
2.  変更する CHECK 制約を右クリックし、 **[変更]** をクリックします。  
  
3.  **[CHECK 制約]** ダイアログ ボックスで、 **[テーブル デザイナー]** の **[レプリケーションに対して適用]** の値として **[いいえ]** を選択します。  
  
4.  **[閉じる]** をクリックします。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>レプリケーションに対して CHECK 制約を無効にするには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 最初の例では、IDENTITY 列を含むテーブルとテーブルに対する CHECK 制約を作成します。 次に、制約を削除した後、NOT FOR REPLICATION 句を指定して制約を再作成します。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.doc_exd (column_a int IDENTITY (1,1)   
    CONSTRAINT exd_check CHECK (column_a > 1))   
  
    ALTER TABLE dbo.doc_exd   
    DROP CONSTRAINT exd_check;   
    GO  
    ALTER TABLE dbo.doc_exd    
    ADD CONSTRAINT exd_check CHECK NOT FOR REPLICATION (column_a > 1);  
    ```  
  
 詳細については、「[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)」を参照してください。  
  
###  <a name="TsqlExample"></a>   
## <a name="see-also"></a>参照  
 [スキーマ オプションの指定](../../relational-databases/replication/publish/specify-schema-options.md)  
  
  
