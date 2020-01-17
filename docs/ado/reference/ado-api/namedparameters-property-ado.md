---
title: NamedParameters プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d63c413ebed585782ca5ce0568119dd7e05bf8ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932062"
---
# <a name="namedparameters-property-ado"></a>NamedParameters プロパティ (ADO)
パラメーター名をプロバイダーに渡す必要があるかどうかを示します。  
  
## <a name="remarks"></a>コメント  
 ADO の値を渡しますこのプロパティが true の場合、**名前**内の各パラメーターのプロパティ、**パラメーター**のコレクション、[コマンド オブジェクト](../../../ado/reference/ado-api/command-object-ado.md)します。 プロバイダーでパラメーターと一致するパラメーター名を使用して、 **CommandText**または**CommandStream**プロパティ。 このプロパティが false の場合 (既定値) は、パラメーター名は無視され、プロバイダーでは、パラメーターの順序を使用して、パラメーターに値を照合する、 **CommandText**または**CommandStream**プロパティ。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [CommandText プロパティ (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream プロパティ (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Parameters コレクション (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
