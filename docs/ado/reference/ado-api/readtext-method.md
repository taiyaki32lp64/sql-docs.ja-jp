---
title: ReadText メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d6c174d2e6a659a3b9da8f89816b5bdf90342416
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917372"
---
# <a name="readtext-method"></a>ReadText メソッド
指定されたテキストの文字数を読み取ります[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *NumChars*  
 任意。 A**長い**ファイルから読み取る文字の数を指定する値または[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)値。 既定値は**adReadAll**します。  
  
## <a name="return-value"></a>戻り値  
 **ReadText**メソッドは、指定された数の文字、行全体、または全体のストリームからを読み取り、 **Stream**オブジェクトし、結果の文字列を返します。  
  
## <a name="remarks"></a>コメント  
 場合*NumChar*がストリームの左の文字数よりも多い、残りの文字のみが返されます。 指定された長さと一致する文字列の読み取りが行われていない*NumChar*します。 読み取り対象文字がない場合は、バリアントの値は null が返されます。 **ReadText**旧バージョンと読み取りに使用することはできません。  
  
> [!NOTE]
>  **ReadText**メソッドは、テキスト ストリームの使用 ([型](../../../ado/reference/ado-api/type-property-ado-stream.md)は**adTypeText**)。 バイナリ ストリームの (**型**は**adTypeBinary**) を使用して、[読み取り](../../../ado/reference/ado-api/read-method.md)します。  
  
 クエリから返される XML データの量が大きくなる、 **ReadText** ActiveX データ オブジェクト (ADO) Stream オブジェクトのメソッドは、これを行う COM + コンポーネントから呼び出された場合; を実行する時間を大幅にかかる場合があります、ASP ページで、ユーザーのセッション タイムアウトになる可能性があります。ADO から utf-8 エンコードが Unicode; に Stream オブジェクト データを変換します一度に大量のデータの変換に関連するメモリが頻繁に再割り当てが非常に時間がかかります。 を解決することを繰り返し呼び出す、 **ReadText** ADO のメソッド、オブジェクトのコマンドし、より小さい文字数を指定します。 128 K (131,072) と等価の値が最適な表示がテストされます。 この値が減少すると、応答時間が減少します。 詳細については、サポート技術情報記事 280067 を参照してください。"[prb]。ADO のストリーム オブジェクトの ReadText メソッドを使用して SQL Server 2000 から非常に大きな XML ドキュメントを取得する場合があります"、Microsoft サポート技術情報で https://support.microsoft.com します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Read メソッド](../../../ado/reference/ado-api/read-method.md)
