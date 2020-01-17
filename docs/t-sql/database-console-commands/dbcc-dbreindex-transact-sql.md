---
title: DBCC DBREINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC DBREINDEX
- DBREINDEX_TSQL
- DBREINDEX
- DBCC_DBREINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- index rebuilding [SQL Server]
- rebuilding indexes
- dynamic index rebuilding [SQL Server]
- DBCC DBREINDEX statement
ms.assetid: 6e929d09-ccb5-4855-a6af-b616022bc8f6
author: pmasl
ms.author: umajay
ms.openlocfilehash: 5aa089ac3c8de549e0c2ec33fd413c9cafba24dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101996"
---
# <a name="dbcc-dbreindex-transact-sql"></a>DBCC DBREINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
指定されたデータベース内のテーブルの 1 つ以上のインデックスを再構築します。
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) を使用してください。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC DBREINDEX   
(   
    table_name   
    [ , index_name [ , fillfactor ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>引数  
 *table_name*  
 再構築するよう指定したインデックスが含まれているテーブルの名前です。 テーブル名は[識別子](../../relational-databases/databases/database-identifiers.md)*の規則に従っている必要があります。*  
  
 *index_name*  
 再構築するインデックスの名前です。 インデックス名は、識別子の規則に従っている必要があります。 *index_name* が指定されている場合、*table_name* を指定する必要があります。 *index_name* を指定しない場合、または " " である場合は、テーブルのすべてのインデックスが再構築されます。  
  
 *fillfactor*  
 インデックスの作成時または再構築時に、データを格納する各インデックス ページの領域の割合を指定します。 *fillfactor* はインデックス作成時の FILL FACTOR を上書きし、そのインデックス、およびクラスター化インデックスが再構築されたために再構築される他の非クラスター化インデックスに対する新しい既定値となります。  
 *fillfactor* が 0 の場合、DBCC DBREINDEX はインデックスに対して最後に指定された FILL FACTOR 値を使用します。 この値は、**sys.indexes** カタログ ビューに格納されます。   
 *fillfactor* が指定されている場合、*table_name* と *index_name* を指定する必要があります。 *fillfactor* が指定されていない場合は、既定の FILL FACTOR 値 100 が使用されます。 詳細については、「 [インデックスの FILL FACTOR の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)」を参照してください。  
  
 WITH NO_INFOMSGS  
 重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks  
DBCC DBREINDEX では、テーブルの 1 つのインデックス、またはテーブルに対して定義されているすべてのインデックスを再構築します。 インデックスを動的に再構築できれば、PRIMARY KEY 制約または UNIQUE 制約を削除して再作成しなくても、それらの制約を強制しているインデックスを再構築できます。 したがって、テーブルの構造やその制約がわからない場合でも、インデックスを再構築することができます。 インデックスの再構築は、テーブルにデータを一括コピーした後に実行できます。

DBCC DBREINDEX では、1 つのステートメントでテーブルのすべてのインデックスを再構築できます。 これは複数の DROP INDEX ステートメントと CREATE INDEX ステートメントをコーディングするより簡単です。 DBCC DBREINDEX は、1 つのステートメントで作業を行うため最初からアトミックです。これに対して、個々の DROP INDEX ステートメントと CREATE INDEX ステートメントをアトミックにするためには、トランザクションに含める必要があります。 また、DBCC DBREINDEX を使用した方が、個々の DROP INDEX ステートメントと CREATE INDEX ステートメントを使用するよりもさらに最適化されます。

DBCC INDEXDEFRAG や、REORGANIZE オプションを使用した ALTER INDEX とは異なり、DBCC DBREINDEX はオフライン操作です。 非クラスター化インデックスを再構築する場合、操作中は、該当のテーブルに対して共有ロックが保持されます。 これにより、テーブルが変更されなくなります。 クラスター化インデックスを再構築する場合は、排他テーブル ロックが保持されます。 これにより、テーブルに一切アクセスできなくなり、実質的にテーブルはオフラインになります。 インデックスの再構築をオンラインで実行したり、インデックスの再構築操作中に並列処理の次数を制御したりするには、ALTER INDEX REBUILD ステートメントに ONLINE オプションを付けて使用してください。

インデックスを再構築または再構成する方法の選択の詳細については、「[インデックスの再構成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。
  
## <a name="restrictions"></a>制限  
DBCC DBREINDEX は、次のオブジェクトに対して使用できません。
-   システム テーブル  
-   空間インデックス  
-   xVelocity メモリ最適化列ストア インデックス  
  
## <a name="result-sets"></a>結果セット  
NO_INFOMSGS を指定しない限り (テーブル名の指定は必要)、DBCC DBREINDEX は常に以下を返します。
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
呼び出し元はテーブルまたはインデックス付きビューを所有しているか、固定サーバー ロール **sysadmin**、固定データベース ロール **db_owner**、または固定データベース ロール **db_ddladmin** のメンバーである必要があります。
  
## <a name="examples"></a>使用例  
### <a name="a-rebuilding-an-index"></a>A. インデックスを再構築する  
次の例では、`AdventureWorks` データベースの `Employee` テーブルで、`Employee_EmployeeID` クラスター化インデックスを FILL FACTOR `80` で再構築します。
  
```sql  
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', PK_Employee_BusinessEntityID,80);  
GO  
```  
  
### <a name="b-rebuilding-all-indexes"></a>B. すべてのインデックスを再構築する  
次の例では、`Employee` の `AdventureWorks` テーブルのすべてのインデックスを、FILL FACTOR 値 `70` で再構築します。
  
```sql
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', ' ', 70);  
GO  
```  
  
## <a name="see-also"></a>参照  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

