---
title: put_OLEDBCommand メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- put_OLEDBCommand method [ADO]
ms.assetid: ca6a5804-bf5c-4afc-99db-22904bc0b33d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e182792a78d07cd6423b4409be95872c707791d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917421"
---
# <a name="putoledbcommand-method"></a>put_OLEDBCommand メソッド
このメソッドは、演算を実行しないと、常に S_OK を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT put_OLEDBCommand(  
      IUnknown *pOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pOLEDBCommand*  
 [in]OLE DB コマンド オブジェクトへのポインター。  
  
## <a name="applies-to"></a>適用対象  
 [IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)
