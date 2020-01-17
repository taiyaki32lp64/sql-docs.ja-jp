---
title: Reset メソッド (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 416aaefa95871e909a12117756ea59747c555650
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963492"
---
# <a name="reset-method-rds"></a>Reset メソッド (RDS)
クライアント側での並べ替えまたはフィルター処理を実行します**レコード セット**指定の並べ替えとフィルター処理のプロパティを基にします。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
 *value*  
 任意。 A**ブール**値**True** 「フィルター」現在の行セットをフィルター処理する場合 (既定)。 **False**以前のフィルター オプションの削除を元の行セットのフィルター処理、ことを示します。  
  
## <a name="remarks"></a>コメント  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)、 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)、および[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)プロパティは、並べ替えおよびフィルター処理、クライアント側キャッシュの機能を提供します。 並べ替えの機能は、1 つの列の値によってレコードを並べ替えます。 フィルターの機能は、すべての検索条件に基づくレコードのサブセットを表示[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)はキャッシュに保持されます。 **リセット**メソッドは、条件を実行し、現在の置換**Recordset**で更新可能な**レコード セット**します。  
  
 送信されていない元のデータへの変更がある場合、**リセット**メソッドは失敗します。 まず、使用して、 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)読み取り/書き込みに変更を保存するメソッド**レコード セット**、しを使用して、**リセット**並べ替えまたはレコードをフィルター処理するメソッド。  
  
 オプションを使用することができます、行セットに対して 1 つ以上のフィルターを実行する場合は、*ブール*引数と、**リセット**メソッド。 次の例では、これを行う方法を示します。  
  
```  
ADC.SQL = "Select au_lname from authors"  
ADC.Refresh    ' Get the new rowset.  
  
ADC.FilterColumn = "au_lname"  
ADC.FilterCriterion = "<"  
ADC.FilterValue = "'M'"  
ADC.Reset         ' Rowset now has all Last Names < "M".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'F'"  
' Passing True is not necessary, because it is the   
' default filter on the current "filtered" rowset.  
ADC.Reset(TRUE)     ' Rowset now has all Last   
                    ' Names < "M" and > "F".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'T'"  
' Filter on the original rowset, throwing out the  
' previous filter options.  
ADC.Reset(FALSE)   ' Rowset now has all Last Names > "T".  
```  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn、SortDirection プロパティおよび Reset メソッドの例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges メソッド (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



