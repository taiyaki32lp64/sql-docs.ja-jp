---
title: sp_fulltext_table (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_table_TSQL
- sp_fulltext_table
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_table
ms.assetid: a765f311-07fc-4af3-b74c-e9a027fbecce
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1db3a16b8072df38937bb482ac85a75dec6e83b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124143"
---
# <a name="spfulltexttable-transact-sql"></a>sp_fulltext_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  フルテキスト インデックスに対してテーブルをマークしたりマークします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md)、 [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)、および[DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_table   
   [ @tabname= ] 'qualified_table_name'           
   , [ @action= ] 'action'   
   [   
   , [ @ftcat= ] 'fulltext_catalog_name'           
   , [ @keyname= ] 'unique_index_name'   
   ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'qualified_table_name'` 1 つまたは 2 つの部分のテーブル名です。 テーブルは、現在のデータベース内に存在している必要があります。 *qualified_table_name*は**nvarchar (517)** 、既定値はありません。  
  
`[ @action = ] 'action'` 実行する操作です。 *アクション*は**nvarchar (50)** , で、既定値はありませんはこれらの値のいずれかを指定します。  
  
|[値]|説明|  
|-----------|-----------------|  
|**作成**|によって参照されるテーブルのフルテキスト インデックスのメタデータを作成します。 *qualified_table_name*をこのテーブルのフルテキスト インデックス データに配置することを指定します。 *fulltext_catalog_name*します。 このアクションを使用することも指定*unique_index_name*フルテキスト キー列として。 この一意なインデックスは既に存在していて、テーブル内の列に定義しておく必要があります。<br /><br /> フルテキスト カタログが作成されるまで、このテーブルに対してフルテキスト検索を実行できません。|  
|**Drop**|メタデータのフルテキスト インデックスを削除*qualified_table_name*します。 フルテキスト インデックスがアクティブである場合は自動的に非アクティブ化された削除される前にします。 フルテキスト インデックスを削除する前に、列を削除する必要はありません。|  
|**Activate**|フルテキスト インデックス データの収集機能をアクティブに*qualified_table_name*が非アクティブにした後で、します。 フルテキスト インデックスをアクティブにするには、フルテキスト インデックスの対象となる列が少なくとも 1 つ必要です。<br /><br /> フルテキスト インデックスは、インデックス作成用の最初の列が追加されるとすぐに自動的にアクティブになり、作成を開始できるようになります。 インデックスから最後の列を削除すると、インデックスは非アクティブになります。 変更の追跡がオンの場合、非アクティブなインデックスをアクティブにすると、新しく作成が開始されます。<br /><br /> このフルテキスト インデックスでは、実際には設定されませんから行をファイル システムで、フルテキスト カタログにテーブルを単に登録*qualified_table_name* [次へ] のフルテキスト インデックスで取得することができますカタログの作成。|  
|**非アクティブ化します。**|フルテキスト インデックスを非アクティブ化*qualified_table_name*のフルテキスト インデックス データを収集できなくするため、 *qualified_table_name*します。 フルテキスト インデックス メタデータはそのまま残り、テーブルは再びアクティブにできます。<br /><br /> 変更の追跡がオンになっている場合、アクティブなインデックスを非アクティブにすると、インデックス作成は停止します。つまり、実行中の作成操作は停止し、インデックスは変更されなくなります。|  
|**start_change_tracking**|フルテキスト インデックスの増分作成を開始します。 テーブルが timestamp 型でない場合は、フルテキスト インデックスの完全作成を開始します。 テーブルに変更の追跡を開始します。<br /><br /> フルテキスト変更の追跡が型のフルテキスト インデックス付き列で実行された WRITETEXT または UPDATETEXT の操作を追跡しない**イメージ**、**テキスト**、または**ntext**します。|  
|**stop_change_tracking**|テーブルに変更の追跡を停止します。|  
|**update_index**|現在、フルテキスト インデックスに追跡された変更のセットを伝達します。|  
|**start_background_updateindex**|変更の追跡中に発生した変更を、発生した時点でフルテキスト インデックスに反映します。|  
|**stop_background_updateindex**|発生すると、フルテキスト インデックスに追跡された変更の伝達を停止します。|  
|**start_full**|テーブルのフルテキスト インデックスの完全作成を開始します。|  
|**start_incremental**|テーブルのフルテキスト インデックスの増分作成を開始します。|  
|**[停止]**|フルまたは増分作成を停止します。|  
  
`[ @ftcat = ] 'fulltext_catalog_name'` 有効な既存のフルテキスト カタログの名前を指定、**作成**アクション。 その他のすべてのアクションでは、このパラメーターは NULL にする必要があります。 *fulltext_catalog_name*は**sysname**、既定値は NULL です。  
  
`[ @keyname = ] 'unique_index_name'` 有効な単一キー列の一意の非 null インデックスが*qualified_table_name*の**作成**アクション。 その他のすべてのアクションでは、このパラメーターは NULL にする必要があります。 *unique_index_name*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 特定のテーブルのフルテキスト インデックスが非アクティブ化した後、既存のフルテキスト インデックスはそのまま残りますまで、[次へ] の完全作成ただし、このインデックスが使用されないため、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]非アクティブ テーブルに対してクエリをブロックします。  
  
 テーブルが再アクティブ化、インデックスが再作成しない場合は、古いインデックスは、に対するクエリは使用できますが、有効にしない新しいフルテキスト列。 削除された列のデータは、すべてのフルテキスト列検索を指定するクエリで照合されます。  
  
 テーブルの後が定義されて、フルテキスト インデックス作成の場合、フルテキスト一意のキー列のデータ型をその列のデータ型を変更するか、1 つの列から完全な再作成しなくても、別に、フルテキストの一意のキーを変更するか、別の切り替え後続のクエリとエラー メッセージを取得中にエラーが発生する可能性があります。"型への変換*data_type*キーの値をフルテキスト検索に失敗しました*key_value*"。 これを回避するを使用してこのテーブルのフルテキスト定義を削除、**ドロップ**のアクション**sp_fulltext_table**再定義**sp_fulltext_table**と**sp_fulltext_column**します。  
  
 フルテキスト キー列は、900 バイトに定義された以下にする必要があります。 パフォーマンス上の理由から、キー列のサイズはできる限り小さくすることをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロール、 **db_owner**と**db_ddladmin**参照、フルテキスト カタログは、アクセス許可を持つデータベース ロール、またはユーザーを修正しました実行**sp_fulltext_table**します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-enabling-a-table-for-full-text-indexing"></a>A. フルテキスト インデックスに対してテーブルを有効にする  
 次の例では、フルテキスト インデックスのメタデータを`Document`のテーブル、`AdventureWorks`データベース。 `Cat_Desc` フルテキスト カタログです。 `PK_Document_DocumentID` は `Document` の一意な単一列のインデックスです。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'create', 'Cat_Desc', 'PK_Document_DocumentID';  
--Add some columns  
EXEC sp_fulltext_column 'Production.Document','DocumentSummary','add';  
-- Activate the full-text index  
EXEC sp_fulltext_table 'Production.Document','activate';  
GO  
```  
  
### <a name="b-activating-and-propagating-track-changes"></a>B. 変更の追跡をアクティブにして変更を反映する  
 次の例では、変更の追跡をアクティブにし、発生した変更を直ちにフルテキスト インデックスに反映します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'Start_change_tracking';  
EXEC sp_fulltext_table 'Production.Document', 'Start_background_updateindex';  
GO  
```  
  
### <a name="c-removing-a-full-text-index"></a>C. フルテキスト インデックスを削除します。  
 次の例では、`Document` データベースの `AdventureWorks` テーブルに対する、フルテキスト インデックス メタデータを削除します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_table 'Production.Document', 'drop';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [sp_helpindex &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [フルテキスト検索およびセマンティック検索ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
