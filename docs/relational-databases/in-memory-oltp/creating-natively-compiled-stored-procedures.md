---
title: ネイティブ コンパイル ストアド プロシージャの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fb7b029527eec87c87b9b21b4da8aff5e289424e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032024"
---
# <a name="creating-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

ネイティブ コンパイル ストアド プロシージャには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のプログラミングとクエリのセキュリティ構成が完全には実装されていません。 ネイティブ コンパイル ストアド プロシージャ内部で使用できない特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] 構造が存在します。 詳細については、「 [ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」を参照してください。  
  
ただし、ネイティブ コンパイル ストアド プロシージャに対してのみサポートされる [!INCLUDE[tsql](../../includes/tsql-md.md)] 機能がいくつかあります。  
  
-   ATOMIC ブロック。 詳細については、「 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)」を参照してください。  
  
-   パラメーターおよび変数に対する **NOT NULL** 制約。 **NULL** として宣言されているパラメーターまたは変数に **NOT NULL**値を割り当てることはできません。 詳細については、「[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)」を参照してください。  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **not null**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **not null = "Hello"** ; -- *(値に初期化する必要があります。)*  
  
    -   SET @myVarchar **= null**; -- *(コンパイルされますが実行時に失敗します。)*  
  
-   ネイティブ コンパイル ストアド プロシージャのスキーマ バインド。  
  
ネイティブ コンパイル ストアド プロシージャは、[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md) を使用して作成します。 次の例は、メモリ最適化テーブルと、このテーブルに行を挿入するために使用されるネイティブ コンパイル ストアド プロシージャを示します。  
  
```sql  
CREATE TABLE [dbo].[T2] (  
  [c1] [int] NOT NULL, 
  [c2] [datetime] NOT NULL,
  [c3] nvarchar(5) NOT NULL, 
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_2] (@c1 int, @c3 nvarchar(5)) 
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
  DECLARE @c2 datetime = GETDATE();  
  INSERT INTO [dbo].[T2] (c1, c2, c3) values (@c1, @c2, @c3);  
END  
GO  
```  
 
コード サンプルの **NATIVE_COMPILATION** は、この [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャがネイティブ コンパイル ストアド プロシージャであることを示しています。 以下のオプションは必須です。  
  
|オプション|[説明]|  
|------------|-----------------|  
|**SCHEMABINDING**|ネイティブ コンパイル ストアド プロシージャは、参照するオブジェクトのスキーマにバインドされている必要があります。 これは、プロシージャによるテーブル参照が必要であることを意味しています。 プロシージャ内で参照されているテーブルにはスキーマ名が含まれている必要があり、クエリでワイルドカード (\*) は使用できません ( `SELECT * from...`はありません)。 このバージョンの**では、ネイティブ コンパイル ストアド プロシージャに対してのみ** SCHEMABINDING [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]がサポートされます。|  
|**BEGIN ATOMIC**|ネイティブ コンパイル ストアド プロシージャの本体は、厳密に 1 つの ATOMIC ブロックで構成されている必要があります。 ATOMIC ブロックでは、ストアド プロシージャのアトミック実行が保証されます。 プロシージャをアクティブなトランザクションのコンテキストの外部で呼び出した場合、新しいトランザクションが開始され、ATOMIC ブロックの末尾でコミットされます。 ネイティブ コンパイル ストアド プロシージャの ATOMIC ブロックには、次の 2 つの必須オプションがあります。<br /><br /> **TRANSACTION ISOLATION LEVEL**。 サポートされる分離レベルについては、「 [メモリ最適化テーブルのトランザクション分離](https://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) 」を参照してください。<br /><br /> **LANGUAGE**。 ストアド プロシージャの言語は、使用可能な言語または言語の別名の 1 つに設定されている必要があります。|  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
