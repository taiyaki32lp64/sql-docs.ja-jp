---
title: ネイティブ コンパイル アドバイザー | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql13.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bc5a4def5c32ffc39c0df58d5a7927a24c90860d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135551"
---
# <a name="native-compilation-advisor"></a>ネイティブ コンパイル アドバイザー
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  トランザクション パフォーマンス分析レポートでは、データベース内にある解釈されたストアド プロシージャをネイティブ コンパイルを使用するように移植した場合に、どのストアド プロシージャで効果が得られるかを知ることができます。 詳細については、「 [テーブルまたはストアド プロシージャをインメモリ OLTP に移植する必要があるかどうかの確認](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)」を参照してください。  
  
 ネイティブ コンパイルを使用するように移植するストアド プロシージャを特定した後、ネイティブ コンパイル アドバイザー (NCA) を使用して、解釈されたストアド プロシージャをネイティブ コンパイルに移行することができます。 ネイティブ コンパイル ストアド プロシージャの詳細については、「 [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)」をご覧ください。  
  
 特定の解釈されたストアド プロシージャでは、NCA を使用して、ネイティブ モジュールではサポートされないすべての機能を識別できます。 NCA には、回避策またはソリューションを説明するドキュメントのリンクが用意されています。  
  
 移行方法については、「[In-Memory OLTP - Common Workload Patterns and Migration Considerations](https://msdn.microsoft.com/library/dn673538.aspx)」(インメモリ OLTP - 一般的なワークロード パターンと移行に関する考慮事項) を参照してください。  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>ネイティブ コンパイル アドバイザーの使用に関するチュートリアル  
 **オブジェクト エクスプローラー**で、変換するストアド プロシージャを右クリックし、 **[ネイティブ コンパイル アドバイザー]** をクリックします。 これにより、 **[ストアド プロシージャのネイティブ コンパイル アドバイザー]** のようこそページが表示されます。 **[次へ]** をクリックして次に進みます。  
  
### <a name="stored-procedure-validation"></a>[ストアド プロシージャの検証]  
 このページでは、ストアド プロシージャでネイティブ コンパイルと互換性のない構造が使用されているかどうかがレポートされます。 **[次へ]** をクリックすると、詳細を表示できます。 ネイティブ コンパイルと互換性のない構造がある場合は、 **[次へ]** をクリックすると、詳細を表示できます。  
  
### <a name="stored-procedure-validation-result"></a>[ストアド プロシージャの検証結果]  
 ネイティブ コンパイルと互換性のない構造がある場合は、 **[ストアド プロシージャの検証結果]** ページに詳細が表示されます。 レポートを生成 ( **[レポートの生成]** をクリック) し、 **ネイティブ コンパイル アドバイザー**を終了して、ネイティブ コンパイルと互換性があるようにコードを更新できます。  
  
## <a name="code-sample"></a>コード サンプル  
 次のサンプルは、解釈されたストアド プロシージャと、ネイティブ コンパイルに対する *同等の* ストアド プロシージャを示しています。 次のサンプルでは、c:\data というディレクトリがあることを前提にしています。  
  
> [!NOTE]  
>  通常どおり、 **FILEGROUP** 要素と **USE** mydatabase ステートメントは Microsoft SQL Server に適用されますが、Azure SQL Database には適用されません。  
  
```sql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
go  
  
USE Demo;  
go  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
     CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
) WITH ( BUCKET_COUNT = 2097152)  
) WITH ( MEMORY_OPTIMIZED = ON )  
go  
  
-- Interpreted.  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
-- Natively Compiled.  
CREATE PROCEDURE [dbo].[InsertOrderXTP]  
      @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
     (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
     )  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
SELECT * from SalesOrders;  
go  
  
EXECUTE dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1;  
EXECUTE dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2;  
  
SELECT * from SalesOrders;  
```  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP への移行](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)   
 [メモリ最適化テーブルを使用するための要件](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)  
  
  
