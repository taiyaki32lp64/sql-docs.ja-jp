---
title: ExecuteOptions プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2ae55ec1fccbd491854fb8bff2daa215d38b20ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964185"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions プロパティ (RDS)
非同期実行が有効になっているかどうかを示します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または値は次のいずれかを返します。  
  
|定数|説明|  
|--------------|-----------------|  
|**adcExecSync**|次の更新の実行、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)同期的にします。|  
|**adcExecAsync**|既定値です。 次の更新の実行、**レコード セット**非同期的にします。|  
  
> [!NOTE]
>  これらの定数を使用する各実行可能ファイルには、それらの宣言を提供する必要があります。 RDS ライブラリの既定のインストール フォルダーにあるファイル Adcvbs.inc から使用する定数の宣言を貼り付けるを切り取ってことができます。  
  
## <a name="remarks"></a>コメント  
 場合**ExecuteOptions**に設定されている**adcExecAsync**、[次へ] を非同期的に実行この**更新**を呼び出す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトの**Recordset**します。  
  
 呼び出しを試みる場合[リセット](../../../ado/reference/rds-api/reset-method-rds.md)、[更新](../../../ado/reference/rds-api/refresh-method-rds.md)、 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)、または[Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)変わる可能性がある別の非同期操作中に、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトの**Recordset**実行すると、エラーが発生します。  
  
 非同期の操作中にエラーが発生した場合、 **rds.DataControl**オブジェクトの[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)値から変更**adcReadyStateLoaded**に**adcReadyStateComplete**、および**レコード セット**プロパティ値のまま*Nothing*します。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [ExecuteOptions と FetchOptions プロパティの例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel メソッド (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


