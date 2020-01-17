---
title: SortDirection プロパティ (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortDirection property [RDS]
ms.assetid: 1d9d8715-e4ad-4ff3-bf7f-f1dc0532d8c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 28f0e247c29673fe4dfec507794ad8977b51fcc1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963414"
---
# <a name="sortdirection-property-rds"></a>SortDirection プロパティ (RDS)
並べ替え順序が昇順または降順かどうかを示します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.SortDirection = value  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
 *[値]*  
 A**ブール**値に設定すると**True**並べ替えの方向は昇順を示します。 **False**降順を示します。  
  
## <a name="remarks"></a>コメント  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)、 **SortDirection**、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)、および[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)プロパティは、並べ替えおよびフィルター処理、クライアント側キャッシュの機能を提供します。 並べ替えの機能は、1 つの列から値を使用してレコードを並べ替えます。 フィルター機能は、完全な検索条件に基づくレコードのサブセットを表示[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)はキャッシュに保持されます。 [リセット](../../../ado/reference/rds-api/reset-method-rds.md)メソッドは、条件を実行し、現在の置換**Recordset**で更新可能な**レコード セット**します。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn、SortDirection プロパティおよび Reset メソッドの例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort プロパティ](../../../ado/reference/ado-api/sort-property.md)   
 [SortColumn プロパティ (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)


