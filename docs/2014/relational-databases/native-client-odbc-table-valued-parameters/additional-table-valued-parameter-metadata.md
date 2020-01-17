---
title: テーブル値パラメーターの追加メタデータ |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b9aea58b56308764f907f8cf54bf74bb0663c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200579"
---
# <a name="additional-table-valued-parameter-metadata"></a>テーブル値パラメーターの追加メタデータ
  テーブル値パラメーターのメタデータを取得するには、は、アプリケーションは、SQLProcedureColumns を呼び出します。 テーブル値パラメーターの場合は、SQLProcedureColumns は、1 つの行を返します。 2 つ追加[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-テーブル値パラメーターに関連付けられたテーブル型のスキーマとカタログ情報を提供する、SS_TYPE_CATALOG_NAME と SS_TYPE_SCHEMA_NAME、特定の列が追加されました。 SS_TYPE_CATALOG_NAME および SS_TYPE_SCHEMA_NAME でドライバー固有のすべての列の以前のバージョンで追加する前に表示は、ODBC 仕様に準拠[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と後、すべての列が ODBC 自体によって指定します。  
  
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
  
 テーブル値パラメーターの追加のメタデータを取得するには、アプリケーションは SQLColumns および SQLPrimaryKeys カタログ関数を使用します。 これらの関数がテーブル値パラメーターのために呼び出される前に、アプリケーションでは、ステートメント属性 SQL_SOPT_SS_NAME_SCOPE を SQL_SS_NAME_SCOPE_TABLE_TYPE に設定する必要があります。 この値は、アプリケーションが実際のテーブルではなくテーブル型のメタデータを必要としていることを示します。 次に、アプリケーションがテーブル値パラメーターの TYPE_NAME を渡します、 *TableName*パラメーター。 SS_TYPE_CATALOG_NAME および SS_TYPE_SCHEMA_NAME は併用、 *CatalogName*と*SchemaName*パラメーターをそれぞれ、カタログとテーブル値パラメーターのスキーマを識別するためにします。 テーブル値パラメーターのメタデータの取得が完了すると、アプリケーションによって、SQL_SOPT_SS_NAME_SCOPE は既定値 SQL_SS_NAME_SCOPE_TABLE に設定し直す必要があります。  
  
 SQL_SOPT_SS_NAME_SCOPE が SQL_SS_NAME_SCOPE_TABLE に設定されると、リンク サーバーへのクエリは失敗します。 SQLColumns または SQLPrimaryKeys とサーバー コンポーネントを含むカタログの呼び出しは失敗します。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
