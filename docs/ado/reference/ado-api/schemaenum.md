---
title: SchemaEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c064120e3c658cafd88a96953ff00e18fbaa9b88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931118"
---
# <a name="schemaenum"></a>SchemaEnum
スキーマの種類を指定します**Recordset**を[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)メソッドを取得します。  
  
## <a name="remarks"></a>コメント  
 各トピックで見つかる各 ADO 定数の関数と列に関する追加情報が返される[付録 b:スキーマ行セット](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1)の OLE DB プログラマーズ リファレンス。 次の表の説明 セクションにかっこで囲まれた各トピックの名前が表示されます。  
  
 各トピックで見つかる各 ADO MD 定数の関数と列に関する追加情報が返される[OLE DB for OLAP オブジェクトおよびスキーマ行セット](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144)オンライン分析処理 (OLAP) のドキュメントの OLE DB でします。 次の表の説明 列にかっこで囲まれた各トピックの名前が表示されます。  
  
 ADO データ型を OLE DB のドキュメント内の列のデータ型を変換するには、ADO の説明の列を参照して[格納](../../../ado/reference/ado-api/datatypeenum.md)トピック。 など、OLE DB データ型の**DBTYPE_WSTR**の ADO データ型と等価**adWChar**します。  
  
 ADO には、定数、値のスキーマのような結果が生成されます。 **adSchemaDBInfoKeywords**と**adSchemaDBInfoLiterals**します。 ADO の作成、**レコード セット**、によってそれぞれ返される値を使用して各行を入力し、 **IDBInfo::GetKeywords**と**IDBInfo::GetLiteralInfo**メソッド。 これらのメソッドに関する追加情報が見つかりません、 [IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) OLE DB プログラマーズ リファレンスのセクション。  
  
