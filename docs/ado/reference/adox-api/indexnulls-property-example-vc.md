---
title: IndexNulls プロパティの例 (vc++) |Microsoft Docs
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
- IndexNulls property [ADOX], VC++ example
ms.assetid: ee407e03-4889-4a22-b031-ca542d637c96
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b6a51a16abf767924ee83e93016743693a9f335
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965961"
---
# <a name="indexnulls-property-example-vc"></a>IndexNulls プロパティの例 (VC++)
この例では、 [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md)のプロパティ、[インデックス](../../../ado/reference/adox-api/index-object-adox.md)します。 コードは、新しいインデックスが作成されの値を設定**IndexNulls**ユーザー入力に基づいて。 次に、**インデックス**に追加されますが、**従業員**[テーブル](../../../ado/reference/adox-api/table-object-adox.md)で、 *Northwind* [カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)します。 新しい**インデックス**に適用される、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)に基づいて、**従業員**テーブル、および**レコード セット**が開かれます。 新しいレコードを追加、**従業員**テーブルで、 **Null**インデックス付きフィールドの値。 この新しいレコードを表示するかどうかの設定によって異なります、 **IndexNulls**プロパティ。  
  
```  
// BeignIndexNullCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
#include "icrsint.h"  
using namespace std;  
  
// This class extracts LastName,Country,FirstName from Employees table  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
      // Column LastName is the 2nd field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_szemp_LastName, sizeof(m_szemp_LastName), lemp_LastNameStatus, TRUE)  
  
      // Column Country is the 11th field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(11, adVarChar, m_szemp_Country, sizeof(m_szemp_Country), lemp_CountryStatus, TRUE)  
  
      // Column Country is the 17th field in the table  
      ADO_VARIABLE_LENGTH_ENTRY2(17, adVarChar, m_szemp_FirstName, sizeof(m_szemp_FirstName), lemp_FirstNameStatus, TRUE)  
      END_ADO_BINDING()  
  
public:  
   CHAR m_szemp_LastName[21];  
   ULONG lemp_LastNameStatus;  
   CHAR m_szemp_Country[16];  
   ULONG lemp_CountryStatus;  
   CHAR m_szemp_FirstName[11];  
   ULONG lemp_FirstNameStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void IndexNullsX(_bstr_t);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;   
  
   printf("\nShow records having indexed field value = NULL? (Y/N):");  
   // char input = getche();  
   // Let's pretend you said Yes  
   char input = 'Y';  
  
   if ( toupper(input) == 'Y' )  
      IndexNullsX("Allow");  
   else if ( toupper(input) == 'N' )  
      IndexNullsX("Ignore");  
   else  
      exit(0);  
  
   ::CoUninitialize();  
}  
  
void IndexNullsX(_bstr_t strSel) {  
   HRESULT hr = S_OK;  
  
   // Define and initialie ADOX object pointers. These are in the ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
   _IndexPtr m_pIndexNew = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
   ADODB::_RecordsetPtr m_pRstEmployees = NULL;  
  
   // Define other variables  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared  
   CEmployeeRs emprs;   // C++ Class Object  
  
   // Define string variable.  
   _bstr_t strCnn("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      TESTHR(hr = m_pIndexNew.CreateInstance(__uuidof(Index)));  
      TESTHR(hr = m_pRstEmployees.CreateInstance(__uuidof(ADODB::Recordset)));  
  
      // Connect the catalog.  
      m_pCnn->Open(strCnn, "", "", NULL);  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *)m_pCnn));  
  
      // Append Country column to new index.  
      m_pIndexNew->Columns->Append("Country", adVarWChar, 0);  
      m_pIndexNew->Name = "NewIndex";  
  
      // Set IndexNulls based on user input  
      if (strcmp((LPSTR)strSel, "Allow") == 0 )  
         m_pIndexNew->IndexNulls = adIndexNullsAllow;  
      else if (strcmp((LPSTR)strSel, "Ignore") == 0 )  
         m_pIndexNew->IndexNulls = adIndexNullsIgnore;  
  
      // Append new index to Employees table  
      m_pCatalog->Tables->GetItem("Employees")->Indexes->Append(_variant_t((IDispatch *)m_pIndexNew));  
      m_pRstEmployees->Index = m_pIndexNew->Name;  
      m_pRstEmployees->Open("Employees",   
         _variant_t((IDispatch *)m_pCnn),   
         ADODB::adOpenKeyset,   
         ADODB::adLockOptimistic,  
         ADODB::adCmdTableDirect);  
  
      // Add a new record to the Employees table.  
      m_pRstEmployees->AddNew();  
      m_pRstEmployees->Fields->GetItem("FirstName")->Value = (_bstr_t) "Gary";  
      m_pRstEmployees->Fields->GetItem("LastName")->Value = (_bstr_t) "Haarsager";  
      m_pRstEmployees->Update();  
  
      // Bookmark the newly added record.  
      _variant_t varBookmark = m_pRstEmployees->Bookmark;  
  
      // Use the new index to set the order of the records.  
      m_pRstEmployees->MoveFirst();  
      printf("\n\nIndex = %s,", (LPSTR) m_pRstEmployees->Index);  
      printf("IndexNulls = %d\n\n", m_pIndexNew->IndexNulls);  
      cout<<"Country            -        Name" << endl;  
  
      // Open an IADORecordBinding interface pointer for binding Recordset to a class  
      TESTHR(hr = m_pRstEmployees->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ class here   
      TESTHR(hr = picRs->BindToRecordset(&emprs));  
  
      // Enumerate the Recordset.The value of the IndexNulls property will determine if the newly  
      // added record appears in the output.  
      while ( !(m_pRstEmployees->EndOfFile) ) {  
         printf("%s    -    %s %s\n",  
            emprs.lemp_CountryStatus == adFldOK ? emprs.m_szemp_Country :"[Null]",  
            emprs.lemp_FirstNameStatus == adFldOK ? emprs.m_szemp_FirstName :"<NULL>",  
            emprs.lemp_LastNameStatus == adFldOK ? emprs.m_szemp_LastName :"<NULL>");  
  
         m_pRstEmployees->MoveNext();  
      }  
  
      // Delete new record because this is a demonstration.  
      m_pRstEmployees->Bookmark = varBookmark;  
      m_pRstEmployees->Delete(ADODB::adAffectCurrent);  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in include files...." << endl;  
   }  
  
   if (m_pRstEmployees)  
      if (m_pRstEmployees->State == 1) {  
         m_pRstEmployees->Close();  
         m_pRstEmployees = NULL;  
      }  
  
      // Delete new Index because this is a demonstration.  
      if (m_pCatalog)  
         m_pCatalog->Tables->GetItem("Employees")->Indexes->Delete(m_pIndexNew->Name);  
  
      if (m_pCnn)  
         if (m_pCnn->State == 1) {  
            m_pCnn->Close();  
            m_pCnn = NULL;  
         }  
  
         m_pCatalog = NULL;  
}  
```
