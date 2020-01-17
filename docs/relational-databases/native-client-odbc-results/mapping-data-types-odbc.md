---
title: データ型のマッピング (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd3bada9ea15d1104edb33024c4ab1476843c73b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779127"
---
# <a name="mapping-data-types-odbc"></a>データ型のマッピング (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL データ型を ODBC SQL データ型にマップします。 次のセクションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL データ型とマップ先の ODBC SQL データ型について説明します。 また、ODBC SQL データ型と対応する ODBC C データ型、およびサポートされる変換と既定の変換についても説明します。  
  
> [!NOTE]  
>  **Timestamp**列の値は**datetime**値ではなく、 **BINARY (8)** または**VARBINARY (8)** の値を示すため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**TIMESTAMP**データ型は、SQL_BINARY または SQL_VARBINARY ODBC データ型にマップされます。行の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクティビティのシーケンス。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、奇数バイトの SQL_C_WCHAR (Unicode) 型の値を処理する場合、末尾の奇数バイトが切り捨てられます。  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>ODBC での sql_variant データ型の処理  
 **Sql_variant**データ型の列には、 **text**、 **ntext**、 **image**などのラージオブジェクト (lob) を除く [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の任意のデータ型を含めることができます。 たとえば、列には、一部の行に対して**smallint**値、他の行の場合は**float**値、残りの場合は**char/nchar**値を含めることができます。  
  
 **Sql_variant**のデータ型は、Microsoft Visual Basic®の**variant**データ型に似ています。  
  
### <a name="retrieving-data-from-the-server"></a>サーバーからのデータの取得  
 ODBC には variant 型の概念がないため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の ODBC ドライバーで**sql_variant**データ型の使用を制限します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、binding を指定する場合、 **sql_variant**データ型は、ドキュメント化されているいずれかの ODBC データ型にバインドする必要があります。 **SQL_CA_SS_VARIANT_TYPE**、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC ドライバーに固有の新しい属性で、 **sql_variant**列のインスタンスのデータ型がユーザーに返されます。  
  
 バインドが指定されていない場合は、 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)関数を使用して、 **sql_variant**列のインスタンスのデータ型を特定できます。  
  
 **Sql_variant**データを取得するには、次の手順に従います。  
  
1.  **Sqlfetch**を呼び出して、取得した行に移動します。  
  
2.  型に SQL_C_BINARY を指定し、データ長に0を指定して、 **SQLGetData**を呼び出します。 これにより、ドライバーは**sql_variant**ヘッダーを強制的に読み取ります。 ヘッダーは、そのインスタンスのデータ型を**sql_variant**列に提供します。 **SQLGetData**は、値のサイズ (バイト単位) を返します。  
  
3.  属性値として**SQL_CA_SS_VARIANT_TYPE**を指定して[sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)を呼び出します。 この関数は、 **sql_variant**列にあるインスタンスの C データ型をクライアントに返します。  
  
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
  
 ユーザーが[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)を使用してバインドを作成すると、ドライバーはメタデータとデータを読み取ります。 次に、そのデータをバインドに指定されている適切な ODBC 型に変換します。  
  
### <a name="sending-data-to-the-server"></a>サーバーへのデータの送信  
 **SQL_SS_VARIANT**は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC ドライバーに固有の新しいデータ型で、 **sql_variant**列に送信されるデータに対して使用されます。 パラメーターを使用してサーバーにデータを送信する場合 (たとえば、INSERT INTO TableName VALUES (?,?))、 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)を使用して、C 型や対応する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型などのパラメーター情報を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、C データ型を適切な**sql_variant**のサブタイプのいずれかに変換します。  
  
## <a name="see-also"></a>参照  
 [結果&#40;の処理 (ODBC)&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
