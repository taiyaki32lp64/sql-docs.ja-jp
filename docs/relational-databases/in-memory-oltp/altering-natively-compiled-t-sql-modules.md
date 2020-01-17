---
title: ネイティブ コンパイル T-SQL モジュールの変更 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6979d05d29b151a34edfe1c220c9d9a4d3046359
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983011"
---
# <a name="altering-natively-compiled-t-sql-modules"></a>Altering Natively Compiled T-SQL Modules
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、`ALTER` ステートメントを使用して、ネイティブ コンパイル ストアド プロシージャおよびスカラー UDF やトリガーなどの他のネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールに対して、`ALTER` 操作を実行できます。  
  
ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールに対して `ALTER` を実行すると、モジュールは新しい定義を使用して再コンパイルされます。 再コンパイルの進行中、古いバージョンのモジュールは引き続き実行に使用できます。 コンパイルが完了すると、モジュールの実行は削除され、新しいバージョンのモジュールがインストールされます。 ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールを変更する場合、次のオプションを変更できます。  
  
-   パラメーター  
-   EXECUTE AS  
-   TRANSACTION ISOLATION LEVEL  
-   LANGUAGE  
-   DATEFIRST  
-   DATEFORMAT  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
> ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールは、非ネイティブ コンパイル モジュールに変換できません。 非ネイティブ コンパイル T-SQL モジュールは、ネイティブ コンパイル モジュールに変換できません。  
  
`ALTER PROCEDURE` の機能と構文の詳細については、「[ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)」を参照してください。  
  
ネイティブ コンパイル [!INCLUDE[tsql](../../includes/tsql-md.md)] モジュールに対して [sp_recompile](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) を実行できます。これにより、モジュールは次の実行時に再コンパイルされます。  
  
## <a name="example"></a>例  
次の例では、メモリ最適化テーブル (T1) と、T1 のすべての列を選択するネイティブ コンパイル ストアド プロシージャ (usp_1) が作成されます。 その後、usp_1 は、`EXECUTE AS` 句を削除し、`LANGUAGE` を変更して、T1 からただ 1 つの列 (C1) を選択するように変更されます。  
  
```sql  
CREATE TABLE [dbo].[T1] (  
  [c1] [int] NOT NULL,  
  [c2] [float] NOT NULL,  
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
   SELECT c1, c2 FROM dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
   SELECT c1 FROM dbo.T1  
END  
GO    
```   
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)    
