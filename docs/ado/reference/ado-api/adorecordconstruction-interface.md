---
title: ADORecordConstruction インターフェイス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c56ba0b9d7ebebbf4a9e4baf669bbdc6eb84355e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920809"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction インターフェイス
**ADORecordConstruction**インターフェイスは、ADO の構築に使用**レコード**から OLE DB オブジェクト**行**C/C++ アプリケーション内のオブジェクト。  
  
 このインターフェイスには、次のプロパティがサポートされています。  
  
## <a name="properties"></a>Properties  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|書き込み専用です。<br />OLE DB のコンテナーを設定します**行**この ado オブジェクト**レコード**オブジェクト。|  
|[行](../../../ado/reference/ado-api/row-property-ado.md)|読み取り/書き込みです。<br />OLE DB を取得/設定**行**オブジェクトとの間にこの ADO**レコード**オブジェクト。|  
  
## <a name="methods"></a>メソッド  
 [なし] :  
  
## <a name="events"></a>イベント  
 [なし] :  
  
## <a name="remarks"></a>コメント  
 OLE DB を指定された**行**オブジェクト (`pRow`)、ADO の構築**レコード**オブジェクト (`adoR`)、次の 3 つの基本的な操作に。  
  
1.  ADO の作成**レコード**オブジェクト。  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  クエリ、 **IADORecordConstruction**インターフェイスを**レコード**オブジェクト。  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  呼び出す、 **IADORecordConstruction::put_Row**プロパティを設定するメソッド、OLE DB**行**ADO 上のオブジェクト**レコード**オブジェクト。  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 結果として得られる**adoR**オブジェクトが、ADO を表すようになりました**レコード**OLE DB から構築されたオブジェクト**行**オブジェクト。  
  
 ADO**レコード**オブジェクトは、OLE DB のコンテナーから構築することもできます**行**オブジェクト。  
  
## <a name="requirements"></a>必要条件  
 **バージョン：** ADO 2.0 以降  
  
 **ライブラリ:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
