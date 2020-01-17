---
title: ALTER INDEX (選択的 XML インデックス) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cca96a8f-7737-42d2-bbcc-03d5f858dcc1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7883a99a223af67f536a0991bb0ba48f30211bc6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071363"
---
# <a name="alter-index-selective-xml-indexes"></a>ALTER INDEX (選択的 XML インデックス)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  既存の選択的 XML インデックスを変更します。 ALTER INDEX ステートメントは次のアイテムの 1 つ以上を変更します。  
  
-   インデックス付きパスの一覧 (FOR 句)。  
  
-   名前空間の一覧 (WITH XMLNAMESPACES 句)。  
  
-   インデックス オプション (WITH 句)。  
  
 セカンダリ選択的 XML インデックスを変更することはできません。 詳しくは、「[選択的セカンダリ XML インデックスの作成、変更、および削除](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ALTER INDEX index_name  
    ON <table_object>   
    [WITH XMLNAMESPACES ( <xmlnamespace_list> )]  
    FOR ( <promoted_node_path_action_list> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ database_name.schema_name.table_name | schema_name.table_name | table_name }  
<promoted_node_path_action_list> ::=   
<promoted_node_path_action_item> [, <promoted_node_path_action_list>]  
  
<promoted_node_path_action_item>::=   
<add_node_path_item_action> | <remove_node_path_item_action>  
  
<add_node_path_item_action> ::=  
ADD <path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<remove_node_path_item_action> ::= REMOVE <path_name>   
  
<path_name_or_typed_node_path>::=   
<path_name> | <typed_node_path>  
  
<typed_node_path> ::=   
<node_path> [[AS XQUERY <xsd_type_ext>] | [AS SQL <sql_type>]]  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | 'node()'  
  
<sql_values_node_path_item> ::=   
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type_ext> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::= character_string_literal  
<xml_namespace_prefix> ::= identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY =OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE =OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> 引数  
 *index_name*  
 変更する既存のインデックスの名前です。  
  
 *\<table_object>*  
 インデックスに XML 列を含むテーブルです。 次のいずれかの形式を使用します。  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 [WITH XMLNAMESPACES **(** \<xmlnamespace_list> **)** ]  
 インデックスを作成するパスで使用される名前空間の一覧を指定します。 WITH XMLNAMESPACES 句の構文については、「[WITH XMLNAMESPACES &#40;Transact-SQL&#41;](../../t-sql/xml/with-xmlnamespaces.md)」をご覧ください。  
  
 FOR **(** \<promoted_node_path_action_list> **)**  
 追加または削除するインデックス付きパスの一覧です。  
  
-   **パスを追加 (ADD) します。** パスを追加する場合は、CREATE SELECTIVE XML INDEX ステートメントでパスを作成するために使用する同じ構文を使用します。 CREATE または ALTER ステートメントで指定できるパスについては、「[選択的 XML インデックスのパスと最適化ヒントの指定](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)」をご覧ください。  
  
-   **パスを削除 (REMOVE) します。** パスを削除 (REMOVE) する場合、パスの作成時にパスに付けられた名前を指定します。  
  
 [WITH **(** \<index_options> **)** ]  
 \<index_options> は、ALTER INDEX を FOR 句なしで使用する場合にのみ、指定することができます。 ALTER INDEX を使用して、インデックスにパスを追加または削除する場合、インデックス オプションは有効な引数ではありません。 インデックス オプションについては、「[CREATE XML INDEX &#40;選択的 XML インデックス&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)」をご覧ください。  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  ALTER INDEX ステートメントを実行すると、選択的 XML インデックスが常に再構築されます。 サーバーのリソースに対するこの処理の影響を考慮してください。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 ALTER INDEX を実行するには、少なくともテーブルまたはビューに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 ALTER INDEX ステートメントの例を次に示します。 このステートメントは、インデックスの XQuery の部分にパス `'/a/b/m'` を追加し、「[CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)」のトピックの例で作成したインデックスの SQL の部分からパス `'/a/b/e'` を削除します。 削除するパスは、作成時に指定された名前によって識別されます。  
  
```sql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
);  
```  
  
 次の例では、インデックス オプションを指定する ALTER INDEX ステートメントを示しています。 ステートメントで、パスを追加または削除するために FOR 句を使用しないため、インデックス オプションを使用できます。  
  
```sql  
ALTER INDEX sxi_index  
ON Tbl  
PAD_INDEX = ON;  
```  
  
## <a name="see-also"></a>参照  
 [選択的 XML インデックス &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [選択的 XML インデックスの作成、変更、および削除](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [選択的 XML インデックスのパスと最適化ヒントの指定](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  
