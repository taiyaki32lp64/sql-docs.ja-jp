---
title: プロパティの例 (vc++) をクラスター化された |Microsoft Docs
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
- Clustered property [ADOX], VC++ example
ms.assetid: b993e357-3e2e-48a7-a627-76909160c97f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33ef2ac09d81d85c6b9170c84bffbc8491dbd995
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966944"
---
# <a name="clustered-property-example-vc"></a>Clustered プロパティの例 (VC++)
この例では、 [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md)のプロパティ、[インデックス](../../../ado/reference/adox-api/index-object-adox.md)します。 エントリのため、この例を返す、Microsoft Jet データベースは、クラスター化インデックスがサポートされていない注**False**の**Clustered**のすべてのインデックスのプロパティ、 *Northwind*データベース。  
  
```  
// BeginClusteredCpp.cpp  
// compile with: /EHsc  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void ClusteredX();  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL) ) )  
      return -1;  
  
   ClusteredX();  
   ::CoUninitialize();  
}  
  
void ClusteredX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _TablePtr m_pTable = NULL;  
   _IndexPtr m_pIndex = NULL;  
  
   // Define other variables here  
   _variant_t vIndex;  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
  
      // Connect to the catalog.  
      m_pCatalog->PutActiveConnection("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';");  
  
      // Enumerate Tables.  
      for (short iTable = 0 ; iTable < m_pCatalog->Tables->Count ; iTable++ ) {  
         vIndex = iTable;  
         m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
  
         // Enumerate Indexes.  
         for (short iIndex = 0 ; iIndex < m_pTable->Indexes->Count ; iIndex++) {  
            vIndex = iIndex;  
            m_pIndex = m_pTable->Indexes->GetItem(vIndex);  
            cout << m_pTable->Name << "   " ;  
            cout << m_pIndex->Name << "   " << (m_pIndex->GetClustered() ? "True" : "False") << endl;  
         }  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in ClusteredX...."<< endl;  
   }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [Clustered プロパティ (ADOX)](../../../ado/reference/adox-api/clustered-property-adox.md)   
 [Index オブジェクト (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)
