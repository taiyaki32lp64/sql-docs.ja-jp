---
title: sys.dm_exec_describe_first_result_set (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_describe_first_result_set
- sys.dm_exec_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_describe_first_result_set catalog view
ms.assetid: 6ea88346-0bdb-4f0e-9f1f-4d85e3487d23
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 523a94718f123fab9d501de9497ca5ecc2b09c95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097812"
---
# <a name="sysdm_exec_describe_first_result_set-transact-sql"></a>sys.dm_exec_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  この動的管理関数には、[!INCLUDE[tsql](../../includes/tsql-md.md)]をパラメーターとしてステートメントと最初の結果、ステートメントのセットのメタデータについて説明します。  
  
 **sys.dm_exec_describe_first_result_set**が、同じ結果セットの定義[sys.dm_exec_describe_first_result_set_for_object &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)と似ています[sp _describe_first_result_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)します。  
  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_exec_describe_first_result_set(@tsql, @params, @include_browse_information)  
```  
  
## <a name="arguments"></a>引数  
 *\@tsql*  
 1 つ以上の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントです。 *Transact SQL_batch*あります**nvarchar (***n***)** または**nvarchar (max)** します。  
  
 *\@params*  
 \@params パラメーターの宣言文字列の提供、[!INCLUDE[tsql](../../includes/tsql-md.md)]バッチ、sp_executesql と同様にします。 パラメーターがあります**nvarchar (n)** または**nvarchar (max)** します。  
  
 1 つの文字列に埋め込まれたすべてのパラメーターの定義を含む、 [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*します。 この文字列は Unicode 定数または Unicode 変数にする必要があります。 各パラメーター定義は、パラメーター名とデータ型で構成されます。 *n*は追加のパラメーター定義を示すプレース ホルダーです。 Stmt に指定する各パラメーターを定義する必要があります\@params します。 場合、[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントまたはステートメント内のバッチは、パラメーターを含まない\@params は必要ありません。 NULL は、このパラメーターの既定値です。  
  
 *\@include_browse_information*  
 1 に設定すると、各クエリは FOR BROWSE オプションが指定されているように分析されます。 追加のキー列とソース テーブル情報が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
 この共通メタデータが結果セットとして返されます。 結果のメタデータの各列に対して、列の種類と NULL 許可属性が次の表に示す形式で 1 行に記述されます。 最初のステートメントは、各コントロールのパスが存在しない場合は、0 行を含む結果セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit**|列が結果セットで実際に表示されていない余分な列参照および情報提供のために追加したことを指定します。|  
|**column_ordinal**|**int**|結果セット内の列の位置を示す序数を格納します。 最初の列の位置は 1 として指定されます。|  
|**name**|**sysname**|列の名前を確認できる場合は、その名前を格納します。 確認できない場合は、NULL が格納されます。|  
|**is_nullable**|**bit**|次の値を格納します。<br /><br /> 列が NULL を許容する場合は 1。<br /><br /> 列 が NULL を許容しない場合は 0。<br /><br /> 列が NULL を許容することを確認できない場合は 1。|  
|**system_type_id**|**int**|Sys.types で指定された列のデータ型の system_type_id を格納します。 CLR 型の場合は、system_type_name 列が NULL を返しても、この列は値 240 を返します。|  
|**system_type_name**|**nvarchar (256)**|列のデータ型に指定されている名前と引数 (長さ、有効桁数、小数点以下桁数など) を格納します。<br /><br /> データ型がユーザー定義の別名型の場合は、基になるシステム型がここで指定されます。<br /><br /> データ型が CLR ユーザー定義型の場合は、この列には NULL が返されます。|  
|**max_length**|**smallint**|列の最大長 (バイト単位) です。<br /><br /> -1 = 列のデータ型は**varchar (max)** 、 **nvarchar (max)** 、 **varbinary (max)** 、または**xml**します。<br /><br /> **テキスト**、列、 **max_length**値は 16 かによって設定された値になります**sp_tableoption 'text in row'** します。|  
|**precision**|**tinyint**|数値ベースの場合は、列の有効桁数です。 それ以外の場合 0 を返します。|  
|**scale**|**tinyint**|数値ベースの場合は、列の小数点以下桁数です。 それ以外の場合 0 を返します。|  
|**collation_name**|**sysname**|文字ベースの場合は、列の照合順序の名前です。 それ以外の場合、NULL を返します。|  
|**user_type_id**|**int**|CLR 型と別名型の場合、sys.types で指定された列のデータ型の user_type_id を格納します。 それ以外の場合は NULL です。|  
|**user_type_database**|**sysname**|CLR 型と別名型の場合、その型が定義されたデータベースの名前を格納します。 それ以外の場合は NULL です。|  
|**user_type_schema**|**sysname**|CLR 型と別名型の場合、その型が定義されたスキーマの名前を格納します。 それ以外の場合は NULL です。|  
|**user_type_name**|**sysname**|CLR 型と別名型の場合、その型の名前を格納します。 それ以外の場合は NULL です。|  
|**assembly_qualified_type_name**|**nvarchar (4000)**|CLR 型の場合、その型を定義するアセンブリの名前とクラスを返します。 それ以外の場合は NULL です。|  
|**xml_collection_id**|**int**|sys.columns で指定された列のデータ型の xml_collection_id を格納します。 返される型は、XML スキーマ コレクションに関連付けられていない場合、この列は NULL を返します。|  
|**xml_collection_database**|**sysname**|この型に関連付けられている XML スキーマ コレクションが定義されているデータベースを格納します。 返される型は、XML スキーマ コレクションに関連付けられていない場合、この列は NULL を返します。|  
|**xml_collection_schema**|**sysname**|この型に関連付けられている XML スキーマ コレクションが定義されているスキーマを格納します。 返される型は、XML スキーマ コレクションに関連付けられていない場合、この列は NULL を返します。|  
|**xml_collection_name**|**sysname**|この型に関連付けられている XML スキーマ コレクションの名前を格納します。 返される型は、XML スキーマ コレクションに関連付けられていない場合、この列は NULL を返します。|  
|**is_xml_document**|**bit**|返されたデータ型が XML で、その型が XML フラグメントではなく完全な XML ドキュメント (ルート ノードを含む) であると保証される場合、1 を返します。 それ以外の場合 0 を返します。|  
|**is_case_sensitive**|**bit**|この列が、大文字と小文字を区別する文字列型の場合、1 を返します。 それ以外の場合は 0 を返します。|  
|**is_fixed_length_clr_type**|**bit**|この列が固定長の CLR 型の場合、1 を返します。 それ以外の場合は 0 を返します。|  
|**source_server**|**sysname**|(リモート サーバーから発生する場合) 元のサーバーの名前です。 Sys.servers に表示される、名前が与えられます。 この列がローカル サーバー上で発生した場合、または元のサーバーを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_database**|**sysname**|この結果内の列によって返された元のデータベースの名前です。 データベースを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_schema**|**sysname**|この結果内の列によって返された元のスキーマの名前です。 スキーマを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_table**|**sysname**|この結果内の列によって返された元のテーブルの名前です。 テーブルを特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**source_column**|**sysname**|結果列から返された元の列の名前です。 列を特定できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**is_identity_column**|**bit**|この列が ID 列の場合は 1、それ以外の場合は 0 を返します。 ID 列であることを確認できない場合は NULL を返します。|  
|**is_part_of_unique_key**|**bit**|ない場合で、列が一意インデックス (一意、主な制約を含む) と 0 の一部である場合は、1 を返します。 一意インデックスの一部であることを確認できない場合は NULL を返します。 参照情報が要求された場合にのみ設定されます。|  
|**is_updateable**|**bit**|この列が更新可能である場合は 1、それ以外の場合は 0 を返します。 更新可能であることを確認できない場合は NULL を返します。|  
|**is_computed_column**|**bit**|この列が計算列の場合は 1、それ以外の場合は 0 を返します。 計算列であることを確認できない場合は NULL を返します。|  
|**is_sparse_column_set**|**bit**|この列がスパース列の場合は 1、それ以外の場合は 0 を返します。 スパース列セットの一部であることを確認できない場合は NULL を返します。|  
|**ordinal_in_order_by_list**|**smallint**|このコラムの ihe 位置は、ORDER BY リスト内です。 列が ORDER BY リストに表示されない場合、または ORDER BY リストを一意に特定できない場合は、NULL を返します。|  
|**order_by_list_length**|**smallint**|ORDER BY リストの長さ。 ORDER BY リストが存在しない場合、または ORDER BY リストを一意に特定できない場合は、NULL が返されます。 この値は、sp_describe_first_result_set によって返されるすべての行に対して同じであることに注意してください。|  
|**order_by_is_descending**|**smallint NULL**|Ordinal_in_order_by_list が NULL でない場合、 **order_by_is_descending**列は、この列の ORDER BY 句の方向を報告します。 それ以外の場合は、NULL が報告されます。|  
|**error_number**|**int**|関数によって返されるエラー番号が格納されます。 エラーが発生しなかった場合は、NULL が格納されます。|  
|**error_severity**|**int**|関数によって返される重大度が格納されます。 エラーが発生しなかった場合は、NULL が格納されます。|  
|**error_state**|**int**|関数によって返される 状態メッセージが格納されます。 エラーが発生しなかった場合は、NULL が格納されます。|  
|**error_message**|**nvarchar(4096)**|関数によって返されるメッセージが格納されます。 エラーが発生しなかった場合は、NULL が格納されます。|  
|**error_type**|**int**|返されるエラーを表す整数が格納されます。 error_type_desc にマップされます。 解説の下の一覧を参照してください。|  
|**error_type_desc**|**nvarchar(60)**|返されるエラーを表す短い大文字の文字列が格納されます。 error_type にマップされます。 解説の下の一覧を参照してください。|  
  
## <a name="remarks"></a>コメント  
 この関数と同じアルゴリズムを使用して**sp_describe_first_result_set**します。 詳細については、[sp_describe_first_result_set & #40 を参照してください。TRANSACT-SQL と #41 です](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)。  
  
 次の表に、エラーの種類とその説明を示します。  
  
|error_type|error_type|説明|  
|-----------------|-----------------|-----------------|  
|1|MISC|他の項目に記載されていないすべてのエラー。|  
|2|SYNTAX|バッチ内で構文エラーが発生しました。|  
|3|CONFLICTING_RESULTS|2 つの有効な最初のステートメント間に競合があるため、結果を特定できませんでした。|  
|4|DYNAMIC_SQL|動的 SQL が最初の結果を返す可能性があるため、結果を特定できませんでした。|  
|5|CLR_PROCEDURE|結果でしたを特定できないため、CLR ストアド プロシージャは、最初の結果を返す可能性がある可能性があります。|  
|6|CLR_TRIGGER|CLR トリガーが最初の結果を返す可能性があるため、結果を特定できませんでした。|  
|7|EXTENDED_PROCEDURE|拡張ストアド プロシージャが最初の結果を返す可能性があるため、結果を特定できませんでした。|  
|8|UNDECLARED_PARAMETER|1 つ以上の結果セットの列のデータ型が、宣言されていないパラメーターに依存する可能性があるために、結果を判別できませんでした。|  
|9|RECURSION|バッチに再帰的なステートメントが含まれているため、結果を特定できませんでした。|  
|10|TEMPORARY_TABLE|バッチの一時テーブルが含まれていますでサポートされていないために、結果を判別できませんでした**sp_describe_first_result_set**します。|  
|11|UNSUPPORTED_STATEMENT|サポートされていないステートメントがバッチに含まれているために、結果を判別できませんでした**sp_describe_first_result_set** (FETCH、REVERT など。)。|  
|12|OBJECT_TYPE_NOT_SUPPORTED|\@Object_id 関数に渡されるでない (つまりストアド プロシージャは) のサポート|  
|13|OBJECT_DOES_NOT_EXIST|\@関数に渡される object_id がシステム カタログに見つかりませんでした。|  
  
## <a name="permissions"></a>アクセス許可  
 実行する権限が必要です、 \@tsql 引数。  
  
## <a name="examples"></a>使用例  
 その他の例のトピックで[sp_describe_first_result_set &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)を使用することできます**sys.dm_exec_describe_first_result_set**します。  
  
### <a name="a-returning-information-about-a-single-transact-sql-statement"></a>A. 単一の Transact-SQL ステートメントに関する情報を返す  
 次のコードは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの結果に関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_exec_describe_first_result_set  
(N'SELECT object_id, name, type_desc FROM sys.indexes', null, 0) ;  
```  
  
### <a name="b-returning-information-about-a-procedure"></a>B. プロシージャに関する情報を返す  
 次の例では、次の 2 つの結果セットを返す pr_TestProc をという名前のストアド プロシージャを作成します。 例を示しますが、 **sys.dm_exec_describe_first_result_set**セットの手順で最初の結果に関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE PROC Production.TestProc  
AS  
SELECT Name, ProductID, Color FROM Production.Product ;  
SELECT Name, SafetyStockLevel, SellStartDate FROM Production.Product ;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set  
('Production.TestProc', NULL, 0) ;  
```  
  
### <a name="c-returning-metadata-from-a-batch-that-contains-multiple-statements"></a>C. 複数のステートメントを含むバッチからメタデータを返す  
 次の例では、2 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント を含むバッチを評価します。 結果セットは、返される最初の結果セットを表します。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set(  
N'SELECT CustomerID, TerritoryID, AccountNumber FROM Sales.Customer WHERE CustomerID = @CustomerID;  
SELECT * FROM Sales.SalesOrderHeader;',  
N'@CustomerID int', 0) AS a;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
  
  
