---
title: ReadyState プロパティ (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a2a3d22f30a865687e38aedfaf6e688e677efae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963590"
---
# <a name="readystate-property-rds"></a>ReadyState プロパティ (RDS)
進行状況を示す、 [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトにデータを取得、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または値は次のいずれかを返します。  
  
|値|説明|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|現在のクエリが実行中で、行が取得されていません。 **DataControl**オブジェクトの**Recordset**を使用するためにご利用いただけません。|  
|**adcReadyStateInteractive**|現在のクエリによって取得される行の初期セットが格納されている、 **DataControl**オブジェクトの**レコード セット**使用できるとします。 残りの行がまだフェッチされています。|  
|**adcReadyStateComplete**|現在のクエリによって取得されるすべての行が格納されている、 **DataControl**オブジェクトの**レコード セット**使用できるとします。<br /><br /> この状態は、エラーのため、操作が中止された場合、または場合にも存在、 **Recordset**オブジェクトが初期化されていません。|  
  
> [!NOTE]
>  これらの定数を使用するクライアント側実行可能ファイルには、それらの宣言を提供する必要があります。 RDS ライブラリの既定のインストール フォルダーにあるファイル Adcvbs.inc から使用する定数の宣言を貼り付けるを切り取ってことができます。  
  
## <a name="remarks"></a>コメント  
 使用して、 [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)変更を監視するイベント、 **ReadyState**非同期クエリ操作中にプロパティ。 これは、プロパティの値を定期的に確認するよりも効率的です。  
  
 非同期の操作中にエラーが発生した場合、 **ReadyState**プロパティに対する変更を**adcReadyStateComplete**、[状態](../../../ado/reference/ado-api/state-property-ado.md)からプロパティが変更された**adStateExecuting**に**取得のみ**、および**レコード セット**オブジェクト[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティは*Nothing*.  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [ReadyState プロパティの例 (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel メソッド (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ExecuteOptions プロパティ (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


