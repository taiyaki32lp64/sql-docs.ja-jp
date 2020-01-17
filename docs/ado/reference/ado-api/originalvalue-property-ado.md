---
title: OriginalValue プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 512569ce2baa8acabdf8bcbf8f637ebf20e4f613
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917845"
---
# <a name="originalvalue-property-ado"></a>OriginalValue プロパティ (ADO)
値を示す、[フィールド](../../../ado/reference/ado-api/field-object.md)変更が行われる前に、レコードに存在します。  
  
## <a name="return-value"></a>戻り値  
 返します、**バリアント**変更前のフィールドの値を表す値です。  
  
## <a name="remarks"></a>コメント  
 使用して、 **OriginalValue**を現在のレコードからフィールドの元のフィールドの値を返すプロパティ。  
  
 *即時更新モード*(を呼び出した後にプロバイダーが基になるデータ ソースへの変更書き込みますが、[更新](../../../ado/reference/ado-api/update-method.md)メソッド)、 **OriginalValue**プロパティを返します。変更する前に存在していたフィールドの値 (つまり、前回**更新**メソッドの呼び出し)。 これは、同じ値を[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)メソッドを使用して、置換、[値](../../../ado/reference/ado-api/value-property-ado.md)プロパティ。  
  
 *バッチ更新モード*(をプロバイダーが複数の変更をキャッシュし、呼び出すときにのみ、基になるデータ ソースに書き込む、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッド)、 **OriginalValue**プロパティが変更する前に存在していたフィールドの値を返します (つまり、前回**UpdateBatch**メソッドの呼び出し)。 これは、同じ値を[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)メソッドを使用して、置換、**値**プロパティ。 このプロパティを使用すると、 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)プロパティ、バッチ更新プログラムに起因する競合を解決することができます。  
  
## <a name="record"></a>レコード  
 [レコード](../../../ado/reference/ado-api/record-object-ado.md)、オブジェクト、 **OriginalValue**プロパティは空にする前に追加されたフィールドになります[Update](../../../ado/reference/ado-api/update-method.md)が呼び出されます。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>関連項目  
 [OriginalValue および UnderlyingValue プロパティの例 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue および UnderlyingValue プロパティの例 (vc++)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue プロパティ](../../../ado/reference/ado-api/underlyingvalue-property.md)
