---
title: FetchOptions プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e4e0943a675ef7cf3684ccddd2699fba02dac9e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964120"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions プロパティ (RDS)
非同期のフェッチの種類を示します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="setting-and-return-values"></a>設定して、戻り値  
 設定または値は次のいずれかを返します。  
  
|定数|説明|  
|--------------|-----------------|  
|**adcFetchUpFront**|すべてのレコード、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)コントロールは、アプリケーションに返される前にフェッチされます。 完全な**Recordset**取得された後で、アプリケーションで、何も実行することはできます。|  
|**adcFetchBackground**|コントロールは、レコードの最初のバッチがフェッチされるとすぐにアプリケーションに返すことができます。 それ以降の読み取り、 **Recordset**こと、要求されたレコードが実際にフェッチされるまで、最初のバッチでフェッチいないレコードにアクセスしようは遅延が、どの時点で、コントロールは、アプリケーションに返します。|  
|**adcFetchAsync**|既定値です。 コントロールは、レコードが、バック グラウンドでフェッチ中に、アプリケーションにすぐに返します。 要求されたレコードに最も近いレコードの読み取りし、コントロールはすぐに復帰、ことを示す場合は、アプリケーションがフェッチされていないレコードを読み取るしようとすると、現在の末尾、**レコード セット**に達しています。 呼び出しなど[MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)場合でも、複数のレコードの設定は引き続き、実際にフェッチされた、最後のレコードを現在のレコードの位置を移動は、 **Recordset**します。|  
  
> [!NOTE]
>  これらの定数を使用するクライアント側実行可能ファイルには、それらの宣言を提供する必要があります。 RDS ライブラリの既定のインストール フォルダーにあるファイル Adcvbs.inc から使用する定数の宣言を貼り付けるを切り取ってことができます。  
  
## <a name="remarks"></a>コメント  
 Web アプリケーションでは、通常、使用する**adcFetchAsync** (既定値) の場合は、パフォーマンスを向上させるためです。 コンパイル済みのクライアント アプリケーションでは、通常、使用する**adcFetchBackground**します。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [ExecuteOptions と FetchOptions プロパティの例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel メソッド (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


