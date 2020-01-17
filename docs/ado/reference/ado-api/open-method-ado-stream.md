---
title: Open メソッド (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6549fd10b173a8e133c941ea4315634badb3f35f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917834"
---
# <a name="open-method-ado-stream"></a>Open メソッド (ADO Stream)
開く、 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)バイナリまたはテキスト データのストリームを操作するオブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Source*  
 任意。 A**バリアント**のデータ ソースを指定する値、 **Stream**します。 *ソース*電子メールまたはファイル システムなどのよく知られているツリー構造で既存のノードを指す絶対 URL 文字列を含めることができます。 URL のキーワードを使用して URL を指定する必要があります ("URL =*スキーム*://*server*/*フォルダー*")。 または、*ソース*既に開いているへの参照を含めることができます[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクトに関連付けられている既定のストリームを開き、**レコード**します。 場合*ソース*が指定されていない、 **Stream**はインスタンス化し、開く、既定ではない基になるソースに関連付けられています。 URL スキームと関連するプロバイダーの詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
 *モード*  
 任意。 A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) 、結果として得られるアクセス モードを指定する値**Stream** (たとえば、読み取り/書き込みまたは読み取り専用)。 既定値は**adModeUnknown**します。 参照してください、[モード](../../../ado/reference/ado-api/mode-property-ado.md)アクセス モードの詳細についての詳細については、プロパティ。 場合*モード*が指定されていない、ソース オブジェクトによって継承されます。 たとえば場合、ソース**レコード**は読み取り専用モードで開かれます、 **Stream**既定では読み取り専用モードで開くこともできます。  
  
 *OpenOptions*  
 任意。 A [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)値。 既定値は**adOpenStreamUnspecified**します。  
  
 *UserName*  
 任意。 A**文字列**値が必要な場合にアクセスするユーザー id を含む、 **Stream**オブジェクト。  
  
 *Password*  
 任意。 A**文字列**値が必要な場合にアクセスするパスワードを含む、 **Stream**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 ときに、**レコード**オブジェクトが、ソースのパラメーターとして渡された、 *UserID*と*パスワード*パラメーターを使用しないためへのアクセス、 **レコード**オブジェクトは既に利用可能です。 同様に、[モード](../../../ado/reference/ado-api/mode-property-ado.md)の**レコード**にオブジェクトが転送される、 **Stream**オブジェクト。 ときに*ソース*が指定されていない、 **Stream**開かれたデータが含まれていないとが、[サイズ](../../../ado/reference/ado-api/size-property-ado-stream.md)のゼロ (0)。 これに書き込まれたデータの損失を回避するために**Stream**ときに、 **Stream**が閉じると、保存、 **Stream**で、 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)または[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)メソッド、またはメモリの別の場所に保存します。  
  
 *OpenOptions*の値**adOpenStreamFromRecord**の内容を識別、*ソース*パラメーターは既に開いている**レコード**オブジェクト。 既定の動作を扱う方法が*ソース*ファイルなどのツリー構造内のノードを直接指す URL として。 そのノードに関連付けられている既定のストリームが開かれます。  
  
 中に、 **Stream**が開いていない場合はのすべての読み取り専用プロパティを読み取ること、 **Stream**します。 場合、 **Stream**を開いたすべての後続の操作では、非同期的に (以外のチェック、[状態](../../../ado/reference/ado-api/state-property-ado.md)およびその他の読み取り専用プロパティ) までブロックされます、**オープン**操作が完了するとします。  
  
 オプションを指定しないで、前に説明しただけでなく*ソース*のインスタンスを作成することができます、 **Stream**基になるソースに関連付けることがなくメモリ内のオブジェクト。 バイナリまたはテキスト データを記述することでデータをストリームに動的に追加することができます、 **Stream**で[書き込み](../../../ado/reference/ado-api/write-method.md)または[WriteText](../../../ado/reference/ado-api/writetext-method.md)、またはファイルからデータを読み込んで[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema メソッド](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile メソッド](../../../ado/reference/ado-api/savetofile-method.md)
