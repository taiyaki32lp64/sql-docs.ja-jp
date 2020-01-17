---
title: bcp_readfmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_readfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_readfmt function
ms.assetid: 654001c8-ae9f-425c-b820-f0191bf89367
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76ccc4271877b81ae103a89b5df727b74017d9ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688671"
---
# <a name="bcpreadfmt"></a>bcp_readfmt
  指定されたフォーマット ファイルからデータ ファイル形式の定義を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_readfmt (  
HDBC   
hdbc  
,  
LPCTSTR   
szFormatFile  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *hdbc*  
 一括コピーが有効な ODBC 接続ハンドルです。  
  
 *szFormatFile*  
 データ ファイルの形式の値を含むファイルに関するパスとファイル名です。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>コメント  
 後`bcp_readfmt`形式の値を読み取り、適切な呼び出し[bcp_columns](bcp-columns.md)と[bcp_colfmt](bcp-colfmt.md)します。 ユーザーがフォーマット ファイルを解析し、このような呼び出しを行う必要はありません。  
  
 フォーマット ファイルを保持するためには、呼び出す[bcp_writefmt](bcp-writefmt.md)します。 呼び出す`bcp_readfmt`保存形式を参照できます。 詳細については、次を参照してください。 [bcp_init](bcp-init.md)します。  
  
 または、一括コピー ユーティリティ (**bcp**) で参照できるファイルにユーザー定義のデータ形式を保存できます`bcp_readfmt`します。 詳細については、 **bcp**ユーティリティと構造の**bcp**データ形式のファイルを参照してください[一括インポートとエクスポートのデータ&#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)します。  
  
 `BCPDELAYREADFMT`の値、 *eOption*パラメーターの[bcp_control](bcp-control.md) bcp_readfmt の動作を変更します。  
  
> [!NOTE]  
>  4\.2 以降のバージョンによって、フォーマット ファイルが生成される必要がありますが、 **bcp**ユーティリティ。  
  
## <a name="example"></a>例  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
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
if (bcp_init(hdbc, _T("myTable"), _T("myData.csv"),  
   _T("myErrors"),    DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_readfmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   cout << nRowsProcessed << " rows copied to SQL Server\n";  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
