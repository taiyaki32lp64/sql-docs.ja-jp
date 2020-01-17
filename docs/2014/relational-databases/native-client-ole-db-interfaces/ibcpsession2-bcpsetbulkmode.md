---
title: Ibcpsession 2::bcpsetbulkmode |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BCPSetBulkMode function
ms.assetid: babba19f-e67b-450c-b0e6-523a0f9d23ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e2ba7f2874cc35fbd662c8696fa999980b52bb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62989988"
---
# <a name="ibcpsession2bcpsetbulkmode"></a>IBCPSession2::BCPSetBulkMode
  Ibcpsession 2::bcpsetbulkmode の代替を提供する[ibcpsession::bcpcolfmt &#40;OLE DB&#41; ](ibcpsession-bcpcolfmt-ole-db.md)列の形式を指定するためです。 個々 の列形式属性を設定するには、ibcpsession::bcpcolfmt とは異なり、ibcpsession 2::bcpsetbulkmode はすべての属性を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT BCPSetBulkMode (  
      int property,  
   void * pField,  
   int cbField,  
   void * pRow,  
   int cbRow  
);  
```  
  
## <a name="arguments"></a>引数  
 *property*  
 BYTE 型の定数です。 定数の一覧については、「解説」の表を参照してください。  
  
 *pField*  
 フィールド ターミネータ値を指すポインターです。  
  
 cbField  
 フィールド ターミネータ値の長さです (バイト単位)。  
  
 pRow  
 行ターミネータ値を指すポインターです。  
  
 cbRow  
 行ターミネータ値の長さです (バイト単位)。  
  
## <a name="returns"></a>戻り値  
 Ibcpsession 2::bcpsetbulkmode には、次のいずれかを返すことができます。  
  
|||  
|-|-|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|プロバイダー固有のエラーが発生しました。詳細を確認するには、ISQLServerErrorInfo インターフェイスを使用してください。|  
|`E_UNEXPECTED`|メソッドの呼び出しが予期されませんでした。 たとえば、 `IBCPSession2::BCPInit` ibcpsession 2::bcpsetbulkmode を呼び出す前に、メソッドは呼び出されませんでした。|  
|`E_INVALIDARG`|引数が無効です。|  
|`E_OUTOFMEMORY`|メモリ不足エラー。|  
  
## <a name="remarks"></a>コメント  
 一括コピー出力、クエリまたはテーブルには、ibcpsession 2::bcpsetbulkmode を使用できます。 IBCPSession2::BCPSetBulkMode を使用してクエリ ステートメントを一括コピー出力する場合は、`IBCPSession::BCPControl(BCP_OPTIONS_HINTS, ...)` を呼び出してクエリ ステートメントを指定する前に、これを呼び出す必要があります。  
  
 RPC 呼び出し構文とバッチ クエリ構文 (`{rpc func};SELECT * from Tbl` など) を 1 つのコマンド テキスト内で組み合わせて使用しないでください。  Icommandprepare::prepare にエラーが返され、メタデータの取得できなくなります。 ストアド プロシージャの実行とバッチ クエリを 1 つのコマンド テキストで組み合わせて使用する必要がある場合は、ODBC CALL 構文 (`{call func}; SELECT * from Tbl` など) を使用します。  
  
 *property* パラメーターとして使用できる定数の一覧を次の表に示します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|文字出力モードを指定します。<br /><br /> BCP で-c オプションに対応します。EXE とでは、ibcpsession::bcpcolfmt *eUserDataType*プロパティに設定`BCP_TYPE_SQLCHARACTER`します。|  
|BCP_OUT_WIDE_CHARACTER_MODE|Unicode 出力モードを指定します。<br /><br /> BCP の-w オプションに対応します。EXE およびでは、ibcpsession::bcpcolfmt *eUserDataType*プロパティに設定`BCP_TYPE_SQLNCHAR`します。|  
|BCP_OUT_NATIVE_TEXT_MODE|文字型以外にネイティブ型を指定し、文字型に Unicode を指定します。<br /><br /> BCP で-n オプションに対応します。EXE およびでは、ibcpsession::bcpcolfmt *eUserDataType*プロパティに設定`BCP_TYPE_SQLNCHAR`列の型が文字列の場合または`BCP_TYPE_DEFAULT`場合文字列ではありません。|  
|BCP_OUT_NATIVE_MODE|ネイティブ データベース型を指定します。<br /><br /> BCP で-n オプションに対応します。EXE およびでは、ibcpsession::bcpcolfmt *eUserDataType*プロパティに設定`BCP_TYPE_DEFAULT`します。|  
  
 Ibcpsession 2::bcpsetbulkmode と競合しない ibcpsession::bcpcontrol オプションについては、ibcpsession::bcpcontrol および ibcpsession 2::bcpsetbulkmode を呼び出すことができます。 たとえば、ibcpsession::bcpcontrol でを呼び出すことができます`BCP_OPTION_FIRST`ibcpsession 2::bcpsetbulkmode とします。  
  
 Ibcpsession::bcpcontrol でを呼び出すことはできません`BCP_OPTION_TEXTFILE`ibcpsession 2::bcpsetbulkmode とします。  
  
 Ibcpsession::bcpcolfmt、ibcpsession::bcpcontrol、および ibcpsession::bcpreadfmt を含む関数呼び出しのシーケンスで ibcpsession 2::bcpsetbulkmode を呼び出すしようとした場合、シーケンス エラーが関数呼び出しの 1 つ戻ります。 このエラーを解決するには、IBCPSession::BCPInit を呼び出して設定をリセットし、最初からやり直してください。  
  
 次の表に、関数のシーケンス エラーが発生する関数呼び出しの例をいくつか示します。  
  
 呼び出しシーケンス  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_IN);  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPReadFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_HINTS, "select ...");  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPColFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPReadFmt();  
BCPColFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetBulkMode();  
BCPControl(BCP_OPTION_HINTS, "select ...");  
BCPReadFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPColumns();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetColFmt();  
```  
  
