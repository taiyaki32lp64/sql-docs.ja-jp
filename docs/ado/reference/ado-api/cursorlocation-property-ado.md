---
title: CursorLocation プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afee71d4f37e2b3a27247fbeacf51dab66cc1e23
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933284"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation プロパティ (ADO)
カーソル サービスの場所を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**長い**値のいずれかに設定できる、 [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)値。  
  
## <a name="remarks"></a>コメント  
 このプロパティを使用すると、プロバイダーにアクセス可能な各種のカーソル ライブラリを選択できます。 通常、サーバー上のクライアント側のカーソル ライブラリまたはにあるいずれかを使用してのことができます。  
  
 このプロパティの設定では、プロパティが設定された後にのみ確立された接続に影響します。 変更、 **CursorLocation**プロパティは既存の接続に影響を与えません。  
  
 カーソルによって返される、 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)メソッドは、この設定を継承します。 **レコード セット**オブジェクトが、関連付けられた接続からこの設定を自動的に継承されます。  
  
 このプロパティは読み取り/書き込み、[接続](../../../ado/reference/ado-api/connection-object-ado.md)または閉じている[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)、読み取り専用で、オープンと**レコード セット**します。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**Recordset**または**接続**オブジェクト、 **CursorLocation**プロパティは、にのみ設定できます**adUseClient**します。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [付録 A: プロバイダー](../../../ado/guide/appendixes/appendix-a-providers.md)
