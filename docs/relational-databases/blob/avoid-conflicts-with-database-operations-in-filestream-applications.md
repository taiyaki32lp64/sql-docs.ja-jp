---
title: 競合の回避 - FILESTREAM データベース操作 | Microsoft Docs
description: FILESTREAM アプリケーションでのデータベース操作との競合の回避
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32 and Transact-SQL Conflicts
ms.assetid: 8b1ee196-69af-4f9b-9bf5-63d8ac2bc39b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7b347a140c07436553945555e52d212e4751fcc4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255580"
---
# <a name="avoid-conflicts-with-database-operations-in-filestream-applications"></a>FILESTREAM アプリケーションでのデータベース操作との競合の回避
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SqlOpenFilestream() により Win32 ファイル ハンドルを開いて FILESTREAM BLOB データの読み取りまたは書き込みを行うアプリケーションでは、共通のトランザクションで管理される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで競合エラーが発生する場合があります。 この例として、完了までに時間がかかる [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリや MARS クエリなどがあります。 アプリケーションは、このような競合を回避できるように注意深く設計する必要があります。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] またはアプリケーションが FILESTREAM BLOB を開こうとする場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって、関連付けられたトランザクション コンテキストがチェックされます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、DDL ステートメント、DML ステートメント、データの取得、トランザクションの管理のうち、どれが開く操作の対象になっているかに基づいて、要求を許可または拒否します。 次の表は、トランザクションで開いているファイルの種類に基づいて、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ステートメントが許可されるか拒否されるかが、 [!INCLUDE[tsql](../../includes/tsql-md.md)] でどのように決まるかを示しています。  
  
|Transact-SQL ステートメント|読み取り用に開く|書き込み用に開く|  
|------------------------------|---------------------|----------------------|  
|CREATE TABLE、CREATE INDEX、DROP TABLE、ALTER TABLE などの、データベース メタデータを処理する DDL ステートメント|許可|ブロックされてタイムアウトで失敗|  
|UPDATE、DELETE、INSERT などの、データベース内に格納されているデータを処理する DML ステートメント|許可|拒否|  
|SELECT|許可|許可|  
|COMMIT TRANSACTION|拒否*|拒否*|  
|SAVE TRANSACTION|拒否*|拒否*|  
|ROLLBACK|許可*|許可*|  
  
 \* トランザクションは取り消され、トランザクション コンテキストで開かれたハンドルは無効になります。 アプリケーションは、開いているハンドルをすべて閉じる必要があります。  
  
## <a name="examples"></a>例  
 次の例に、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントと FILESTREAM Win32 アクセスで競合が発生する可能性がある場合を示します。  
  
### <a name="a-opening-a-filestream-blob-for-write-access"></a>A. 書き込みアクセス用に FILESTREAM BLOB を開く  
 次の例は、書き込み専用アクセスでファイルを開いた場合の影響を示しています。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//Write some date to the FILESTREAM BLOB.  
WriteFile(dstHandle, updateData, ...);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed. The FILESTREAM BLOB is  
//returned without the modifications that are made by  
//WriteFile(dstHandle, updateData, ...).  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed. The FILESTREAM BLOB  
//is returned with the updateData applied.  
```  
  
### <a name="b-opening-a-filestream-blob-for-read-access"></a>B. 読み取りアクセス用に FILESTREAM BLOB を開く  
 次の例は、読み取り専用アクセスでファイルを開いた場合の影響を示しています。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed. Any changes that are  
//made to the FILESTREAM BLOB will not be returned until  
//the dstHandle is closed.  
//SELECT statements will be allowed.  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="c-opening-and-closing-multiple-filestream-blob-files"></a>C. 複数の FILESTREAM BLOB ファイルを開いて閉じる  
 複数のファイルが開いている場合は、最も厳しい規則が使用されます。 2 つのファイルを開く例を次に示します。 最初のファイルは読み取り用に、2 番目のファイルは書き込み用に開かれます。 DML ステートメントは、2 番目のファイルが開かれるまで拒否されます。  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
  
dstHandle1 =  OpenSqlFilestream(dstFilePath1, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
//Close the read handle. The write handle is still open.  
CloseHandle(dstHandle);  
//DML statements are still denied because the write handle is open.  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
CloseHandle(dstHandle1);  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="d-failing-to-close-a-cursor"></a>D. カーソルが閉じられていない  
 次の例では、ステートメントのカーソルが閉じられていないために、 `OpenSqlFilestream()` で書き込みアクセス用に BLOB を開くことができない場合を示しています。  
  
```  
TCHAR *sqlDBQuery =  
TEXT("SELECT GET_FILESTREAM_TRANSACTION_CONTEXT(),")  
TEXT("Chart.PathName() FROM Archive.dbo.Records");  
  
//Execute a long-running Transact-SQL statement. Do not allow  
//the statement to complete before trying to  
//open the file.  
  
SQLExecDirect(hstmt, sqlDBQuery, SQL_NTS);  
  
//Before you call OpenSqlFilestream() any open files  
//that the Cursor the Transact-SQL statement is using  
// must be closed. In this example,  
//SQLCloseCursor(hstmt) is not called so that  
//the transaction will indicate that there is a file  
//open for reading. This will cause the call to  
//OpenSqlFilestream() to fail because the file is  
//still open.  
  
HANDLE srcHandle =  OpenSqlFilestream(srcFilePath,  
     Write, 0,  transactionToken,  cbTransactionToken,  0);  
  
//srcHandle will == INVALID_HANDLE_VALUE because the  
//cursor is still open.  
```  
  
## <a name="see-also"></a>参照  
 [OpenSqlFilestream による FILESTREAM データへのアクセス](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [複数のアクティブな結果セット &#40;MARS&#41; の使用](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
  
  
