---
title: getFunctionColumns メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6c25349d6fbf9495647ae73773d984dfcd269f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982963"
---
# <a name="getfunctioncolumns-method-sqlserverdatabasemetadata"></a>getFunctionColumns メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたカタログのシステム関数またはユーザー関数のパラメーターと戻り値の型に関する記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public ResultSet getFunctionColumns(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern  
                       java.lang.String columnNamePattern)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *catalog*  
  
 カタログ名を含む**文字列**です。 空の文字列 "" の場合、結果にはカタログのない関数が含まれます。 **null** の場合、カタログ名は検索に使用されません。  
  
 *schemaPattern*  
  
 スキーマ名のパターンを含む**文字列**です。 空の文字列 "" の場合、結果にはスキーマのない関数が含まれます。 **null** の場合、スキーマ名は検索に使用されません。  
  
 *functionNamePattern*  
  
 関数の名前を含む**文字列**です。  
  
 *columnNamePattern*  
  
 パラメーターの名前を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getFunctionColumns メソッドは、java.sql.DatabaseMetaData インターフェイスの getFunctionColumns メソッドで規定されています。  
  
 このメソッドは、指定されたカタログ内の指定されたスキーマ、関数名、およびパラメーター名に一致する関数およびパラメーターだけを返します。  
  
 結果セットの各行には、パラメーターの説明、列の説明、または戻り値の型に対する次の列が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|関数が存在するデータベースの名前です。|  
|FUNCTION_SCHEM|**String**|関数のスキーマです。|  
|FUNCTION_NAME|**String**|関数の名前です。|  
|COLUMN_NAME|**String**|パラメーターまたは列の名前です。|  
|COLUMN_TYPE|**short**|**列の型。次のいずれかの値を指定できます。**<br /><br /> functionColumnUnknown (0): 不明な型です。<br /><br /> functionColumnIn (1): 入力パラメーターです。<br /><br /> functionColumnInOut (2): 入力/出力パラメーターです。<br /><br /> functionColumnOut (3): 出力パラメーターです。<br /><br /> functionReturn (4): 関数の戻り値です。<br /><br /> functionColumnResult (5): パラメーターまたは列は結果セット内の列です。|  
|DATA_TYPE|**smallint**|Java.sql.Types からの SQL データ型値です。|  
|TYPE_NAME|**String**|データ型の名前です。|  
|PRECISION|**int**|有効桁数の合計。|  
|LENGTH|**int**|データの長さです (バイト)。|  
|SCALE|**short**|小数点以下の桁数です。|  
|RADIX|**short**|数値型の基数です。|  
|NULLABLE|**short**|パラメーターまたは戻り値に **null** 値を含めることができるかどうかを示します。<br /><br /> **次のいずれかの値を指定できます。**<br /><br /> functionNoNulls (0): NULL 値は許可されません。<br /><br /> functionNullable (1): NULL 値は許可されます。<br /><br /> functionNullableUnknown (2): 不明です。|  
|REMARKS|**String**|列またはパラメーターに関するコメントです。|  
|COLUMN_DEF|**String**|列の既定値です。<br /><br /> **注:** この情報は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で利用可能であり、JDBC ドライバー固有のものです。|  
|SQL_DATA_TYPE|**smallint**|この列は、**datetime** データ型と ISO **interval** データ型以外は、**DATA_TYPE** 列と同じです。<br /><br /> **注:** この情報は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で利用可能であり、JDBC ドライバー固有のものです。|  
|SQL_DATETIME_SUB|**smallint**|**SQL_DATA_TYPE** の値が **SQL_DATETIME** または **SQL_INTERVAL** の場合は、**datetime** ISO **interval** サブコードになります。 **datetime** および **ISO interval** 以外のデータ型の場合、この列は NULL です。<br /><br /> **注:** この情報は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で利用可能であり、JDBC ドライバー固有のものです。|  
|CHAR_OCTET_LENGTH|**int**|パラメーターまたは列に基づいたバイナリおよび文字の最大長です。 他のデータ型の場合は NULL です。|  
|ORDINAL_POSITION|**int**|入力パラメーターおよび出力パラメーターの場合は、1 から始まる位置を表します。<br /><br /> 結果セット列の場合は、1 から始まる結果セット内の列の位置です。<br /><br /> 戻り値の場合は 0 です。|  
|IS_NULLABLE|**String**|パラメーターまたは列で null 値が許可されるかどうかを決定します。<br /><br /> 次のいずれかの値を指定できます。<br /><br /> **YES**: パラメーターまたは列に NULL 値を含めることができます。<br /><br /> **NO**: パラメーターまたは列に NULL 値を含めることができません。<br /><br /> 空の文字列 (""): 不明です。|  
|SS_TYPE_CATALOG_NAME|**String**|UDT (ユーザー定義型) を含むカタログの名前です。|  
|SS_TYPE_SCHEMA_NAME|**String**|UDT (ユーザー定義型) を含むスキーマの名前です。|  
|SS_UDT_CATALOG_NAME|**String**|完全修飾名の UDT (ユーザー定義型) です。|  
|SS_UDT_SCHEMA_NAME|**String**|XML スキーマ コレクション名が定義されているカタログの名前です。 カタログ名が見つからない場合は、この変数に空文字列が含まれます。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|XML スキーマ コレクション名が定義されているスキーマの名前です。 スキーマ名が見つからない場合は、空文字列です。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML スキーマ コレクションの名前です。 名前が見つからない場合は、空文字列です。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|UDT (ユーザー定義型) を含むカタログの名前です。|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|UDT (ユーザー定義型) を含むスキーマの名前です。|  
|SS_DATA_TYPE|**tinyint**|拡張ストアド プロシージャによって使用される [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型です。<br /><br /> **注** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって返されるデータ型の詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「データ型 (Transact-SQL)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