|定数|Value|説明|制約列|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|特定のユーザーによって所有されているカタログで定義されているアサーションを返します。<br /><br /> (アサーションの行セット)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|データベース管理システムからアクセス可能なカタログに関連付けられている物理属性を返します。<br /><br /> (行セットのカタログ)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|特定のユーザーにアクセスできる、カタログで定義されている文字セットを返します。<br /><br /> (CHARACTER_SETS 行セット)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|特定のユーザーによって所有されているカタログで定義された check 制約を返します。<br /><br /> (CHECK_CONSTRAINTS)行セット)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|カタログで定義されている、特定のユーザーがアクセスできる文字照合を返します。<br /><br /> (行セットの照合順序)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|カタログで定義されているが使用できる、または特定のユーザーによって付与されるテーブル列の特権を返します。<br /><br /> (COLUMN_PRIVILEGES 行セット)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、COLUMN_NAME、GRANTOR、GRANTEE|  
|**adSchemaColumns**|4|テーブルの列 (ビューを含む)、カタログに定義された特定のユーザーにアクセスできるを返します。<br /><br /> (COLUMNS 行セット)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|カタログで定義されているし、特定のユーザーによって所有されているドメインに依存する、カタログに定義された列を返します。<br /><br /> (COLUMN_DOMAIN_USAGE 行セット)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|参照に関する制約、unique 制約、check 制約、およびアサーションによって使用される、カタログで定義されているし、特定のユーザーによって所有されている列を返します。<br /><br /> (CONSTRAINT_COLUMN_USAGE 行セット)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|参照に関する制約、unique 制約、check 制約、およびカタログで定義されているし、特定のユーザーによって所有されているアサーションによって使用されるテーブルを返します。<br /><br /> (CONSTRAINT_TABLE_USAGE 行セット)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME|  
|**adSchemaCubes**|32|スキーマ (またはプロバイダーがスキーマをサポートしていない場合は、カタログ) では、使用可能なキューブに関する情報を返します。<br /><br /> (キューブ行セット *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|プロバイダー固有のキーワードの一覧を返します。<br /><br /> (IDBInfo::GetKeywords)|\<なし >|  
|**adSchemaDBInfoLiterals**|31|テキスト コマンドで使用されるプロバイダー固有のリテラルの一覧を返します。<br /><br /> (IDBInfo::GetLiteralInfo)|\<なし >|  
|**adSchemaDimensions**|33|特定のキューブ ディメンションに関する情報を返します。 各ディメンションの 1 つの行があります。<br /><br /> (ディメンション行セット)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|特定のユーザーによってカタログで定義されている外部キー列を返します。<br /><br /> (FOREIGN_KEYS 行セット)|PK_TABLE_CATALOG、PK_TABLE_SCHEMA、PK_TABLE_NAME、FK_TABLE_CATALOG、FK_TABLE_SCHEMA、FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|ディメンションの使用可能な階層についての情報を返します。<br /><br /> (行セットの階層)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|特定のユーザーによって所有されているカタログで定義されているインデックスを返します。<br /><br /> (インデックス行セット)|TABLE_CATALOG、TABLE_SCHEMA、INDEX_NAME 型 TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|カタログで定義されている特定のユーザーがキーとして制約する列を返します。<br /><br /> (KEY_COLUMN_USAGE 行セット)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、COLUMN_NAME|  
|**adSchemaLevels**|35|ディメンションで使用できるレベルに関する情報を返します。<br /><br /> (行セットのレベル)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME される LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|使用できるメジャーに関する情報を返します。<br /><br /> (メジャー行セット)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|利用可能なメンバーに関する情報を返します。<br /><br /> (行セットのメンバー)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME される LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE ツリー演算子です。 詳細については、のオンライン分析処理 (OLAP) の OLE DB を参照してください。|  
|**adSchemaPrimaryKeys**|28|特定のユーザーによってカタログで定義されている主キー列を返します。<br /><br /> (PRIMARY_KEYS 行セット)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|プロシージャによって返される行セットの列に関する情報を返します。<br /><br /> (PROCEDURE_COLUMNS 行セット)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|プロシージャのパラメーターとリターン コードに関する情報を返します。<br /><br /> (PROCEDURE_PARAMETERS 行セット)|PROCEDURE_CATALOG、PROCEDURE_SCHEMA、PROCEDURE_NAME、PARAMETER_NAME|  
|**adSchemaProcedures**|16|特定のユーザーによって所有されているカタログで定義されているプロシージャを返します。<br /><br /> (プロシージャ行セット)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|ディメンションの各レベルで利用できるプロパティに関する情報を返します。<br /><br /> (行セットのプロパティ)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME される LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|プロバイダーには、独自の標準スキーマ クエリが定義されている場合に使用されます。|\<プロバイダー固有 >|  
|**adSchemaProviderTypes**|22|データ プロバイダーでサポートされている (基本) データ型を返します。<br /><br /> (PROVIDER_TYPES 行セット)|DATA_TYPE、BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|特定のユーザーによって所有されているカタログで定義されている参照に関する制約を返します。<br /><br /> (REFERENTIAL_CONSTRAINTS 行セット)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|特定のユーザーによって所有されているスキーマ (データベース オブジェクト) を返します。<br /><br /> (スキーマ行セット)|CATALOG_NAME、SCHEMA_NAME、SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|適合性レベル、オプション、およびカタログで定義されているデータには、SQL の実装の処理がサポートされている言語を返します。<br /><br /> (SQL_LANGUAGES 行セット)|\<なし >|  
|**adSchemaStatistics**|19|特定のユーザーによって所有されているカタログで定義されている統計を返します。<br /><br /> (行セットの統計情報)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME|  
|**adSchemaTableConstraints**|10|特定のユーザーによって所有されているカタログで定義されているテーブル制約を返します。<br /><br /> (TABLE_CONSTRAINTS 行セット)|CONSTRAINT_CATALOG、CONSTRAINT_SCHEMA、CONSTRAINT_NAME、TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|カタログで定義されているテーブルが使用できる、または特定のユーザーによって付与される特権を返します。<br /><br /> (TABLE_PRIVILEGES 行セット)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、GRANTOR、GRANTEE|  
|**adSchemaTables**|20|テーブル (ビューを含む)、カタログに定義された特定のユーザーにアクセスできるを返します。<br /><br /> (テーブルの行セット)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME、TABLE_TYPE|  
|**adSchemaTranslations**|21|特定のユーザーにアクセスできる、カタログで定義されている文字変換を返します。<br /><br /> (行セットの翻訳)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|将来使用するために予約されています。||  
|**adSchemaUsagePrivileges**|15|カタログで定義されているオブジェクトが使用できる、または特定のユーザーによって付与の使用法の特権を返します。<br /><br /> (USAGE_PRIVILEGES 行セット)|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE、GRANTOR、GRANTEE|  
|**adSchemaViewColumnUsage**|24|依存する列のテーブルを表示、カタログで定義されている、および、特定のユーザーによって所有されている返します。<br /><br /> (VIEW_COLUMN_USAGE 行セット)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|特定のユーザーにアクセスできる、カタログに定義されたビューを返します。<br /><br /> (行セット ビュー)|TABLE_CATALOG、TABLE_SCHEMA、TABLE_NAME|  
|**adSchemaViewTableUsage**|25|依存するテーブルのテーブルを表示、カタログで定義されているし、特定のユーザーによって所有されている返します。<br /><br /> (VIEW_TABLE_USAGE 行セット)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.Schema.ASSERTS|  
|AdoEnums.Schema.CATALOGS|  
|AdoEnums.Schema.CHARACTERSETS|  
|AdoEnums.Schema.CHECKCONSTRAINTS|  
|AdoEnums.Schema.COLLATIONS|  
|AdoEnums.Schema.COLUMNPRIVILEGES|  
|AdoEnums.Schema.COLUMNS|  
|AdoEnums.Schema.COLUMNSDOMAINUSAGE|  
|AdoEnums.Schema.CONSTRAINTCOLUMNUSAGE|  
|AdoEnums.Schema.CONSTRAINTTABLEUSAGE|  
|AdoEnums.Schema.CUBES|  
|AdoEnums.Schema.DBINFOKEYWORDS|  
|AdoEnums.Schema.DBINFOLITERALS|  
|AdoEnums.Schema.DIMENSIONS|  
|AdoEnums.Schema.FOREIGNKEYS|  
|AdoEnums.Schema.HIERARCHIES|  
|AdoEnums.Schema.INDEXES|  
|AdoEnums.Schema.KEYCOLUMNUSAGE|  
|AdoEnums.Schema.LEVELS|  
|AdoEnums.Schema.MEASURES|  
|AdoEnums.Schema.MEMBERS|  
|AdoEnums.Schema.PRIMARYKEYS|  
|AdoEnums.Schema.PROCEDURECOLUMNS|  
|AdoEnums.Schema.PROCEDUREPARAMETERS|  
|AdoEnums.Schema.PROCEDURES|  
|AdoEnums.Schema.PROPERTIES|  
|AdoEnums.Schema.PROVIDERSPECIFIC|  
|AdoEnums.Schema.PROVIDERTYPES|  
|AdoEnums.Schema.REFERENTIALCONTRAINTS|  
|AdoEnums.Schema.SCHEMATA|  
|AdoEnums.Schema.SQLLANGUAGES|  
|AdoEnums.Schema.STATISTICS|  
|AdoEnums.Schema.TABLECONSTRAINTS|  
|AdoEnums.Schema.TABLEPRIVILEGES|  
|AdoEnums.Schema.TABLES|  
|AdoEnums.Schema.TRANSLATIONS|  
|AdoEnums.Schema.TRUSTEES|  
|AdoEnums.Schema.USAGEPRIVILEGES|  
|AdoEnums.Schema.VIEWCOLUMNUSAGE|  
|AdoEnums.Schema.VIEWS|  
|AdoEnums.Schema.VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>適用対象  
 [OpenSchema メソッド](../../../ado/reference/ado-api/openschema-method.md)
