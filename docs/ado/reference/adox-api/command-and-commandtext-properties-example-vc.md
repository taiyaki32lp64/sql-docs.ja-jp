---
title: Command プロパティおよび CommandText プロパティの例 (vc++) |Microsoft Docs
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
- CommandText property [ADOX], VC++ example
- Command property [ADOX], VC++ example
ms.assetid: 5a007b9a-be11-4fba-96db-6252993f97b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3c1a54ea3f101449d18fcae00373344b7ecf11c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966733"
---
# <a name="command-and-commandtext-properties-example-vc"></a>Command プロパティおよび CommandText プロパティの例 (VC++)
次のコードを使用する方法を示します、[コマンド](../../../ado/reference/adox-api/command-property-adox.md)プロシージャのテキストを更新するプロパティ。  
  
```  
// BeginCommandTextCpp  
// This sample runs correctly only if procedure 'CustomerById' exists.  
  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ProcedureTextX();  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADOX namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Define ADODB object pointers.  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
   ADODB::_CommandPtr m_pCommand = NULL;  
  
   try {  
      // Open the Connection  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
      TESTHR(hr = m_pCommand.CreateInstance(__uuidof(ADODB::Command)));  
      m_pCnn->Open("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';", "", "", NULL);  
  
      // Open the catalog  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
      // Get the Command  
      m_pCommand = m_pCatalog->Procedures->GetItem("CustomerById")->GetCommand();  
  
      // Update the CommandText  
      m_pCommand->PutCommandText("PARAMETERS [CustId] Text;select "  
         "CustomerId, CompanyName, ContactName "  
         "from Customers where CustomerId = [CustId]");  
      printf("CommandText is updated.\n");  
  
      // Update the Procedure  
      m_pCatalog->Procedures->GetItem("CustomerById")->PutCommand(_variant_t((IDispatch *)m_pCommand));  
      printf("Procedure 'CustomerById' is updated.\n");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in ProcedureTextX...."<< endl;  
   }  
  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [Command プロパティ (ADOX)](../../../ado/reference/adox-api/command-property-adox.md)
