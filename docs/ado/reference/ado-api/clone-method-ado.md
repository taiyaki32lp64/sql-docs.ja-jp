---
title: Clone メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7439f9a4a04582f4cf4c4878892ed0f4f33e228c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920014"
---
# <a name="clone-method-ado"></a>Clone メソッド (ADO)
複製を作成します[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)既存のオブジェクト**Recordset**オブジェクト。 必要に応じて、複製が読み取り専用であることを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>戻り値  
 返します、 **Recordset**オブジェクト参照。  
  
#### <a name="parameters"></a>パラメーター  
 *rstDuplicate*  
 重複を識別するオブジェクト変数**Recordset**オブジェクトを作成します。  
  
 *rstOriginal*  
 オブジェクト変数を識別する、 **Recordset**重複するオブジェクト。  
  
 *LockType*  
 任意。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 、元のいずれか、ロックの種類を指定する値**レコード セット**、または読み取り専用**Recordset**します。 有効な値は**adLockUnspecified**または**adLockReadOnly**します。  
  
## <a name="remarks"></a>コメント  
 使用して、**複製**複数作成するメソッドが重複しています**レコード セット**オブジェクトの場合、特定のレコード セットの 1 つ以上の現在のレコードを保持したい場合に特にです。 使用して、**複製**メソッドが作成して開く、新しいよりも効率的**レコード セット**元として、同じ定義を使用するオブジェクト。  
  
 [フィルター](../../../ado/reference/ado-api/filter-property.md) 、元のプロパティ**レコード セット**、複製には適用されません。 設定、**フィルター**プロパティの新しい**Recordset**結果をフィルター処理します。 既存のすべてのコピーを最も簡単な方法**フィルター**値は、次のように、直接割り当てることができます。  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 新しく作成された複製の現在のレコードは、最初のレコードに設定されます。  
  
 いずれかに加えた**Recordset**オブジェクトは、すべてのカーソルの種類に関係なく複製に表示されます。 実行した後、ただし[Requery](../../../ado/reference/ado-api/requery-method.md)元の**レコード セット**クローンは元に不要になった同期します。  
  
 元の閉じる**レコード セット**が、そのコピーを閉じないも閉じるコピーを閉じるは元のまたは他のコピーのいずれか。  
  
 複製することしか、 **Recordset**ブックマークをサポートするオブジェクト。 ブックマークの値を交換できます。1 つからのブックマーク参照は、**レコード セット**オブジェクトがその複製のいずれかで同じレコードを参照します。  
  
 いくつか**Recordset**すべてにもトリガーされるイベントが発生**レコード セット**のクローンを作成します。 ただし、現在のレコードが異なるため、複製**レコード セット**イベントは、複製の有効なできない可能性があります。 たとえば、フィールドの値を変更する場合、 [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)で、変更されたイベントが発生**レコード セット**とすべてのクローンで。 *フィールド*のパラメーター、 **WillChangeField**の複製されたイベント**Recordset** (場所は変更されませんでした) は、複製の現在のレコードのフィールドを参照元の現在のレコードより別のレコードである**レコード セット**変更が発生しました。  
  
 次の表は、すべての完全な一覧**Recordset**イベント。 有効でを使用して生成されたすべてのレコード セットの複製のトリガーされたかどうかを示します、**複製**メソッド。  
  
|event|クローンで発生するでしょうか。|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|いいえ|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|いいえ|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|いいえ|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[はい]|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|いいえ|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|はい|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|いいえ|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[はい]|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[はい]|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|いいえ|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|いいえ|  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Clone メソッドの例 (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Clone メソッドの例 (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Clone メソッドの例 (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
