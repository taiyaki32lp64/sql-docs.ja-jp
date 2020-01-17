---
title: RecordCount プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7304062298a95406a223ba58026379a3bebf392f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931477"
---
# <a name="recordcount-property-ado"></a>RecordCount プロパティ (ADO)

内のレコードの数を示す、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。
  
## <a name="return-value"></a>戻り値

返します、**長い**内のレコードの数を示す値、 **Recordset**します。
  
## <a name="remarks"></a>コメント

使用して、 **RecordCount**でレコードの数を確認するプロパティには、**レコード セット**オブジェクト。 プロパティは、ADO レコードの数を判断できない場合、または、プロバイダーまたはカーソルの種類がサポートされていない場合に-1 を返します**RecordCount**します。 読み取り、 **RecordCount**プロパティを閉じている**Recordset**エラーが発生します。

#### <a name="bookmarks-or-approximate-positioning"></a>ブックマークまたは概数の配置

場合、レコード セット オブジェクト*は*いずれかのブックマークをサポートまたは概数配置、このプロパティを返しますレコード数の正確なレコード セット。 このプロパティは、レコード セットに完全設定がされるかどうかに関係なく正確な数を返します。

これに対して、レコード セット オブジェクトは*いない*ブックマークまたはおおよその位置のいずれかをサポートして、このプロパティにアクセスがリソースを大量消費する可能性があります。 ドレインでは、すべてのレコードが取得する必要があり、正確な RecordCount の値を返すをカウントするために発生します。

- **adBookmark**に関連するブックマーク。
- **adApproxPosition**おおよその位置に関連しています。

> [!NOTE]
> 返されるという事実に関係なく、サーバー側カーソルを使用すると ADO version 2.8 およびそれ以前では、SQLOLEDB プロバイダーがすべてのレコードをフェッチ**True**両方の**サポート (adApproxPosition)** と**サポート (adBookmark)** します。
  
カーソルの種類、 **Recordset**オブジェクトは、レコードの数を決定できるかどうかに影響します。 **RecordCount**プロパティは順方向専用カーソルは実際の数、静的なキーセット カーソルといずれか-1 の場合は-1 または動的カーソルのデータ ソースによっては、実際の数を返します。
  
## <a name="applies-to"></a>適用対象

[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目

[Filter および RecordCount プロパティの例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filter および RecordCount プロパティの例 (vc++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition プロパティ (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount プロパティ (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
