---
title: CancelUpdate メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CancelUpdate method [RDS]
ms.assetid: 76d8a6e9-bc6c-4ea0-8e7a-2bae5ed06650
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea3be9a06d41718271fee2480da1bf58081c1f07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964590"
---
# <a name="cancelupdate-method-rds"></a>CancelUpdate メソッド (RDS)
現在のまたは新しい行に加えられた変更を取り消します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.CancelUpdate  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
## <a name="remarks"></a>コメント  
 OLE DB により元の値のコピーと、変更のキャッシュの両方のカーソル サービス。 呼び出すと**CancelUpdate**変更のキャッシュが空でにリセットされ、バインドされたコントロールは、元のデータで更新されます。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [CancelUpdate メソッドの例 (VBScript)](../../../ado/reference/rds-api/cancelupdate-method-example-vbscript.md)   
 [アドレス帳のコマンド ボタン](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Cancel メソッド (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel メソッド (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch メソッド (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate メソッド (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Refresh メソッド (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges メソッド (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


