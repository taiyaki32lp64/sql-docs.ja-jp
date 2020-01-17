---
title: bcp_moretext |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_moretext
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83142e83ba04328ddf025e0a2f16ff18ad947075
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688843"
---
# <a name="bcpmoretext"></a>bcp_moretext
  長い可変長データ型の値の一部を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_moretext (  
HDBC   
hdbc  
,  
DBINT   
cbData  
,  
LPCBYTE   
pData  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *hdbc*  
 一括コピーが有効な ODBC 接続ハンドルです。  
  
 *cbData*  
 によって参照されるデータから SQL Server にコピーするデータのバイト数は、 *pData*します。 値 SQL_NULL_DATA は、NULL を示します。  
  
 *pData*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信する、サポートされている長い可変長データ チャンクへのポインターです。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>コメント  
 この関数を組み合わせて使用できる[bcp_bind](bcp-bind.md)と[bcp_sendrow](bcp-sendrow.md) long、数より小さいチャンク内の SQL Server に可変長データ値をコピーします。 **bcp_moretext**次の SQL Server データ型を持つ列で使用できます: `text`、 `ntext`、 `image`、 `varchar(max)`、 `nvarchar(max)`、 `varbinary(max)`、ユーザー定義型 (UDT)、および XML。 **bcp_moretext**サポート データ変換ではありませんが、指定したデータが対象列のデータ型と一致する必要があります。  
  
 場合**bcp_bind**が null 以外で呼び出された*pData*でサポートされているデータ型のパラメーター **bcp_moretext**、`bcp_sendrow`に関係なく、すべてのデータ値を送信します長さ。 場合、ただし、 **bcp_bind** null になります*pData*サポートされているデータ型のパラメーター **bcp_moretext** から正常に返された後すぐにデータをコピーするために使用できます`bcp_sendrow`存在するデータを含むバインドされた列が処理されたことを示します。  
  
 使用する場合**bcp_moretext**行でサポートされているデータ型の 1 つの列を送信する必要がありますもために使用する行の他のすべてのサポートされているデータ型の列を送信します。 列はスキップされません。 サポートされるデータ型は、SQLTEXT、SQLNTEXT、SQLIMAGE、SQLUDT、および SQLXML です。 列の型が varchar(max)、nvarchar(max)、または varbinary(max) の場合、SQLCHARACTER、SQLVARCHAR、SQNCHAR、SQLBINARY、SQLVARBINARY も、サポート対象となります。  
  
 いずれかを呼び出す**bcp_bind**または[bcp_collen](bcp-collen.md) SQL Server の列にコピーするすべてのデータ部分の合計の長さを設定します。 SQL Server への呼び出しで指定されたバイトを送信しようとすると、 **bcp_bind**または`bcp_collen`エラーが生成されます。 このエラーが発生すること、たとえば、使用するアプリケーションで`bcp_collen`、SQL Server の使用可能なデータの長さを設定する`text`4500、列と呼ばれる**bcp_moretext**呼び出しのたびを示すときに 5 回データ バッファーの長さが 1000 バイトです。  
  
 コピーする行に 1 つ以上の長い可変長列が含まれている場合**bcp_moretext**最初の送信を低いものまで、そのデータには、次に、列序数番号が付けられます最小番号序数の列では、という具合です。 コピーするデータの合計長を正しく設定することが重要です。 長さの設定以外に、一括コピーによって列のすべてのデータを受け取ったことを示す方法はありません。  
  
 ときに`var(max)`値が送信される bcp_sendrow と bcp_moretext を使用してサーバーにない列の長さを設定する bcp_collen を呼び出す必要です。 代わりに、ような種類の場合にのみ、値が 0 の長さを持つ呼び出し元の bcp_sendrow で終了します。  
  
 アプリケーションが通常どおり呼び出す`bcp_sendrow`と**bcp_moretext**内でのデータの行数を送信するループします。 ここでは、この 2 つを含むテーブルに対して行う方法の概要`text`列。  
  
```  
while (there are still rows to send)  
{  
bcp_sendrow(...);  
  
for (all the data in the first varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
for (all the data in the second varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
}  
  
```  
  
## <a name="example"></a>例  
 この例は、使用する方法を示します**bcp_moretext**で**bcp_bind**と`bcp_sendrow`:  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      idRow = 5;  
char*      pPart1 = "This text value isn't very long,";  
char*      pPart2 = " but it's broken into three parts";  
char*      pPart3 = " anyhow.";  
DBINT      cbAllParts;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, "comdb..articles", NULL, NULL, DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idRow, 0, SQL_VARLEN_DATA, NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
cbAllParts = (DBINT) (strnlen(pPart1, sizeof(pPart1) + 1) + strnlen(pPart2, sizeof(pPart2) + 1) + strnlen(pPart3, sizeof(pPart3) + 1));  
if (bcp_bind(hdbc, NULL, 0, cbAllParts, NULL, 0, SQLTEXT, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Send this row, with the text value broken into three chunks.   
if (bcp_sendrow(hdbc) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart1, sizeof(pPart1) + 1), pPart1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart2, sizeof(pPart2) + 1), pPart2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart3, sizeof(pPart3) + 1), pPart3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// All done. Get the number of rows processed (should be one).  
nRowsProcessed = bcp_done(hdbc);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
