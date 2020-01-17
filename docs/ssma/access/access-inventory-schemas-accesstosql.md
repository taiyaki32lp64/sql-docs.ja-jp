---
title: インベントリ スキーマ (AccessToSQL) へのアクセス |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c140489877be5f34bc6d7a5b20a4ce36fdb3820f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068953"
---
# <a name="access-inventory-schemas-accesstosql"></a>Access インベントリ スキーマ (AccessToSQL)
次のセクションでは、SSMA によってへのアクセスのスキーマをエクスポートするときに作成されるテーブルを記述する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
## <a name="databases"></a>データベース  
データベース メタデータにエクスポートするが、 **SSMA_Access_InventoryDatabases**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|各データベースを一意に識別する GUID。 この列がテーブルの主キーもあります。|  
|**DatabaseName**|**nvarchar (4000)**|Access データベースの名前。|  
|**ExportTime**|**datetime**|このメタデータが SSMA によって作成された日付と時刻。|  
|**ファイル パス**|**nvarchar (4000)**|Access データベースの完全パスとファイル名。|  
|**FileSize**|**bigint**|サポート技術情報で Access データベースのサイズ。|  
|**FileOwner**|**nvarchar (4000)**|Access データベースの所有者として指定されている Windows アカウント。|  
|**DateCreated**|**datetime**|日付と、Access データベースが作成された時刻。|  
|**DateModified**|**datetime**|日付と、Access データベースが最後に変更します。|  
|**TablesCount**|**int**|Access データベース内のテーブルの数。|  
|**QueriesCount**|**int**|Access データベースにクエリの数。|  
|**FormsCount**|**int**|Access データベース内のフォームの数。|  
|**ModulesCount**|**int**|Access データベース内のモジュールの数。|  
|**ReportsCount**|**int**|Access データベースでのレポートの数。|  
|**MacrosCount**|**int**|Access データベース内のマクロの数。|  
|**AccessVersion**|**nvarchar (4000)**|データベースのアクセスのバージョン。|  
|**照合順序**|**nvarchar (4000)**|Access データベースの照合順序です。 データベースの並べ替えし、文字列を比較、照合順序が決定します。|  
|**JetVersion**|**nvarchar (4000)**|Jet データベース エンジンのバージョン。 Access データベースは、基になる Jet データベース エンジンを使用します。|  
|**IsUpdatable**|**bit**|データベースを更新できるかどうかを示します。 値が 1 の場合は、データベースは更新可能にします。 値が 0 の場合、データベースは読み取り専用です。|  
|**QueryTimeout**|**int**|構成されている ODBC クエリのタイムアウト値 (秒)、データベース。 既定値は 60 秒です。|  
  
## <a name="tables"></a>テーブル  
テーブルのメタデータをエクスポート、 **SSMA_Access_InventoryTables**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このテーブルを含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|テーブルを一意に識別する GUID。 この列がテーブルの主キーもあります。|  
|**TableName**|**nvarchar (4000)**|テーブルの名前です。|  
|**RowsCount**|**int**|テーブルに含まれる行数です。|  
|**ValidationRule**|**nvarchar (4000)**|テーブルの有効な入力を定義するルール。 検証規則が存在しない場合、フィールドには空の文字列が含まれます。|  
|**LinkedTable**|**nvarchar (4000)**|別のテーブル、存在する場合、テーブルにリンクさせます。 このテーブルを使用して、追加、削除、およびその他のテーブルの更新をテーブルをリンクできます。|  
|**ExternalSource**|**nvarchar (4000)**|データ ソースに存在する場合に関連付けられているテーブル。 テーブルがリンクされている場合、このフィールドで指定された外部データ ソースがあります。|  
  
## <a name="columns"></a>[列]  
列のメタデータをエクスポート、 **SSMA_Access_InventoryColumns**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|この列を含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|この列を含むテーブルを識別します。|  
|**ColumnId**|**int**|列を識別するインクリメント整数。 **ColumnId**テーブルの主キーします。|  
|**[ColumnName]**|**nvarchar (4000)**|列の名前です。|  
|**IsNullable**|**bit**|列が null 値を含めることができるかどうかを指定します。 値が 1 の場合、列は null 値を含めることができます。 値が 0 の場合、列は null 値を含めることはできません。 検証規則は null 値を防ぐためにも使用できますに注意してください。|  
|**DataType**|**nvarchar (4000)**|データ アクセスなどの列の入力**テキスト**または**長い**します。|  
|**IsAutoIncrement**|**bit**|列が整数値を自動的にインクリメントするかどうかを指定します。 値が 1 の場合、整数が自動的にインクリメントします。|  
|**Ordinal**|**smallint**|0 から始まる、テーブル内の列の順序。|  
|**DefaultValue**|**nvarchar (4000)**|列の既定値です。|  
|**ValidationRule**|**nvarchar (4000)**|データの検証に使用する規則を追加または列で更新します。|  
  
