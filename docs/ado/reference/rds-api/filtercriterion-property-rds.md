---
title: FilterCriterion プロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b14e042c7566b6b6f8559e9dc371028a509979
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964071"
---
# <a name="filtercriterion-property-rds"></a>FilterCriterion プロパティ (RDS)
フィルター値で使用する評価演算子を示します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
 *String*  
 A**文字列**の評価の演算子を指定する値、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)レコードにします。 次のいずれかを指定できます: <、 \<=、>、> =、=、または <> します。  
  
## <a name="remarks"></a>コメント  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)、 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 **FilterCriterion**、および[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)プロパティは、並べ替えおよびフィルター処理、クライアント側キャッシュの機能を提供します。 並べ替えの機能は、1 つの列の値によってレコードを並べ替えます。 フィルター機能は、完全な検索条件に基づくレコードのサブセットを表示[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)はキャッシュに保持されます。 [リセット](../../../ado/reference/rds-api/reset-method-rds.md)メソッドは、条件を実行し、現在の置換**Recordset**で更新可能な**レコード セット**します。  
  
 "! ="演算子は無効です**FilterCriterion**。 代わりに、"<>"を使用します。  
  
 フィルターおよび並べ替えの両方のプロパティを設定しを呼び出すかどうか、**リセット**メソッド、行セットが最初にフィルター処理およびに並べ替えられます。 上部にある null 値は、昇順の並べ替えの下部にある null 値は、並べ替えを降順 (既定の動作は、昇順)。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn、SortDirection プロパティおよび Reset メソッドの例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn プロパティ (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterValue プロパティ (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn プロパティ (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection プロパティ (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


