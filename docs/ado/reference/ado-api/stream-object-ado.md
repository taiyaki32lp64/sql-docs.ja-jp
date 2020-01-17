---
title: Stream オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c70a22a3048c769aac343d51e621e4d755d3baeb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916720"
---
# <a name="stream-object-ado"></a>Stream オブジェクト (ADO)
バイナリ データまたはテキストのストリームを表します。  
  
 ファイル システムや、電子メール システムなどのツリー構造の階層で、[レコード](../../../ado/reference/ado-api/record-object-ado.md)ファイルや電子メールの内容を含む既定のバイナリ関連付けられているビット ストリームがあります。 A **Stream**オブジェクトは、これらのデータ ストリームを含むフィールドやレコードを操作するために使用できます。 A **Stream**オブジェクトは、次の方法で取得できます。  
  
-   バイナリまたはテキスト データを格納しているオブジェクト (通常はファイル) を指す URL。 このオブジェクトは、単純なドキュメント、**レコード**構造のドキュメントまたはフォルダーを表すオブジェクト。  
  
-   既定値を開いて**Stream**オブジェクトに関連付けられている、**レコード**オブジェクト。 関連付けられている既定のストリームを取得することができます、**レコード**オブジェクトと、**レコード**ストリームを開くだけへのラウンドト リップの排除を開きます。  
  
-   インスタンス化して、 **Stream**オブジェクト。 これら**Stream**アプリケーションの目的でデータを格納するオブジェクトを使用できます。 異なり、 **Stream** URL、または既定値に関連付けられている**Stream**の**レコード**、インスタンス化された**Stream**との関連付けを持たない、既定では基になるソース。  
  
 メソッドとプロパティの使用、 **Stream**オブジェクトを次を行うことができます。  
  
-   開く、 **Stream**オブジェクトから、**レコード**または URL を[オープン](../../../ado/reference/ado-api/open-method-ado-stream.md)メソッド。  
  
-   閉じる、 **Stream**で、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メソッド。  
  
-   入力バイトまたはテキストを**Stream**で、[書き込み](../../../ado/reference/ado-api/write-method.md)と[WriteText](../../../ado/reference/ado-api/writetext-method.md)メソッド。  
  
-   バイトを読み取り、 **Stream**で、[読み取り](../../../ado/reference/ado-api/read-method.md)と[ReadText](../../../ado/reference/ado-api/readtext-method.md)メソッド。  
  
-   いずれかを記述**Stream** 、ADO ではまだデータ バッファーを基になるオブジェクトへ、[フラッシュ](../../../ado/reference/ado-api/flush-method-ado.md)メソッド。  
  
-   内容をコピー、 **Stream**間**Stream**で、 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)メソッド。  
  
-   ソース ファイルから行を読み取る方法を制御、 [SkipLine](../../../ado/reference/ado-api/skipline-method.md)メソッドと[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)プロパティ。  
  
-   ストリームの位置での最後の判断、 [EOS](../../../ado/reference/ado-api/eos-property.md)プロパティと[SetEOS](../../../ado/reference/ado-api/seteos-method.md)メソッド。  
  
-   保存し、ファイル内のデータの復元、 [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)と[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)メソッド。  
  
-   格納するために使用する文字セットの指定、 **Stream**で、 [Charset](../../../ado/reference/ado-api/charset-property-ado.md)プロパティ。  
  
-   非同期の中止**Stream**と操作、[キャンセル](../../../ado/reference/ado-api/cancel-method-ado.md)メソッド。  
  
-   内のバイト数を決定する**Stream**で、[サイズ](../../../ado/reference/ado-api/size-property-ado-stream.md)プロパティ。  
  
-   内の現在位置を制御する**Stream**で、[位置](../../../ado/reference/ado-api/position-property-ado.md)プロパティ。  
  
-   内のデータの種類を決定する**Stream**で、[型](../../../ado/reference/ado-api/type-property-ado-stream.md)プロパティ。  
  
-   現在の状態を判断、 **Stream** (閉じる、開くには、またはを実行する) で、[状態](../../../ado/reference/ado-api/state-property-ado.md)プロパティ。  
  
-   指定のアクセス モード、 **Stream**で、[モード](../../../ado/reference/ado-api/mode-property-ado.md)プロパティ。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
 **Stream**オブジェクトがスクリプトを実行します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Stream オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [レコードとストリーム](../../../ado/guide/data/records-and-streams.md)
