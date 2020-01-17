---
title: 文字変換処理の ODBC ドライバーの動作変更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7f9562f8594e29c33832c595b9296eaf4f2019b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162435"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>文字変換処理での ODBC ドライバーの動作の変更
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC ドライバー (SQLNCLI11.dll) の変更方法での SQL_WCHAR * (NCHAR/NVARCHAR/NVARCHAR(MAX)) と SQL_CHAR\* (CHAR/VARCHAR/NARCHAR(MAX)) 変換します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client ODBC ドライバーを使用する場合、SQLGetData、SQLBindCol、SQLBindParameter などの ODBC 関数では長さまたはインジケーターのパラメーターとして (-4) SQL_NO_TOTAL が返されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは長さの値が返されましたが、これは誤りである可能性があります。  
  
## <a name="sqlgetdata-behavior"></a>SQLGetData の動作  
 多くの Windows 関数ではバッファー サイズに 0 を指定できます。返される長さは、返されるデータのサイズです。 以下は、Windows プログラミングで一般的なパターンです。  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 ただし、 **SQLGetData**このシナリオでは使用しない必要があります。 次のパターンは使用できません。  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 **SQLGetData**実際のデータのチャンクを取得するのみと呼ばれることができます。 使用して**SQLGetData**データのサイズを取得するのにはサポートされていません。  
  
 次に、不適切なパターンを使用した場合のドライバーの変更による影響を示します。 このアプリケーションでは `varchar` 列およびバインドを Unicode (SQL_UNICODE/SQL_WCHAR) としてクエリを実行します。  
  
 クエリ:  `select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ....., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのバージョン|長さまたはインジケーターの結果|説明|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 以前|6|ドライバーには、CHAR から WCHAR への変換が長さ * 2 として実行できるという誤った想定がありました。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (Version 11.0.2100.60) 以降|-4 (SQL_NO_TOTAL)|ドライバーが不要になったが CHAR から WCHAR または WCHAR に変換することを想定する (乗算) \*2 または (除算)/2 操作。<br /><br /> 呼び出す**SQLGetData**不要になった、予期される変換の長さを返します。 ドライバーでは CHAR と WCHAR との間の変換が検出され、誤りの可能性のある *2 または /2 の動作の代わりに (-4) SQL_NO_TOTAL が返されます。|  
  
 使用**SQLGetData**データのチャンクを取得します。 (擬似コードを示します)。  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>SQLBindCol の動作  
 クエリ:  `select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(... SQL_W_CHAR, ...)   // Only bound a buffer of WCHAR[4] - Expecting String Data Right Truncation behavior  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのバージョン|長さまたはインジケーターの結果|説明|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 以前|20|-   **SQLFetch**右側にあるデータの切り捨てがあることを報告します。<br />長さは返される、格納されたしないデータの長さです (前提としています * 2 による CHAR から WCHAR への変換グリフに対して正しいことができます)。<br />-バッファーに格納されたデータは、123 \0 です。 バッファーは NULL 終端であることが保証されます。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (Version 11.0.2100.60) 以降|-4 (SQL_NO_TOTAL)|-   **SQLFetch**右側にあるデータの切り捨てがあることを報告します。<br />残りのデータは変換されていないために、長は-4 (SQL_NO_TOTAL) を示します。<br />-バッファーに格納されたデータは、123 \0 です。 - バッファーは NULL 終端であることが保証されます。|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter (出力パラメーターの動作)  
 クエリ:  `create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(... SQL_W_CHAR, ...)   // Only bind up to first 64 characters  
```  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのバージョン|長さまたはインジケーターの結果|説明|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 以前|2468|-   **SQLFetch**使用可能なデータを返します。<br />-   **SQLMoreResults**使用可能なデータを返します。<br />長さでは、いないバッファーに格納されているサーバーから返されるデータのサイズを示します。<br />-元のバッファーには 63 バイトと終端の NULL が含まれています。 バッファーは NULL 終端であることが保証されます。|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (Version 11.0.2100.60) 以降|-4 (SQL_NO_TOTAL)|-   **SQLFetch**使用可能なデータを返します。<br />-   **SQLMoreResults**使用可能なデータを返します。<br />長さは、残りのデータは変換されていないため、(-4) SQL_NO_TOTAL を示します。<br />-元のバッファーには 63 バイトと終端の NULL が含まれています。 バッファーは NULL 終端であることが保証されます。|  
  
## <a name="performing-char-and-wchar-conversions"></a>CHAR と WCHAR の変換の実行  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ODBC ドライバーには、CHAR と WCHAR の変換を実行する方法が複数用意されています。 ロジックは、blob (varchar (max)、nvarchar (max)、...) の操作に似ています。  
  
-   データの保存またはでバインドする場合は、指定されたバッファーに切り捨てられます**SQLBindCol**または**SQLBindParameter**します。  
  
-   使用してデータ チャンクを取得するには、バインドしない場合**SQLGetData**と**SQLParamData**します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)  
  
  
