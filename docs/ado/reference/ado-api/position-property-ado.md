---
title: Position プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dba8636f07b88f1c05d465b844376c6ef3e61240
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931654"
---
# <a name="position-property-ado"></a>Position プロパティ (ADO)
内の現在位置を示す、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**長い**ストリームの先頭から現在の位置のバイト数でオフセットを指定する値。 既定では 0 で、ストリーム内の最初のバイトを表します。  
  
## <a name="remarks"></a>コメント  
 現在の位置は、ストリームの終了後、ポイントに移動できます。 現在のストリームの末尾を越える位置を指定する場合、[サイズ](../../../ado/reference/ado-api/size-property-ado-stream.md)の**Stream**オブジェクトがそれに応じて増加します。 この方法で追加された新しいバイトは、null になります。  
  
> [!NOTE]
>  **位置**常にバイトを測定します。 テキスト ストリームはマルチバイト文字セットを使用して、位置の文字数を決定する、文字のサイズを乗算します。 たとえば、2 バイト文字セットでは、最初の文字は、位置 0、2、3 番目の文字の位置にある 2 番目の文字位置 4、具合が。  
  
> [!NOTE]
>  負の値を使用しての現在の位置を変更することはできません、 **Stream**します。 正の数値のみを使用できる**位置**します。  
  
> [!NOTE]
>  読み取り専用**Stream**オブジェクトの場合は、ADO はエラーを返しません。**位置**より大きい値に設定されて、**サイズ**の、 **Stream**します。 サイズは変わりません、 **Stream**、alter、または、 **Stream**何らかの方法でコンテンツ。 ただし、これを行う避ける必要がありますので、意味のない**位置**値。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Charset プロパティ (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
