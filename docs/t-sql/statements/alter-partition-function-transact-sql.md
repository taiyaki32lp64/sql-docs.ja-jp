---
title: ALTER PARTITION FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION FUNCTION
- ALTER_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- splitting partitions [SQL Server]
- partitioned tables [SQL Server], splitting
- ALTER PARTITION FUNCTION statement
- merging partitions [SQL Server]
- partitioned indexes [SQL Server], merging
- partitioned indexes [SQL Server], splitting
- modifying partition functions
- partition functions [SQL Server], modifying
- partitioned tables [SQL Server], merging
ms.assetid: 70866dac-0a8f-4235-8108-51547949ada4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c2418bedb172464002fd640a50c8b57f3daca712
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071253"
---
# <a name="alter-partition-function-transact-sql"></a>ALTER PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

境界値の分割または結合によって、パーティション関数を変更します。 ALTER PARTITION FUNCTION ステートメントを実行すると、1 つのテーブル パーティションやパーティション関数を使用するインデックスを、2 つのパーティションに分割できます。 また、そのステートメントは 2 つのパーティションを 1 つのパーティションにマージすることもできます。  
  
> [!CAUTION]  
>  複数のテーブルやインデックスで同じパーティション関数を使用できます。 ALTER PARTITION FUNCTION では、1 回のトランザクションでこれらすべてを操作できます。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER PARTITION FUNCTION partition_function_name()  
{   
    SPLIT RANGE ( boundary_value )  
  | MERGE RANGE ( boundary_value )   
} [ ; ]  
```  
  
## <a name="arguments"></a>引数  
*partition_function_name*  
変更するパーティション関数の名前です。  
  
SPLIT RANGE ( *boundary_value* )  
1 つのパーティションをパーティション関数に追加します。 *boundary_value* は、新しいパーティションの範囲を決定します。boundary_value は、そのパーティション関数の既存の境界範囲と異なるようにする必要があります。 *boundary_value* に基づき、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって既存の範囲が 2 つに分割されます。 これらの 2 つの範囲のうち、新しい *boundary_value* を持つパーティションが新しいパーティションです。  
  
ファイル グループはオンラインに存在する必要があります。 また、新しいパーティションを保持するために、そのパーティション関数を NEXT USED として使用するパーティション構成が、そのファイルグループをマークする必要があります。 CREATE PARTITION SCHEME ステートメントはファイルグループをパーティションに割り当てます。 CREATE PARTITION FUNCTION ステートメントは、ファイルグループよりも少ない数のパーティションを作成し、それらを保持します。 CREATE PARTITION SCHEME ステートメントは、必要以上に多くのファイルグループを備えておくことがあります。 それが発生した場合、最終的に未割り当てのファイルグループが作成されることがあります。 また、パーティション構成はそのファイルグループのいずれか 1 つを NEXT USED としてマークします。 このファイル グループが新しいパーティションを保持します。 パーティション構成が NEXT USED としてマークしたファイルグループがない場合は、ALTER PARTITION SCHEME ステートメントを使用する必要があります。 

ALTER PARTITION SCHEME ステートメントでは、新しいパーティションを保持するために、ファイルグループを追加するか、既存のファイルグループを選択できます。 既にパーティションを保持しているファイルグループを割り当てて、追加のパーティションを保持するように指定できます。 1 つのパーティション関数は複数のパーティション構成に参加させることができます。 この理由から、パーティションを追加する、そのパーティション関数を使用するすべてのパーティション構成に、NEXT USED ファイルグループが必要です。 ない場合、パーティション構成に NEXT USED ファイルグループが存在しないというエラーが表示され、ALTER PARTITION FUNCTION ステートメントが失敗します。  
  
すべてのパーティションを同じファイル グループ内に作成した場合、最初に、そのグループが自動的に NEXT USED ファイル グループに割り当てられます。 ただし、分割操作が実行された後は、選択された NEXT USED ファイルグループはなくなります。 ALTER PARTITION SCHEME を使用してファイルグループを NEXT USED ファイルグループとして明示的に割り当てないと、その後の分割操作が失敗します。  
  
> [!NOTE]  
>  列ストア インデックスに関する制限:テーブルに列ストア インデックスが存在するときは、空のパーティションのみを分割できます。 この操作を実行する前に、列ストア インデックスを削除するか無効にする必要があります。  
  
MERGE [ RANGE ( *boundary_value*) ]  
パーティションを削除し、そのパーティションに存在する任意の値を残りの 1 つのパーティションにマージします。 RANGE (*boundary_value*) は、既存の境界値である必要があります。ここに、削除したパーティションの値がマージされます。 この引数は、最初に *boundary_value* を保持していたファイルグループを、残りのパーティションがそれを使用しない場合、または NEXT USED プロパティでマークしない場合を除き、パーティション構成から削除します。 マージされたパーティションは、最初に *boundary_value* を保持していなかったファイル グループに存在します。 *boundary_value* は定数式であり、変数 (ユーザー定義型変数を含む) または関数 (ユーザー定義関数を含む) を参照できます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 式は参照できません。 *boundary_value* は、対応するパーティション分割列のデータ型と一致するか、パーティション分割列のデータ型に暗黙的に変換される必要があります。 また、明示的な変換中に、値のサイズおよびスケールが対応する *input_parameter_type* のものと一致しない方法で *boundary_value* を切り詰めることはできません。  
  
> [!NOTE]  
>  列ストア インデックスに関する制限:列ストア インデックスを含む 2 つの空でないパーティションをマージすることはできません。 この操作を実行する前に、列ストア インデックスを削除するか無効にする必要があります  
  
## <a name="best-practices"></a>ベスト プラクティス  
空のパーティションは、常にパーティションの範囲の両端に保持します。 パーティションの分割やパーティションのマージによりデータ移動が発生しないように、パーティションを両端に保持します。 パーティションの分割は最初に発生し、パーティションのマージは最後に発生します。 設定されたパーティションが分割またはマージされないようにします。 データが入力されているパーティションの分割やマージは効率的でなくなることがあります。 非効率になる理由は、分割やマージによりログの生成が最大で 4 倍になり、大量のロックが発生する場合があるためです。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
ALTER PARTITION FUNCTION は、1 回のアトミックな操作で、その関数を使用するすべてのテーブルおよびインデックスのパーティションを分割し直します。 しかし、この操作はオフラインで実行され、分割し直すエクステントによってはリソースを大きく消費する場合があります。  
  
ALTER PARTITION FUNCTION は、1 つのパーティションを 2 つに分割する、または 2 つのパーティションを 1 つにマージするときにのみ使用します。 他のパーティション分割方法でテーブルを変更する (たとえば、10 のパーティションを 5 つにする) には、次のいずれかを実行します。 システムの構成に応じて、これらの方法のリソース消費量は異なる場合があります。  
  
-   必要なパーティション関数を使用して新しいパーティション テーブルを作成します。 その後、INSERT INTO...SELECT FROM ステートメントを使用して、古いテーブルから新しいテーブルにデータを挿入します。  
  
-   パーティション分割されたクラスター化インデックスを、ヒープ上に作成します。  
  
    > [!NOTE]  
    >  パーティション分割されたクラスター化インデックスを削除すると、パーティション分割されたヒープが生成されます。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] の CREATE INDEX ステートメントと DROP EXISTING = ON 句を使用して、既存のパーティション インデックスを削除および再構築します。  
  
-   一連の ALTER PARTITION FUNCTION ステートメントを実行します。  
  
ALTER PARTITION FUNCTION の影響を受けるすべてのファイル グループは、オンラインである必要があります。  
  
ALTER PARTITION FUNCTION は、そのパーティション関数を使用するテーブル上に無効化されたクラスター化インデックスが存在すると失敗します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、パーティション関数の変更に関するレプリケーションはサポートされていません。 パブリケーション データベース内のパーティション関数への変更は、手動でサブスクリプション データベースに適用する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
次の権限のいずれかを使用すると、ALTER PARTITION FUNCTION を実行できます。  
  
-   ALTER ANY DATASPACE 権限。 この権限は、既定では **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_ddladmin** 固定データベース ロールのメンバーに与えられています。  
  
-   パーティション関数が作成されたデータベースでの CONTROL または ALTER 権限。  
  
-   パーティション関数が作成されたデータベースのサーバーでの CONTROL SERVER または ALTER ANY DATABASE 権限。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-splitting-a-partition-of-a-partitioned-table-or-index-into-two-partitions"></a>A. パーティション テーブルまたはパーティション インデックスの 1 つのパーティションを 2 つのパーティションに分割する  
次の例では、テーブルまたはインデックスを 4 つのパーティションに分割するパーティション関数を作成します。 `ALTER PARTITION FUNCTION` でこれらのパーティションのうちの 1 つを 2 つに分割して、合計 5 つのパーティションを作成します。  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Split the partition between boundary_values 100 and 1000  
--to create two partitions between boundary_values 100 and 500  
--and between boundary_values 500 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
SPLIT RANGE (500);  
```  
  
### <a name="b-merging-two-partitions-of-a-partitioned-table-into-one-partition"></a>B. パーティション テーブルの 2 つのパーティションを 1 つのパーティションにマージする  
次の例では、上記と同じパーティション関数を作成し、次にこれらのパーティションのうちの 2 つを 1 つにマージして、合計 3 つのパーティションにします。  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Merge the partitions between boundary_values 1 and 100  
--and between boundary_values 100 and 1000 to create one partition  
--between boundary_values 1 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
MERGE RANGE (100);  
```  
  
## <a name="see-also"></a>参照  
[パーティション テーブルとパーティション インデックス](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
[CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
[DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
[CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
[ALTER PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
[DROP PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
[sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
[sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md) [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
[sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
[sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
