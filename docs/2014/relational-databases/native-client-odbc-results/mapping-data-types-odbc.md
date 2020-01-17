---
title: データ型 (ODBC) のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcca4bc6161526d1bd78e55bc9452f2d7d9d69d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200004"
---
# <a name="mapping-data-types-odbc"></a>データ型のマッピング (ODBC)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのマップ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ODBC SQL データ型への SQL データ型。 次のセクションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL データ型とマップ先の ODBC SQL データ型について説明します。 また、ODBC SQL データ型と対応する ODBC C データ型、およびサポートされる変換と既定の変換についても説明します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**タイムスタンプ**ため、データ型の SQL_BINARY または SQL_VARBINARY ODBC データ型にマップ内の値**タイムスタンプ**の列がない**datetime**値**binary (8)** または**varbinary (8)** のシーケンスを示す値を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]行上のアクティビティ。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、奇数バイトの SQL_C_WCHAR (Unicode) 型の値を処理する場合、末尾の奇数バイトが切り捨てられます。  
  
## <a name="dealing-with-sqlvariant-data-type-in-odbc"></a>ODBC での sql_variant データ型の処理  
 **Sql_variant**データ型の列は内のデータ型のいずれかを含めることができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]などのラージ オブジェクト (Lob) を除く**テキスト**、 **ntext**、および**イメージ**します。 たとえば、列を含めたり**smallint**いくつかの行の値**float** 、他の行の値と**char または nchar**残りの部分で値。  
  
 **Sql_variant**データ型と似ています、**バリアント**Microsoft Visual Basic でのデータ型します。  
  
### <a name="retrieving-data-from-the-server"></a>サーバーからのデータの取得  
 ODBC がバリアントの型の概念の使用を制限、 **sql_variant**で ODBC ドライバーのデータ型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、バインドが指定した場合、 **sql_variant**データ型は、文書化されている ODBC のデータ型のいずれかにバインドする必要があります。 **SQL_CA_SS_VARIANT_TYPE**、固有の新しい属性、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、インスタンス内のデータ型を返します、 **sql_variant**列をユーザーにします。  
  
 バインドが指定されていない場合、 [SQLGetData](../native-client-odbc-api/sqlgetdata.md)内のインスタンスのデータ型を決定する関数を使用できます、 **sql_variant**列。  
  
 取得する**sql_variant**データが次の手順に従います。  
  
1.  呼び出す**SQLFetch**を取得する行に配置します。  
  
2.  呼び出す**SQLGetData**SQL_C_BINARY を型とデータ長に 0 を指定します。 これにより、読み取り、ドライバー、 **sql_variant**ヘッダー。 ヘッダーでは、そのインスタンスのデータ型には、 **sql_variant**列。 **SQLGetData**値のバイト単位でサイズを返します。  
  
3.  呼び出す[SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)を指定して**SQL_CA_SS_VARIANT_TYPE**属性値として。 この関数は、インスタンスでの C データ型を返します、 **sql_variant**クライアントへの列。  
  
 上記の手順を行うコードを次に示します。  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 ユーザーを使用してバインディングを作成した場合[SQLBindCol](../native-client-odbc-api/sqlbindcol.md)ドライバーが、メタデータとデータを読み取ります。 次に、そのデータをバインドに指定されている適切な ODBC 型に変換します。  
  
### <a name="sending-data-to-the-server"></a>サーバーへのデータの送信  
 **SQL_SS_VARIANT**、新しいデータ型に固有の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC ドライバーに送信されるデータの使用、 **sql_variant**列。 パラメーターを使用してサーバーにデータを送信するときに (たとえば、INSERT INTO TableName VALUES (?、ですか?))、 [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) C 型と、対応するなどのパラメーター情報を指定するために使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、適切ないずれかに C データ型を変換**sql_variant**サブタイプ。  
  
## <a name="see-also"></a>関連項目  
 [結果の処理&#40;ODBC&#41;](processing-results-odbc.md)  
  
  
