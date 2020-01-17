---
title: 入力プロパティの例 (プロパティ) (vc++) |Microsoft Docs
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
- Type property [property] [ADO], VC++ example
ms.assetid: a4e23508-fbf3-4468-be55-212e7238802b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e13079d18c8887aa0cdba8e5ae06f86eebca897c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938862"
---
# <a name="type-property-example-property-vc"></a>Type プロパティの例 (プロパティ) (VC++)
この例では、[型](../../../ado/reference/ado-api/type-property-ado.md)プロパティ。 これは、モデルなどの名前と、コレクションの型を一覧表示するためのユーティリティの[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)、[フィールド](../../../ado/reference/ado-api/fields-collection-ado.md)など。  
  
 開く必要はありません、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)へのアクセスをその**プロパティ**コレクションが存在することになるときに、**レコード セット**オブジェクトがインスタンス化します。 ただし、設定、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**をいくつかの動的プロパティを追加、**レコード セット**オブジェクトの**プロパティ**コレクション、例では、もう少し興味深いものを作成します。 図では、単純に明示的に使用して、[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティにアクセスする各[プロパティ](../../../ado/reference/ado-api/property-object-ado.md)オブジェクト。  
  
```  
// BeginTypePropertyCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void TypeX();  
void PrintComError(_com_error &e);  
  
int main() {  
   if (FAILED(::CoInitialize(NULL)))  
      return -1;  
  
   TypeX();  
   ::CoUninitialize();  
}  
  
void TypeX() {  
   // Define ADO object pointers, initialize pointers. These are in the ADODB:: namespace  
   _RecordsetPtr pRst = NULL;  
   PropertyPtr pProperty = NULL;  
  
   // Define Other Variables  
   _bstr_t strMsg;  
   _variant_t vIndex;  
   int intLineCnt = 0;     
  
   try {  
      TESTHR(pRst.CreateInstance (__uuidof(Recordset)));  
  
      // Set the Recordset Cursor Location  
      pRst->CursorLocation = adUseClient;  
  
      for (short iIndex = 0; iIndex <= (pRst->Properties->GetCount() - 1);iIndex++) {  
         vIndex = iIndex;  
         pProperty = pRst->Properties->GetItem(vIndex);  
  
         int propType = (int)pProperty->GetType();  
  
         switch(propType) {  
         case adBigInt:  
            strMsg = "adBigInt";  
            break;  
         case adBinary:  
            strMsg = "adBinary";  
            break;  
         case adBoolean:  
            strMsg = "adBoolean";  
            break;  
         case adBSTR:  
            strMsg = "adBSTR";  
            break;  
         case adChapter:  
            strMsg = "adChapter";  
            break;  
         case adChar:  
            strMsg = "adChar";  
            break;  
         case adCurrency:  
            strMsg = "adCurrency";  
            break;  
         case adDate:  
            strMsg = "adDate";  
            break;  
         case adDBDate:  
            strMsg = "adDBDate";  
            break;  
         case adDBTime:  
            strMsg = "adDBTime";  
            break;  
         case adDBTimeStamp:  
            strMsg = "adDBTimeStamp";  
            break;  
         case adDecimal:  
            strMsg = "adDecimal";  
            break;  
         case adDouble:  
            strMsg = "adDouble";  
            break;  
         case adEmpty:  
            strMsg = "adEmpty";  
            break;  
         case adError:  
            strMsg = "adError";  
            break;  
         case adFileTime:  
            strMsg = "adFileTime";  
            break;  
         case adGUID:  
            strMsg = "adGUID";  
            break;  
         case adIDispatch:  
            strMsg = "adIDispatch";  
            break;  
         case adInteger:  
            strMsg = "adInteger";  
            break;  
         case adIUnknown:  
            strMsg = "adIUnknown";  
            break;  
         case adLongVarBinary:  
            strMsg = "adLongVarBinary";  
            break;  
         case adLongVarChar:  
            strMsg = "adLongVarChar";  
            break;  
         case adLongVarWChar:  
            strMsg = "adLongVarWChar";  
            break;  
         case adNumeric:  
            strMsg = "adNumeric";  
            break;  
         case adPropVariant:  
            strMsg = "adPropVariant";  
            break;  
         case adSingle:  
            strMsg = "adSingle";  
            break;  
         case adSmallInt:  
            strMsg = "adSmallInt";  
            break;  
         case adTinyInt:  
            strMsg = "adTinyInt";  
            break;  
         case adUnsignedBigInt:  
            strMsg = "adUnsignedBigInt";  
            break;  
         case adUnsignedInt:  
            strMsg = "adUnsignedInt";  
            break;  
         case adUnsignedSmallInt:  
            strMsg = "adUnsignedSmallInt";  
            break;  
         case adUnsignedTinyInt:  
            strMsg = "adUnsignedTinyInt";  
            break;  
         case adUserDefined:  
            strMsg = "adUserDefined";  
            break;  
         case adVarBinary:  
            strMsg = "adVarBinary";  
            break;  
         case adVarChar:  
            strMsg = "adVarChar";  
            break;  
         case adVariant:  
            strMsg = "adVariant";  
            break;  
         case adVarNumeric:  
            strMsg = "adVarNumeric";  
            break;  
         case adVarWChar:  
            strMsg = "adVarWChar";  
            break;  
         case adWChar:  
            strMsg = "adWChar";  
            break;  
         default:  
            strMsg = "*UNKNOWN*";  
            break;  
         }  
  
         intLineCnt++;  
  
         printf ("Property %d : %s,Type = %s\n",iIndex, (LPCSTR)pProperty->GetName(),  
            (LPCSTR)strMsg);  
      }  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      PrintComError(e);  
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
  
## <a name="see-also"></a>関連項目  
 [オブジェクトのプロパティ (ADO)](../../../ado/reference/ado-api/property-object-ado.md)   
 [Type プロパティ (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
