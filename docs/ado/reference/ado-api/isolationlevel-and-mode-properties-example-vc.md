---
title: IsolationLevel および Mode プロパティの例 (vc++) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Mode property [ADO], VC++ example
- IsolationLevel property [ADO], VC++ example
ms.assetid: 92ddec5d-e3dc-4e8e-997a-c5417cceab69
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb39288499e2a78523ca29f2e1e4feff4ea9a310
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932318"
---
# <a name="isolationlevel-and-mode-properties-example-vc"></a>IsolationLevel および Mode プロパティの例 (vc++)
この例では、[モード](../../../ado/reference/ado-api/mode-property-ado.md)、排他的な接続を開き、プロパティ、および[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)を他のトランザクションの分離を実行したトランザクションを開きます。  
  
## <a name="example"></a>例  
  
```  
// BeginIsolationLevelCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF","EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// This class extracts titles and type from Title table  
class CTitleRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CTitleRs)  
  
   // Column title is the 2nd field in the table  
    ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szau_Title, sizeof(m_szau_Title), lau_TitleStatus, FALSE)  
  
   // Column type is the 3rd field in the table  
   ADO_VARIABLE_LENGTH_ENTRY2(3, adVarChar, m_szau_Type, sizeof(m_szau_Type), lau_TypeStatus, TRUE)  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szau_Title[81];  
   ULONG lau_TitleStatus;  
   CHAR m_szau_Type[13];  
   ULONG lau_TypeStatus;  
};  
  
// Function Declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void IsolationLevelX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   IsolationLevelX();  
  
   ::CoUninitialize();  
}  
  
void IsolationLevelX() {  
   // Define ADO ObjectPointers.  Initialize Pointers on define.  These are in the ADODB :: namespace.  
   _RecordsetPtr  pRstTitles  = NULL;  
   _ConnectionPtr pConnection = NULL;  
  
   // Define other Variables  
   HRESULT hr = S_OK;  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared  
   CTitleRs titlers;   // C++ Class Object  
   LPSTR p_TempStr = NULL;  
   char * token1;  
  
   // Assign Connection String to Variable  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   try {  
      // Open Connection and Titles Table  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Mode = adModeShareExclusive;  
      pConnection->IsolationLevel = adXactIsolated;  
      pConnection->Open(strCnn,"", "", adConnectUnspecified);  
  
      TESTHR(pRstTitles.CreateInstance(__uuidof(Recordset)));  
      pRstTitles->CursorType = adOpenDynamic;  
      pRstTitles->LockType = adLockPessimistic;  
  
      pRstTitles->Open("titles", _variant_t((IDispatch*) pConnection, true),  
                       adOpenDynamic, adLockPessimistic, adCmdTable);  
  
      pConnection->BeginTrans();  
  
      // Display Connection Mode  
      if (pConnection->Mode == adModeShareExclusive)  
         printf("Connection Mode Is Exclusive");  
      else  
         printf("Connection Mode Is Not Exclusive");       
  
      // Display Isolation Level   
      if (pConnection->IsolationLevel == adXactIsolated)  
         printf("\nTransaction is Isolated\n");  
      else  
         printf("\nTransaction is not Isolated\n");  
  
      // Open an IADORecordBinding interface pointer which we will use for binding Recordset to a class.  
      TESTHR(pRstTitles->QueryInterface( __uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ class here  
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Change the type of psychology titles.  
      p_TempStr = (LPSTR) malloc(sizeof(titlers.m_szau_Type));  
  
      while (!(pRstTitles->EndOfFile)) {  
         // Set the final character of the destination string to NULL.  
         p_TempStr[sizeof(titlers.m_szau_Type) - 1] = '\0';  
  
         // The source string will get truncated if its length is   
         // longer than the length of the destination string minus one.  
         strncpy_s(p_TempStr, sizeof(titlers.m_szau_Type), strtok_s(titlers.m_szau_Type, " ", &token1), sizeof(titlers.m_szau_Type) - 1);  
  
         // Compare type with psychology  
         if (!strcmp(p_TempStr,"psychology")) {  
            // Set the final character of the destination string to NULL.  
            titlers.m_szau_Type[sizeof(titlers.m_szau_Type) - 1] = '\0';  
  
            // Copy "self_help" title field.  The source string will get truncated if its length is   
            // longer than the length of the destination string minus one.  
            strncpy_s(titlers.m_szau_Type, sizeof(titlers.m_szau_Type), "self_help", sizeof(titlers.m_szau_Type) - 1);  
            picRs->Update(&titlers);  
         }  
         pRstTitles->MoveNext();  
      }  
  
      // Print current data in recordset.  
      pRstTitles->Requery(adOptionUnspecified);  
  
      // Open again IADORecordBinding interface pointer for Binding   
      // Recordset to a class.  
      TESTHR(pRstTitles->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // ReBinding the Recordset to a C++ Class  
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Move to the first record of the title table  
      pRstTitles->MoveFirst();  
  
      // Clear the screen for the next display  
      // system("cls");  
  
      while (!pRstTitles->EndOfFile) {  
         printf("%s -  %s\n",titlers.lau_TitleStatus == adFldOK ?   
            titlers.m_szau_Title :"<NULL>",  
            titlers.lau_TypeStatus == adFldOK ?   
            titlers.m_szau_Type :"<NULL>");  
         pRstTitles->MoveNext();  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  Release the IADORecordset Interface here.  
   if (picRs)  
      picRs->Release();  
  
   if (pRstTitles)  
      if (pRstTitles->State == adStateOpen)  
         pRstTitles->Close();  
  
   if (pConnection)  
      if (pConnection->State == adStateOpen) {  
         // Restore Original Data  
         pConnection->RollbackTrans();  
  
         pConnection->Close();  
      }  
  
   // Deallocate the memory  
   if (p_TempStr)  
      free(p_TempStr);  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object  
   // pErr is a record object in the Connection's Error collection  
   ErrorPtr pErr = NULL;  
  
   if ((pConnection->Errors->Count)>0) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount-1  
      for (long i = 0 ; i < nCount ; i++) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error Number :%x \t %s",pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.  
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
 **接続モードは排他的**  
**トランザクション分離**  
**データベースのビジー状態 Executive のガイド - ビジネス**  
**コンピューターと料理。その貸借対照表のビジネス**  
**コンピューターの負荷に対処することができます!-ビジネス**  
**コンピューター - ビジネスについての直接の説明**  
**シリコン バレー Gastronomic 扱います - mod_cook**  
**Gourmet 電子レンジ - mod_cook**  
**コンピューターの料理 - 決心についていないユーザーの心理状態**  
**ですがユーザー フレンドリですか。-popular_comp**  
**シリコン バレー - popular_comp のシークレット**  
**Net エチケット - popular_comp**  
**コンピューターの Phobic と非他者と個人:動作のバリエーションの self_help**  
**怒りの敵ですか。-self_help**  
**-Self_help を与えることがなく有効期間**  
**長期にわたるデータ Deprivation:次の 4 つのケース スタディ - self_help**  
**感情的なセキュリティ:新しいアルゴリズムの self_help**  
**タマネギ、Leeks とガーリック トースト:地中海 - trad_cook の料理のシークレット**  
**バッキンガム Palace 台所 - trad_cook で 50 年**  
**寿司、すべてのユーザーですか?-trad_cook**   
## <a name="see-also"></a>関連項目  
 [IsolationLevel プロパティ](../../../ado/reference/ado-api/isolationlevel-property.md)   
 [Mode プロパティ (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)
