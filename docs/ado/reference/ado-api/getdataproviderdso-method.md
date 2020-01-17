---
title: GetDataProviderDSO メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2b5fbe59ab58b31cd0b796cbe46963683aa890b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932486"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO メソッド
Shape プロバイダーから基になる OLE DB データ ソース オブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ppDataProviderDSOIUnknown*  
 [out] 返す基になる OLE DB データ ソース オブジェクトの IUnknown ポインターへのポインター。  
  
## <a name="remarks"></a>コメント  
 このメソッドではない addref インターフェイス ポインター。 呼び出し元が必要な addref を行う必要があります、呼び出し元ポインターを保持する場合、およびリリースします。  
  
## <a name="applies-to"></a>対象  
 [IDSOShapeExtensions インターフェイス](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
