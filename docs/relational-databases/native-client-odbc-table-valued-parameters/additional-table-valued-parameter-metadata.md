---
title: 追加のテーブル値パラメーターのメタデータ |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a83df9dde4ada571b0fc39f6ac8e45c49d9ac17
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73777898"
---
# <a name="additional-table-valued-parameter-metadata"></a>テーブル値パラメーターの追加メタデータ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  アプリケーションは、テーブル値パラメーターのメタデータを取得するために SQLProcedureColumns を呼び出します。 テーブル値パラメーターの場合、SQLProcedureColumns は単一の行を返します。 テーブル値パラメーターに関連付けられているテーブル型のスキーマとカタログの情報を提供するために、SS_TYPE_CATALOG_NAME と SS_TYPE_SCHEMA_NAME の2つの追加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固有の列が追加されました。 ODBC 仕様に準拠して、SS_TYPE_CATALOG_NAME と SS_TYPE_SCHEMA_NAME は、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で追加されたすべてのドライバー固有の列の前、および ODBC 自体によって指定されたすべての列の前に表示されます。  
  
 テーブル値パラメーターにとって重要な列を次の表に示します。  
  
|列名|データ型|値およびコメント|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|Smallint (NULL 以外)|SQL_SS_TABLE|  
|TYPE_NAME|WVarchar(128) (NULL 以外)|テーブル値パラメーターの型名|  
|COLUMN_SIZE|Integer|NULL|  
|BUFFER_LENGTH|Integer|0|  
|DECIMAL_DIGITS|Smallint|NULL|  
|NUM_PREC_RADIX|Smallint|NULL|  
|NULLABLE|Smallint (NULL 以外)|SQL_NULLABLE|  
|REMARKS|Varchar|NULL|  
|COLUMN_DEF|WVarchar(4000)|NULL|  
|SQL_DATA_TYPE|Smallint (NULL 以外)|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULL|  
|CHAR_OCTET_LENGTH|Integer|NULL|  
|ORDINAL_POSITION|Integer (NULL 以外)|パラメーターの序数位置。|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128) (NULL 以外)|テーブル値パラメーターのテーブル型の型定義が格納されているカタログ。|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128) (NULL 以外)|テーブル値パラメーターのテーブル型の型定義が格納されているスキーマ。|  
  
 WVarchar 列は、ODBC 仕様では Varchar として定義されていますが、実際には、最近のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC ドライバーでは、WVarchar として返されます。 この変更は、ODBC 3.5 仕様に Unicode のサポートが追加されたときに行われましたが、明示されていませんでした。  
  
 アプリケーションでは、テーブル値パラメーターの追加のメタデータを取得するために、SQLColumns および SQLPrimaryKeys カタログ関数を使用します。 これらの関数がテーブル値パラメーターのために呼び出される前に、アプリケーションでは、ステートメント属性 SQL_SOPT_SS_NAME_SCOPE を SQL_SS_NAME_SCOPE_TABLE_TYPE に設定する必要があります。 この値は、アプリケーションが実際のテーブルではなくテーブル型のメタデータを必要としていることを示します。 その後、アプリケーションはテーブル値パラメーターの TYPE_NAME を*TableName*パラメーターとして渡します。 SS_TYPE_CATALOG_NAME と SS_TYPE_SCHEMA_NAME は、 *CatalogName*パラメーターと*SchemaName*パラメーターでそれぞれ使用され、テーブル値パラメーターのカタログとスキーマを識別します。 テーブル値パラメーターのメタデータの取得が完了すると、アプリケーションによって、SQL_SOPT_SS_NAME_SCOPE は既定値 SQL_SS_NAME_SCOPE_TABLE に設定し直す必要があります。  
  
 SQL_SOPT_SS_NAME_SCOPE が SQL_SS_NAME_SCOPE_TABLE に設定されると、リンク サーバーへのクエリは失敗します。 サーバーコンポーネントを含むカタログを使用した SQLColumns または Sqlprimarykey の呼び出しは失敗します。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;の ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
