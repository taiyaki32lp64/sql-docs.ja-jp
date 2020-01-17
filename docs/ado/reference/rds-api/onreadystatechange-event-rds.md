---
title: onReadyStateChange イベント (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3558fc1fecd343fff480cca3b45c468860a801f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963838"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange イベント (RDS)
**OnReadyStateChange**イベントが呼び出されるたびの値、 [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)プロパティの変更。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>パラメーター  
 [なし] :  
  
## <a name="remarks"></a>コメント  
 **ReadyState**プロパティの進行状況を反映する、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトにデータを非同期的に取得されてその[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 使用して、 **onReadyStateChange**変更を監視するイベント、 **ReadyState**プロパティが出現するたびにします。 これは、プロパティの値を定期的に確認するよりも効率的です。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)


