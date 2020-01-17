---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c2ee83335e00c3129d73c26db37d40af2375c410
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786049"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  テーブルには、一意の行識別子として使用できる1つ以上の列が含まれる場合があります。また、PRIMARY KEY 制約なしで作成されたテーブルは、SQLPrimaryKeys に空の結果セットを返します。 ODBC 関数[sqlの列](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md)は、主キーのないテーブルの行識別子の候補を報告します。  
  
 SQLPrimaryKeys は、 *CatalogName*、 *SchemaName*、または*TableName*パラメーターの値が存在するかどうかを SQL_SUCCESS 返します。 これらのパラメーターで無効な値が使用されている場合、SQLFetch は SQL_NO_DATA を返します。  
  
 SQLPrimaryKeys は、静的サーバーカーソルで実行できます。 更新可能なカーソル (動的カーソルまたはキーセットカーソル) で SQLPrimaryKeys を実行しようとすると、カーソルの種類が変更されたことを示す SQL_SUCCESS_WITH_INFO が返されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、 *CatalogName*パラメーターの2部構成の名前を使用して、リンクサーバー上のテーブルの情報をレポートすることができます。 *Linked_Server_Name Catalog_Name*です。  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys とテーブル値パラメーター  
 ステートメント属性 SQL_SOPT_SS_NAME_SCOPE の値が既定値の SQL_SS_NAME_SCOPE_TABLE ではなく SQL_SS_NAME_SCOPE_TABLE_TYPE の場合、SQLPrimaryKeys はテーブル型の主キー列に関する情報を返します。 SQL_SOPT_SS_NAME_SCOPE の詳細については、「 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)」を参照してください。  
  
 テーブル値パラメーターの詳細については、「[テーブル値パラメーター &#40;の&#41;ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Sqlprimarykeys 関数](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
