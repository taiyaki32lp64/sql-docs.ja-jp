---
title: CopyTo メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25d57116e1fa24658d62a0c9083e00a3e320d2a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933372"
---
# <a name="copyto-method-ado"></a>CopyTo メソッド (ADO)
指定した数の文字またはバイトのコピー (に応じて[型](../../../ado/reference/ado-api/type-property-ado-stream.md)) で、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)間**Stream**オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DestStream*  
 オブジェクト変数の値をオープンへの参照を含む**Stream**オブジェクト。 現在**Stream**先にコピーが**Stream**で指定された*DestStream*します。 宛先**Stream**開く必要があります。 そうでない場合は、実行時エラーが発生します。  
  
> [!NOTE]
>  *DestStream*パラメーターでのプロキシができない可能性があります**Stream**オブジェクトのプライベート インターフェイスへのアクセスが要求されるため、 **Stream**オブジェクトをリモート処理は実行することはできません、クライアント。  
  
 *NumChars*  
 任意。 **整数**バイトまたはソース内の現在位置からコピーする文字の数を指定する値**Stream**先に**Stream**します。 既定値は-1 で、すべての文字またはバイト数を現在の位置からコピーされるように指定[EOS](../../../ado/reference/ado-api/eos-property.md)します。  
  
## <a name="remarks"></a>コメント  
 このメソッドは文字またはバイト単位で指定された現在の位置からの指定した数をコピー、[位置](../../../ado/reference/ado-api/position-property-ado.md)プロパティ。 指定した数が利用できるまでのバイト数よりも多い場合**EOS**、し、文字またはバイトのみに現在位置から**EOS**コピーされます。 場合の値*NumChars* -1 で、または省略すると、すべての文字または現在位置から始まるバイトをコピーします。  
  
 文字またはコピー先のストリームにバイトを既存は、コピーの終了時点より前のすべての内容は残りますが、およびは切り捨てられていません。 **位置**バイトをコピーする最後のバイトの直後になります。 これらのバイトを切り捨てる場合は、呼び出す[SetEOS](../../../ado/reference/ado-api/seteos-method.md)します。  
  
 **CopyTo**先のデータをコピーするために使用する必要があります**Stream**ソースと同じ型の**Stream** (その**型**プロパティの設定は両方**adTypeText**またはその両方**adTypeBinary**)。 テキストの**Stream**オブジェクトを変更することができます、 [Charset](../../../ado/reference/ado-api/charset-property-ado.md)プロパティの設定、変換先の**Stream**別に設定する 1 つの文字から変換します。 また、テキスト**Stream**オブジェクトをバイナリに正常にコピーできる**Stream**オブジェクトではなくバイナリ**Stream**テキストにオブジェクトをコピーすることはできません**Stream**オブジェクト。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
