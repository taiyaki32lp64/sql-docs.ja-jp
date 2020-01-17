---
title: Transact-SQL による FILESTREAM データへのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Transact-SQL
ms.assetid: a6bf0ce7-7e5e-4a07-8917-ee526c9d0a05
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 067f14e857addc5f43a0b17d81d554997adbc09f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010444"
---
# <a name="access-filestream-data-with-transact-sql"></a>Transact-SQL による FILESTREAM データへのアクセス
  このトピックでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] の INSERT、UPDATE、および DELETE ステートメントを使用して FILESTREAM データを管理する方法について説明します。  
  
> [!NOTE]  
>  このトピックの例を実行するには、「 [FILESTREAM が有効なデータベースを作成する方法](create-a-filestream-enabled-database.md) 」および「 [FILESTREAM データを格納するテーブルを作成する方法](create-a-table-for-storing-filestream-data.md)」に基づいて、FILESTREAM が有効なデータベースとテーブルを作成する必要があります。  
  
##  <a name="ins"></a> FILESTREAM データを含む行の挿入  
 FILESTREAM データをサポートするテーブルに行を追加するには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT ステートメントを使用します。 NULL を挿入するには、FILESTREAM 列にデータを挿入するとき、または`varbinary(max)`値。  
  
### <a name="inserting-null"></a>NULL の挿入  
 `NULL`を挿入する方法を次の例に示します。 FILESTREAM 値が `NULL`の場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] はファイル システムにファイルを作成しません。  
  
 [!code-sql[FILESTREAM#FS_InsertNULL](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertnull)]  
  
### <a name="inserting-a-zero-length-record"></a>長さ 0 のレコードの挿入  
 `INSERT` を使用して長さ 0 のレコードを作成する方法を次の例に示します。 これは、ファイル ハンドルを取得する必要がある場合に役立ちますが、Win32 API を使用してファイルを操作します。  
  
 [!code-sql[FILESTREAM#FS_InsertZero](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertzero)]  
  
### <a name="creating-a-data-file"></a>データ ファイルの作成  
 `INSERT` を使用して、データを含むファイルを作成する方法を次の例に示します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によって、文字列 `Seismic Data` が `varbinary(max)` 値に変換されます。 Windows ファイルが存在しない場合は、FILESTREAM によってそのファイルが作成されます。その後にデータがデータ ファイルに追加されます。  
  
 [!code-sql[FILESTREAM#FS_InsertData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertdata)]  
  
 すべてのデータを `Archive`.`dbo.Records` テーブルから選択すると、次の表に示すような結果になります。 ただし、 `Id` 列に格納される GUID は異なります。  
  
|Id|SerialNumber|[再開]|  
|--------|------------------|------------|  
|`C871B90F-D25E-47B3-A560-7CC0CA405DAC`|`1`|`NULL`|  
|`F8F5C314-0559-4927-8FA9-1535EE0BDF50`|`2`|`0x`|  
|`7F680840-B7A4-45D4-8CD5-527C44D35B3F`|`3`|`0x536569736D69632044617461`|  
  
##  <a name="upd"></a> FILESTREAM データを更新する  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用すると、ファイル システムのファイルのデータを更新できます。ただし、大量のデータをファイルにストリーミングする必要があるときには、この操作は適していません。  
  
 ファイル レコード内の任意のテキストを、 `Xray 1`というテキストに置換する例を次に示します。  
  
 [!code-sql[FILESTREAM#FS_UpdateData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_updatedata)]  
  
##  <a name="del"></a> FILESTREAM データの削除  
 FILESTREAM フィールドを含む行を削除すると、その基となるファイル システム ファイルも削除されます。 行、したがってファイルを削除する唯一の方法は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE ステートメントを使用する方法です。  
  
 行およびそれに関連付けられているファイル システム ファイルを削除する方法を次の例に示します。  
  
 [!code-sql[FILESTREAM#FS_DeleteData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_deletedata)]  
  
 すべてのデータを `dbo.Archive` テーブルから選択すると、その行が削除されます。 関連付けられていたファイルは使用できなくなります。  
  
> [!NOTE]  
>  基になるファイルは、FILESTREAM ガベージ コレクターによって削除されます。  
  
## <a name="see-also"></a>参照  
 [FILESTREAM の有効化と構成](enable-and-configure-filestream.md)   
 [FILESTREAM アプリケーションでのデータベース操作との競合の回避](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
