---
title: ADOStreamConstruction インターフェイス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70a6dd02722a34159b345a83b32897aa8c38d0ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920786"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction インターフェイス
**ADOStreamConstruction**インターフェイスは、ADO の構築に使用**Stream**から OLE DB オブジェクト**IStream** C/C++ アプリケーション内のオブジェクト。  
  
## <a name="properties"></a>Properties  
  
|||  
|-|-|  
|[Stream プロパティ](../../../ado/reference/ado-api/stream-property.md)|読み取り/書き込みです。 OLE DB を取得/設定**Stream**オブジェクト。|  
  
## <a name="methods"></a>メソッド  
 [なし] :  
  
## <a name="events"></a>イベント  
 [なし] :  
  
## <a name="remarks"></a>コメント  
 OLE DB を指定された**IStream**オブジェクト (`pStream`)、ADO の構築**Stream**オブジェクト (`adoStr`) に次の 3 つの基本的な操作。  
  
1.  ADO の作成**Stream**オブジェクト。  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  クエリ、 **IADOStreamConstruction**インターフェイスを**Stream**オブジェクト。  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 呼び出す、`IADOStreamConstruction::get_Stream`プロパティを設定するメソッド、OLE DB **IStream** ADO 上のオブジェクト**Stream**オブジェクト。  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 結果として得られる`adoStr`オブジェクトが、ADO を表すようになりました**Stream** OLE DB から構築されたオブジェクト**IStream**オブジェクト。  
  
## <a name="requirements"></a>必要条件  
 **バージョン：** ADO 2.0 またはそれ以降のバージョン  
  
 **ライブラリ:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>関連項目  
 [ADO の API リファレンス](../../../ado/reference/ado-api/ado-api-reference.md)
