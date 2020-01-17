---
title: bcp_writefmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_writefmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_writefmt function
ms.assetid: cb4c1d37-667d-4bcd-b13c-eb638bcc9b69
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d4a5067598b475ed8fe103606088d0e4d6d0554
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62689408"
---
# <a name="bcpwritefmt"></a>bcp_writefmt
  現在の一括コピー データ ファイルの形式に関する記述を含むフォーマット ファイルを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_writefmt (  
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
 データ ファイルの形式の値を受け取るユーザー ファイルのパスとファイル名です。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>コメント  
 フォーマット ファイルでは、一括コピーで作成されるデータ ファイルのデータの形式を指定します。 呼び出す[bcp_columns](bcp-columns.md)と[bcp_colfmt](bcp-colfmt.md)データ ファイルの形式を定義します。 **bcp_writefmt**によって参照されるファイルのこの定義を保存します。 *szFormatFile*します。 詳細については、次を参照してください。 [bcp_init](bcp-init.md)します。  
  
 構造の詳細については**bcp**データ形式のファイルを参照してください[インポートおよび bcp ユーティリティを使用した一括データのエクスポート&#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)します。  
  
 保存されたフォーマット ファイルを読み込むには、次のように使用します。 [bcp_readfmt](bcp-readfmt.md)します。  
  
> [!NOTE]  
>  によって生成されたフォーマット ファイル**bcp_writefmt**のバージョンでのみサポートされて、 **bcp**ユーティリティが付属[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]version 7.0 以降。  
  
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
   _T("myErrors"),    DB_OUT) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_columns(hdbc, 3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
bcp_colfmt(hdbc, 1, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 1);  
bcp_colfmt(hdbc, 2, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 2);  
bcp_colfmt(hdbc, 3, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 3);  
  
if (bcp_writefmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   printf_s("%ld rows copied from SQL Server\n", nRowsProcessed);  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
