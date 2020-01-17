---
title: SaveToFile メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2e56178ad306d5b39c2445c391c3bbabe4fc424
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917034"
---
# <a name="savetofile-method"></a>SaveToFile メソッド
バイナリ コンテンツを保存、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)ファイル。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>パラメーター  
 *FileName*  
 A**文字列**先ファイルの完全修飾名を含む値の内容、 **Stream**が保存されます。 有効なローカルの場所に保存できますか、任意の場所に UNC の値を使用してアクセスが。  
  
 *SaveOptions*  
 A [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)によって新しいファイルを作成するかどうかを指定する値**SaveToFile**が既に存在しない場合、します。 既定値は**adSaveCreateNotExists**します。 これらのオプションでは、指定したファイルが存在しない場合にエラーが発生したことを指定できます。 指定することもできます**SaveToFile**既存のファイルの現在の内容が上書きされます。  
  
> [!NOTE]
>  既存のファイルを上書きする場合 (と**adSaveCreateOverwrite**設定されている)、 **SaveToFile**新しいに続く元の既存のファイルからバイトを切り捨てます[EOS](../../../ado/reference/ado-api/eos-property.md)します。  
  
## <a name="remarks"></a>コメント  
 **SaveToFile**の内容のコピーに使用できる、 **Stream**オブジェクトをローカル ファイルにします。 内容、またはプロパティの変更はありません、 **Stream**オブジェクト。 **Stream**オブジェクトが呼び出す前に開く必要があります**SaveToFile**します。  
  
 このメソッドの関連付けを変更していない、 **Stream**基になるソース オブジェクト。 **Stream**オブジェクトは元の URL に関連付けされますまたは**レコード**開かれたときにそのソースでした。  
  
 後に、 **SaveToFile**操作、現在の位置 ([位置](../../../ado/reference/ado-api/position-property-ado.md))、ストリームでは (0) のストリームの先頭に設定します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)