## <a name="indexes"></a>インデックス  
インデックスのメタデータにエクスポートするが、 **SSMA_Access_InventoryIndexes**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このインデックスを含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|このインデックスを含むテーブルを識別します。|  
|**IndexId**|**int**|インデックスを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**IndexName**|**nvarchar (4000)**|インデックスの名前です。|  
|**ColumnsIncluded**|**nvarchar (4000)**|インデックスに含まれる列を一覧表示します。 列名は、セミコロンで区切られます。|  
|**IsUnique**|**bit**|かどうか、インデックス内の各項目が一意である必要がありますを指定します。 複数列のインデックスの値の組み合わせは一意である必要があります。 値が 1 の場合、インデックスは一意の値を適用します。|  
|**IsPK**|**bit**|かどうか、インデックスが主キーの定義の一部として自動的に作成を指定します。|  
|**IsClustered**|**bit**|インデックスがクラスター化されているを指定します。 クラスター化インデックスは、データの物理記憶域を並べ替えます。 テーブルには、1 つだけのクラスター化インデックスを持つことができます。|  
  
## <a name="foreign-keys"></a>外部キー  
外部キーのメタデータをエクスポート、 **SSMA_Access_InventoryForeignKeys**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|この外部キーを含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|この外部キーを含むテーブルを識別します。|  
|**ForeignKeyId**|**int**|外部キーを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**ForeignKeyName**|**nvarchar (4000)**|インデックスの名前です。|  
|**ReferencedTableId**|**uniqueidentifier**|ソース列を含むテーブルを識別します。|  
|**SourceColumns**|**nvarchar (4000)**|外部キー列または列を一覧表示します。|  
|**ReferencedColumns**|**nvarchar (4000)**|主キー列または外部キーによって参照されている列を一覧表示します。|  
|**IsCascadeForUpdate**|**bit**|主キーの値が更新された場合、そのキー値を参照するすべての行も更新を指定します。|  
|**IsCascadeForDelete**|**bit**|主キーの値が削除された場合、そのキー値を参照するすべての行も削除を指定します。|  
|**IsEnforced**|**bit**|外部キー制約が適用されることを指定します。|  
  
## <a name="queries"></a>クエリ  
クエリのメタデータにエクスポートするが、 **SSMA_Access_InventoryQueries**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このクエリを含むデータベースを識別します。|  
|**QueryId**|**int**|クエリを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**QueryName**|**nvarchar (4000)**|クエリ名を返します。|  
|**QueryText**|**nvarchar (4000)**|SELECT ステートメントなどの SQL クエリ コード。|  
|**IsUpdateable**|**bit**|クエリは更新可能または読み取り専用のかどうかを指定します。|  
|**QueryType**|**nvarchar (4000)**|などのクエリの種類を指定**選択**または**SetOperation**します。|  
|**ExternalSource**|**nvarchar (4000)**|クエリでは、外部データ ソースを参照する場合、クエリで使用される接続文字列です。|  
  
## <a name="forms"></a>フォーム  
フォームのメタデータをエクスポートするのには**SSMA_Access_InventoryForms**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このフォームを含むデータベースを識別します。|  
|**FormId**|**int**|フォームを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**FormName**|**nvarchar (4000)**|フォームの名前。|  
  
## <a name="macros"></a>[マクロ]  
マクロのメタデータにエクスポートするが、 **SSMA_Access_InventoryMacros**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|マクロを含むデータベースを識別します。|  
|**MacroId**|**int**|マクロを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**マクロ名**|**nvarchar (4000)**|マクロの名前。|  
  
## <a name="reports"></a>レポート  
レポートのメタデータにエクスポートするが、 **SSMA_Access_InventoryReports**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|レポートを含むデータベースを識別します。|  
|**ReportId**|**int**|レポートを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**ReportName**|**nvarchar (4000)**|レポートの名前です。|  
  
## <a name="modules"></a>モジュール  
モジュールのメタデータにエクスポートするが、 **SSMA_Access_InventoryModules**テーブル。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|モジュールを含むデータベースを識別します。|  
|**ModuleId**|**int**|モジュールを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**ModuleName**|**nvarchar (4000)**|モジュールの名前。|  
  
## <a name="see-also"></a>関連項目  
[Access インベントリのエクスポート](exporting-an-access-inventory-accesstosql.md)  
  
