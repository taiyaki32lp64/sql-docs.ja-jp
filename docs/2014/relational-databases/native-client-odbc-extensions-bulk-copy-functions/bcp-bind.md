---
title: bcp_bind |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_bind
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 711c82bb627ca9ad1620cf1e11fdbc9dfa5f4351
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63140565"
---
# <a name="bcp_bind"></a>bcp_bind
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に一括コピーするために、プログラム変数からテーブル列にデータをバインドします。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_bind (  
HDBC   
hdbc  
,   
LPCBYTE   
pData  
,  
INT   
cbIndicator  
,  
DBINT   
cbData  
,  
LPCBYTE   
pTerm  
,  
INT   
cbTerm  
,  
INT   
eDataType  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *hdbc*  
 一括コピーが有効な ODBC 接続ハンドルです。  
  
 *pData*  
 データへのポインターがコピーされます。 場合*eDataType*が SQLTEXT、SQLNTEXT、SQLXML、SQLUDT、SQLCHARACTER、SQLVARCHAR、SQLVARBINARY、SQLBINARY、SQLNCHAR または sqlimage の場合、 *pData* NULL を指定できます。 NULL *pData*を長い形式のデータ値が送信されることを示します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用してまとめて[bcp_moretext](bcp-moretext.md)します。 ユーザーを設定する必要がありますのみ*pData*が BLOB 列のそれ以外の場合、バインドするフィールドに対応する列の場合は NULL に**bcp_bind**は失敗します。  
  
 データ内にインジケーターが存在する場合、それらのインジケーターはメモリ内ではデータの直前にあります。 *PData*パラメーターがこの場合と、インジケーターの幅はインジケーター変数を指す、 *cbIndicator*アドレスのユーザー データを一括コピーでは、パラメーターが正しく使用されています。  
  
 *cbIndicator*  
 列のデータに関する長さのインジケーターや NULL インジケーターのバイト単位の長さです。 インジケーターの長さの有効値は、0 (インジケーターを使用しない場合)、1、2、4、または 8 です。 インジケーターは、メモリ内ではすべてのデータの直前にあります。 たとえば、一括コピーを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに整数値を挿入するには、次のような構造体の型定義を使用します。  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 例の場合、 *pData*パラメーターは、宣言された構造体、つまり、BCPBOUNDINT のアドレスのインスタンスのアドレスに設定されます*iIndicator*構造体のメンバー。 *CbIndicator*パラメーターは整数のサイズに設定されます (sizeof と*cbData* (sizeof(int)) 整数のサイズにパラメーターを設定するともう一度。 インスタンスの値、バインドされた列の値の null 値を格納しているサーバーへの行の一括コピーする*iIndicator* SQL_NULL_DATA にメンバーを設定する必要があります。  
  
 *cbData*  
 プログラム変数内のデータのバイト数です。長さのインジケーター、NULL インジケーター、およびターミネータの長さは含まれません。  
  
 設定*cbData* SQL_NULL_DATA をサーバーにコピーされるすべての行に列の NULL 値があることを示します。  
  
 設定*cbData*を SQL_VARLEN_DATA またはことを示します、システムが、文字列ターミネータを使用してデータの長さを決定するその他のメソッドをコピーします。  
  
 整数などの固定長データ型の場合、データ型によってデータの長さがシステムに示されます。 そのため、固定長データ型の*cbData* SQL_VARLEN_DATA にしても、データの長さを安全にすることができます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]文字やバイナリ データ型、 *cbData* SQL_VARLEN_DATA、SQL_NULL_DATA、正の値、または 0 にすることができます。 場合*cbData* SQL_VARLEN_DATA は、システムは、長さや null インジケーター (存在する場合) またはターミネータ シーケンスのいずれかを使用して、データの長さを決定します。 インジケーターとターミネータ シーケンスの両方を指定した場合、システムでは、コピーされるデータ量が少なくなる方法が使用されます。 場合*cbData* SQL_VARLEN_DATA には、列のデータ型は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]文字またはバイナリの型と長さのインジケーターもターミネータ シーケンスを指定すると、システムには、エラー メッセージが返されます。  
  
 場合*cbData*が 0 または正の値をシステムを使用して*cbData*データ長として。 ただし、正の値の場合、 *cbData*長さのインジケーターとターミネータ シーケンスを指定する値をコピーするデータ量が少なくなる方法を使用してデータの長さを決定します。  
  
 *CbData*パラメーターの値は、データのバイト数を表します。 文字データが Unicode ワイド文字では、正の値で表されている場合*cbData*パラメーターの値は、各文字のバイト単位のサイズを乗算する文字数を表します。  
  
 *pTerm*  
 このプログラム変数の終了位置をマークするバイト パターンがある場合、そのバイト パターンを指すポインターです。 たとえば、通常、ANSI 文字列と MBCS C 文字列には 1 バイトのターミネータ (\0) があります。  
  
 変数にターミネータがない場合は、設定*pTerm*を NULL にします。  
  
 C NULL ターミネータをプログラム変数のターミネータとして指定する場合、空文字列 ("") を使用できます。 Null で終わる空の文字列が 1 バイト (ターミネータのバイト自体) を構成するため、設定*cbTerm*を 1 にします。 たとえば、あることを示す内の文字列*szName*が null で終わる、長さを示すために、終端記号を使用することと。  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 この例の文字列形式はから 15 文字をコピーすることを示す可能性があります、 *szName*変数にバインドされたテーブルの 2 番目の列。  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 一括コピー API では、必要に応じて Unicode から MBCS への文字変換が実行されます。 ターミネータのバイト文字列とそのバイト文字列の長さの両方を正しく設定してください。 たとえば、あることを示すで文字列*szName* Unicode null ターミネータ値で終わる Unicode ワイド文字の文字列は。  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 場合、バインドされた[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列がワイド文字での変換は行われません[bcp_sendrow](bcp-sendrow.md)します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列が MBCS 文字型の場合、データが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信されるときに、ワイド文字がマルチバイト文字に変換されます。  
  
 *cbTerm*  
 プログラム変数にターミネータがある場合は、そのターミネータを構成するバイト数です。 変数にターミネータがない場合は、設定*cbTerm*を 0 にします。  
  
 *eDataType*  
 プログラム変数の C データ型です。 プログラム変数内のデータは、データベース列の型に変換されます。 このパラメーターが 0 の場合、変換は実行されません。  
  
 *EDataType*パラメーターは列挙型によって、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlncli.h 内のデータ型のトークン、しない、ODBC C データ型の列挙子。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有の SQLINT2 型を使用して、ODBC の SQL_C_SHORT 型の 2 バイトの整数を指定できます。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SQLXML および SQLUDT データ型のトークンでのサポートが導入され、 *`eDataType`* パラメーター。  
  
 *idxServerCol*  
 データベース テーブル内にある、データのコピー先となる列の序数位置です。 テーブル内の最初の列は列 1 です。 列の序数位置がによって報告された[SQLColumns](../native-client-odbc-api/sqlcolumns.md)します。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>コメント  
 使用**bcp_bind**プログラム変数からのテーブルにデータをコピーする高速で効率的な方法を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 呼び出す[bcp_init](bcp-init.md)これまたは他の一括コピー関数を呼び出す前にします。 呼び出す**bcp_init**設定、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一括コピー先のテーブル。 呼び出すときに**bcp_init**で使用するため**bcp_bind**と[bcp_sendrow](bcp-sendrow.md)、 **bcp_init** _szDataFile_、データ ファイルを示すパラメーターが NULL に設定されています。**bcp_init**_eDirection_パラメーターが DB_IN に設定されます。  
  
 個別**bcp_bind**の各列に対して呼び出し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をコピーするテーブル。 後、必要な**bcp_bind**呼び出しが行われているし、呼び出す**bcp_sendrow**をプログラム変数からのデータ行を送信する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 列の再バインドはサポートされていません。  
  
 必要な場合に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を既に受信した行をコミットするには、呼び出す[bcp_batch](bcp-batch.md)します。 たとえば、呼び出す**bcp_batch** 1000 行が挿入されるたびに、またはその他の任意の間隔で 1 回です。  
  
 挿入する行がこれ以上が存在する場合、呼び出す[bcp_done](bcp-done.md)します。 この操作を行わないと、エラーが発生します。  
  
 指定されたパラメーターの設定を制御[bcp_control](bcp-control.md)、の影響はありません**bcp_bind**行転送します。  
  
 場合*pData*はその値への呼び出しによって指定されるため、列が NULL に設定されて[bcp_moretext](bcp-moretext.md)、以降のすべての列で*eDataType* SQLTEXT、SQLNTEXT に設定SQLXML、SQLUDT、SQLCHARACTER、SQLVARCHAR、SQLVARBINARY、SQLBINARY、SQLNCHAR、または SQLIMAGE をバインドする必要がありますも*pData*は NULL に設定し、その値への呼び出しによっても指定する必要があります`bcp_moretext`します。  
  
 新しい大きな値型など`varchar(max)`、 `varbinary(max)`、または`nvarchar(max)`の型を表すインジケーターとして SQLCHARACTER、SQLVARCHAR、SQLVARBINARY、SQLBINARY、および SQLNCHAR を使用することができます、 *eDataType*パラメーター。  
  
 場合*cbTerm*は任意の値 (1、2、4、または 8) は、プレフィックス、0 ではありません (*cbIndicator*)。 このような状況で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client は、終端文字の検索、ターミネータを基準データの長さを計算 (*は*) を設定し、 *cbData* i の値と値を小さくするプレフィックス。  
  
 場合*cbTerm*は 0 と*cbIndicator* (プレフィックス) が 0、 *cbIndicator* 8 にする必要があります。 8 バイトのプレフィックスでは、次の値を受け取ることができます。  
  
-   0xFFFFFFFFFFFFFFFF は、フィールドの NULL 値を示します。  
  
-   0xFFFFFFFFFFFFFFFE は、データをチャンク単位でサーバーに効率的に送信するために使用する特別なプレフィックスの値として処理されます。 この特別なプレフィックス値を含むデータは、次のような形式になります。  
  
-   < SPECIAL_PREFIX > \<0 または複数のデータ チャンク >< ZERO_CHUNK > 場所。  
  
-   SPECIAL_PREFIX には 0xFFFFFFFFFFFFFFFE を指定します。  
  
-   DATA_CHUNK には、チャンクの長さを含む 4 バイトのプレフィックスを指定し、その後に 4 バイトのプレフィックスで長さを指定した実際のデータを指定します。  
  
-   ZERO_CHUNK には、データの終了を示す、すべてがゼロの 4 バイトの値 (00000000) を指定します。  
  
-   その他の有効な 8 バイト長は、通常のデータ長として処理されます。  
  
 呼び出す[bcp_columns](bcp-columns.md)を使用する場合**bcp_bind**エラーが発生します。  
  
## <a name="bcp_bind-support-for-enhanced-date-and-time-features"></a>bcp_bind による機能強化された日付と時刻のサポート  
 使用される型については、 *eDataType*日付/時刻の型のパラメーターを参照してください[強化された日付と時刻型向けの一括コピーの変更&#40;OLE DB および ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)します。  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="example"></a>例  
  
```  
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.   
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.   
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.   
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