## <a name="example"></a>例  
 次のサンプルでは、IBCPSession2::BCPSetBulkMode の異なる設定を使用して、4 つのファイルを作成します。  
  
```  
  
// compile with: sqlncli11.lib oleaut32.lib ole32.lib  
  
#include <stdio.h>  
#include "sqlncli.h"  
  
IDBInitialize*  g_pIDBInitialize = NULL;  
IBCPSession2 * g_pIBcpSession = NULL;  
class COLEDBPropSet : public DBPROPSET {  
public:  
   COLEDBPropSet() {  
      rgProperties = NULL;  
      cProperties = 0;  
   };  
   COLEDBPropSet(const GUID& guid) {  
      rgProperties = NULL;  
      cProperties = 0;  
      guidPropertySet = guid;  
   };  
   ~COLEDBPropSet() {  
      for ( ULONG i = 0 ; i < cProperties ; i++ )  
         VariantClear(&rgProperties[i].vValue);  
      CoTaskMemFree(rgProperties);  
   }  
   void SetGUID(const GUID& guid) {  
      guidPropertySet = guid;  
   };  
   bool AddProperty(DWORD dwPropertyID, bool bValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BOOL;  
      rgProperties[cProperties].vValue.boolVal = (bValue) ? VARIANT_TRUE : VARIANT_FALSE;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID, long nValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID  = dwPropertyID;  
      rgProperties[cProperties].vValue.vt     = VT_I4;  
      rgProperties[cProperties].vValue.lVal   = nValue;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID,LPCWSTR szValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BSTR;  
      rgProperties[cProperties].vValue.bstrVal = SysAllocString(szValue);  
      cProperties++;  
      return true;  
   };  
   bool Add() {  
      DBPROP* p = (DBPROP*)CoTaskMemRealloc(rgProperties, (cProperties + 1) * sizeof(DBPROP));  
      if (p != NULL) {  
         rgProperties = p;  
         rgProperties[cProperties].dwOptions = DBPROPOPTIONS_REQUIRED;  
         rgProperties[cProperties].colid = DB_NULLID;  
         rgProperties[cProperties].vValue.vt = VT_EMPTY;  
         return true;  
      }  
      else  
         return false;  
   };  
};  
  
void OLEDBCleanUp() {  
   if (g_pIDBInitialize) {  
      g_pIDBInitialize->Release();  
      g_pIDBInitialize = NULL;  
   }  
   if (g_pIBcpSession) {  
      g_pIBcpSession->Release();  
      g_pIBcpSession = NULL;  
   }  
}  
  
BOOL MakeOLEDBConnect(LPWSTR  pServer) {  
   BOOL ret = true;  
   IDBProperties * pIDBProperties = NULL;  
   IDBCreateSession * pIDBCreateSession = NULL;  
   COLEDBPropSet PropSet(DBPROPSET_DBINIT);  
   COLEDBPropSet BcpProperty(DBPROPSET_SQLSERVERDATASOURCE);  
   try {  
      HRESULT hr = CoInitializeEx(NULL,COINIT_MULTITHREADED);   
      hr = CoCreateInstance(SQLNCLI_CLSID, NULL, CLSCTX_INPROC_SERVER, IID_IDBInitialize, (LPVOID *)&g_pIDBInitialize);  
      if (FAILED(hr)) {  
         printf("CoCreateInstance failed\n");  
         return false;  
      }  
      PropSet.AddProperty(DBPROP_INIT_DATASOURCE, (LPWSTR)pServer);  
      PropSet.AddProperty(DBPROP_AUTH_INTEGRATED, L"SSPI");  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBProperties, (void**) &pIDBProperties);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->QueryInterface(IID_IDBProperties...) failed\n");  
         throw false;  
      }  
      hr = pIDBProperties->SetProperties(1, &PropSet);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties(...) failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->Initialize();  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->Initialize() failed\n");  
         throw false;  
      }  
      BcpProperty.AddProperty(SSPROP_ENABLEFASTLOAD, true);  
      BcpProperty.AddProperty(SSPROP_ENABLEBULKCOPY, true);  
      hr = pIDBProperties->SetProperties(1, &BcpProperty);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties() for bcp failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void**) &pIDBCreateSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->QueryInterface(IID_IDBCreateSession..) failed\n");  
         throw false;  
      }  
  
      hr = pIDBCreateSession->CreateSession(NULL, IID_IBCPSession2, (IUnknown**) &g_pIBcpSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBCreateSession->CreateSession() failed\n");  
         throw false;  
      }  
   }  
   catch(...) {  
      ret = false;  
   }  
   if (pIDBProperties)  
      pIDBProperties->Release();  
   if (pIDBCreateSession)  
      pIDBCreateSession->Release();  
   return ret;  
}  
  
BOOL BCPSetBulkMode(LPWSTR pszServer, LPTSTR pszQureryOut, char BCPType, LPWSTR pszDataFile) {  
   HRESULThr;  
   if (!MakeOLEDBConnect(pszServer))  
      return false;  
   hr = g_pIBcpSession->BCPInit(NULL, pszDataFile, NULL, BCP_DIRECTION_OUT );   // bcp init for queryout  
   if (FAILED(hr)) {  
      printf("BCP init failed\n");  
      OLEDBCleanUp();  
      return false;  
   }  
   // setbulkmode  
   char ColTerm[] = "\t";  
   char RowTerm[] = "\r\n";  
   wchar_t wColTerm[] = L"\t";  
   wchar_t wRowTerm[] = L"\r\n";  
   BYTE * pColTerm = NULL;  
   int cbColTerm = NULL;  
   BYTE * pRowTerm = 0;  
   int cbRowTerm = 0;  
   int bulkmode = -1;  
  
   if(BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if(BCPType == 'w') {   // bcp -w  
         pColTerm = (BYTE*)wColTerm;  
         pRowTerm = (BYTE*)wRowTerm;  
         cbColTerm = 2;  
         cbRowTerm = 4;  
         bulkmode = BCP_OUT_WIDE_CHARACTER_MODE;  
      }  
      else  
         if (BCPType == 'n')   // bcp -n  
            bulkmode = BCP_OUT_NATIVE_MODE;  
         else  
            if (BCPType == 'N')   // bcp -n  
               bulkmode = BCP_OUT_NATIVE_TEXT_MODE;  
            else {  
               printf("unknown bcp mode\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            hr = g_pIBcpSession->BCPSetBulkMode(bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (FAILED(hr)) {  
               printf("BCPSetBulkMode failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
  
            // set queryout TSQL statement  
            hr = g_pIBcpSession->BCPControl(BCP_OPTION_HINTS, pszQureryOut);  
            if (FAILED(hr)) {  
               printf("BCPControl failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBROWCOUNT nRowsInserted = 0;  
            hr = g_pIBcpSession->BCPExec(&nRowsInserted);  
            if (FAILED(hr)) {  
               printf("BCPExec failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            OLEDBCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', L"bcpc.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', L"bcpw.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', L"bcpn.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', L"bcp_N.dat");  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [IBCPSession2 &#40;OLE DB&#41;](ibcpsession2-ole-db.md)  
  
  
