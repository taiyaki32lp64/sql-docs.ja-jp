---
title: Flush メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3d9ab76d2f2ed1a6f5dbeaf58be7d2f919acd3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932542"
---
# <a name="flush-method-ado"></a>Flush メソッド (ADO)
内容を強制的、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)を基になるオブジェクトへの ADO のバッファーに残っている、 **Stream**が関連付けられています。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>コメント  
 基になるオブジェクトにストリーム バッファーの内容を送信するこのメソッドを使用できます。 ノードまたはのソースでは、URL で表されるファイルなど、 **Stream**オブジェクト。 すべての変更することを確認する場合、このメソッドを呼び出す必要がありますの内容に加え、 **Stream**書き込まれています。 ただし、ADO を使用した必要はありませんは、通常を呼び出す**フラッシュ**ADO は継続的にバック グラウンドで可能な限り、バッファーをフラッシュします。 コンテンツの変更、 **Stream**キャッシュされないまでに、自動的に行われる**フラッシュ**が呼び出されます。  
  
 閉じる、 **Stream**で、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メソッドの内容をフラッシュ、 **Stream**は自動的に明示的に呼び出す必要はありません**をフラッシュ**直前**閉じる**します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
