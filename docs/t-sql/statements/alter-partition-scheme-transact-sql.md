---
title: ALTER PARTITION SCHEME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 593c2d8bf9cff3e10aaafc339aa82ef16c4bc09f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071237"
---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  パーティション構成にファイル グループを追加したり、パーティション構成の NEXT USED ファイル グループの指定を変更します。 

>[!NOTE]
>Azure SQL Database では、プライマリ ファイル グループのみがサポートされます。  
  
 ![記事のリンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事のリンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *partition_scheme_name*  
 変更するパーティション構成の名前です。  
  
 *filegroup_name*  
 NEXT USED としてパーティション構成によってマークされるファイルグループを指定します。 これは、このファイル グループに、[ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md) ステートメントによって作成される新しいパーティションが受け入れられることを表します。  
  
 パーティション構成では、1 つのファイル グループのみを NEXT USED として指定できます。 これには空でないファイル グループを指定できます。 *filegroup_name* を指定した場合に、現在 NEXT USED とマークされているファイル グループがなければ、*filegroup_name* が NEXT USED としてマークされます。 *filegroup_name* を指定した場合に、NEXT USED プロパティの指定されているファイル グループが既にあれば、NEXT USED プロパティは既存のファイル グループから *filegroup_name* に移動します。  
  
 *filegroup_name* を指定しなかった場合に、NEXT USED プロパティの指定されているファイル グループが既にあれば、そのファイル グループの NEXT USED 指定は解除され、*partition_scheme_name* には、NEXT USED の指定されたファイル グループが存在しない状態になります。  
  
 *filegroup_name* を指定しなかった場合に、NEXT USED とマークされているファイル グループがなければ、ALTER PARTITION SCHEME から警告が返されます。  
  
## <a name="remarks"></a>Remarks  
 ALTER PARTITION SCHEME の対象となるファイル グループは、オンラインになっている必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 次の権限を使って ALTER PARTITION SCHEME を実行できます。  
  
-   ALTER ANY DATASPACE 権限。 この権限は、既定では **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_ddladmin** 固定データベース ロールのメンバーに与えられています。  
  
-   パーティション構成が作成されたデータベースに対する CONTROL または ALTER 権限。  
  
-   パーティション構成が作成されたデータベースのサーバーに対する CONTROL SERVER または ALTER ANY DATABASE 権限。  
  
## <a name="examples"></a>使用例  
 次の例では、パーティション構成 `MyRangePS1` およびファイル グループ `test5fg` が現在のデータベースに存在することを前提としています。  
  
```  
ALTER PARTITION SCHEME MyRangePS1  
NEXT USED test5fg;  
```  
  
 ファイル グループ `test5fg` には、ALTER PARTITION FUNCTION ステートメントの結果として作成された、パーティション テーブルまたはインデックスの追加パーティションが受け入れられます。  
  
## <a name="see-also"></a>参照  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
