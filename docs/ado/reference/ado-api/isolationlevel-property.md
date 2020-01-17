---
title: IsolationLevel プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc360bc91e977228a6f9139089a7bfa87d912e1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918441"
---
# <a name="isolationlevel-property"></a>IsolationLevel プロパティ
分離のレベルを示します、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 取得または設定、 [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)値。 既定値は**adXactReadCommitted**します。  
  
## <a name="remarks"></a>コメント  
 使用して、 **IsolationLevel** 、分離のレベルを設定するプロパティを**接続**オブジェクト。 設定は無効になります次に呼び出すまで、 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)メソッド。 更新することがなく、プロバイダーが次に高い分離レベルを返す可能性がありますを要求する分離レベルが使用できない場合、 **IsolationLevel**プロパティ。  
  
 **IsolationLevel**読み取り/書き込みプロパティです。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**接続**オブジェクト、 **IsolationLevel**にのみ設定できるプロパティ**adXactUnspecified**。 切断を操作するため、 **Recordset**オブジェクト クライアント サイド キャッシュ、マルチ ユーザーの問題がある可能性があります。 たとえば、2 人のユーザーが同じレコードを更新しようとすると、リモート データ サービスだけは、"win"を最初のレコードを更新したユーザー 2 番目のユーザーの更新要求はエラーで失敗します。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [IsolationLevel および Mode プロパティの例 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel および Mode プロパティの例 (vc++)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
