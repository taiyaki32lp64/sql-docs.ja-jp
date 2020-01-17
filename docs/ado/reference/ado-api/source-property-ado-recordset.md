---
title: Source プロパティ (ADO Recordset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f6ac84445272ae3657d4e25691dbbf150f32c5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930927"
---
# <a name="source-property-ado-recordset"></a>Source プロパティ (ADO Recordset)
データ ソースを示す、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 セットを**文字列**値または[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクト参照; のみを返します、**文字列**のソースを示す値、**レコード セット**します。  
  
## <a name="remarks"></a>コメント  
 使用して、**ソース**のデータ ソースを指定するプロパティを**レコード セット**オブジェクトを使用して、次のいずれか:**コマンド**オブジェクト変数、SQL ステートメント、ストアド プロシージャでは、または、テーブル名。  
  
 設定した場合、**ソース**プロパティを**コマンド**オブジェクト、 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)のプロパティ、**レコード セット**オブジェクトは継承、値、 **ActiveConnection** 、指定されたプロパティ**コマンド**オブジェクト。 ただし、読み取り、**ソース**プロパティは返されません、**コマンド**オブジェクトは、代わりを返します、 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)のプロパティ、 **コマンド**オブジェクトを設定する、**ソース**プロパティ。  
  
 場合、**ソース**プロパティは、SQL ステートメント、ストアド プロシージャ、またはテーブル名、パフォーマンスを最適化するには、適切なを渡すことによって*オプション*引数と、 [を開く](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドの呼び出し。  
  
 **ソース**プロパティは読み取り/書き込み終了**レコード セット**オブジェクトおよび読み取り専用のオープン**レコード セット**オブジェクト。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Source プロパティの例 (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [ソースのプロパティ (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source プロパティ (ADO Record)](../../../ado/reference/ado-api/source-property-ado-record.md)
