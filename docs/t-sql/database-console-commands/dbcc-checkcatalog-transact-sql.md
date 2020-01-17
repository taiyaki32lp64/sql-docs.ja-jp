---
title: DBCC CHECKCATALOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_CHECKCATALOG_TSQL
- DBCC CHECKCATALOG
- CHECKCATALOG_TSQL
- CHECKCATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- catalogs [SQL Server], consistency checks
- checking catalog consistency
- DBCC CHECKCATALOG statement
- integrity [SQL Server], catalogs
- consistency [SQL Server], catalogs
ms.assetid: 8076eb4e-f049-44bf-9a35-45cdd6ef0105
author: pmasl
ms.author: umajay
ms.openlocfilehash: d75739e2a8594bbd049a7d9b1c2a6908b1c0e29c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102202"
---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定されたデータベース内でのカタログの一貫性をチェックします。 データベースはオンラインである必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DBCC CHECKCATALOG   
[   
    (   
    database_name | database_id | 0  
    )  
]  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>引数  
 *database_name* | *database_id* | 0  
 カタログの一貫性をチェックするデータベースの名前または ID です。 値を指定しないか 0 を指定した場合は、現在のデータベースが使用されます。 データベース名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
 WITH NO_INFOMSGS  
 すべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks  
DBCC CATALOG コマンドの終了後、メッセージが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに書き込まれます。 DBCC コマンドが正常に実行された場合、メッセージでは正常完了とコマンド実行時間が示されます。 エラーが発生して DBCC コマンドが完了前に停止した場合、メッセージではコマンドが終了したことと、状態の値、コマンド実行時間が示されます。 次の表は、メッセージに含まれる可能性がある状態値の一覧と説明です。
  
|状態|[説明]|  
|-----------|-----------------|  
|0|エラー番号 8930 が発生しました。 メタデータの破損が原因で DBCC コマンドが終了しました。|  
|1|エラー番号 8967 が発生しました。 内部 DBCC エラーがあります。|  
|2|緊急モードのデータベース修復中にエラーが発生しました。|  
|3|メタデータの破損が原因で DBCC コマンドが終了しました。|  
|4|アサートまたはアクセス違反が検出されました。|  
|5|不明なエラーが発生し、DBCC コマンドが終了しました。|  
  
DBCC CHECKCATALOG は、システム メタデータ テーブル間でさまざまな一貫性チェックを実行します。 DBCC CHECKCATALOG は、内部データベース スナップショットを使用してこれらのチェックを実行するために必要なトランザクション一貫性を確保します。 詳細については、次を参照してください。「[データベース スナップショットのスパース ファイルのサイズを表示する方法 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)」および「[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)」の「DBCC 内部データベース スナップショットの使用」セクション。
スナップショットが作成できない場合、DBCC CHECKCATALOG は排他データベース ロックを獲得して必要な一貫性を取得します。 不一致が検出された場合、これらは修復できず、データベースをバックアップから復元する必要があります。
  
> [!NOTE]  
> **tempdb** に対して DBCC CHECKCATALOG を実行してもチェックは実行されません。 これは、パフォーマンス上の理由から、データベースのスナップショットが **tempdb** では利用できないためです。 つまり、必要なトランザクションの一貫性を実現できないためです。 **tempdb** メタデータの問題を解決するにはサーバーを再利用します。  
  
> [!NOTE]  
> DBCC CHECKCATALOG では、FILESTREAM データはチェックされません。 FILESTREAM はバイナリ ラージ オブジェクト (BLOB) をファイル システムに格納します。  
  
DBCC CHECKCATALOG は、[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) の一部としても実行されます。
  
## <a name="result-sets"></a>結果セット  
データベースが指定されていない場合、DBCC CHECKCATALOG は次の値を返します。
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] がデータベース名として指定されていない場合、DBCC CHECKCATALOG は次の値を返します。
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
次の例では、現在のデータベースと `AdventureWorks` データベースの両方におけるカタログの整合性をチェックしています。
  
```sql
-- Check the current database.  
DBCC CHECKCATALOG;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKCATALOG (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  
