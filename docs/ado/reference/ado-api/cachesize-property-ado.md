---
title: CacheSize プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6b33ef7eb4bae796fa2b2da59a7b1dc805d739e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920330"
---
# <a name="cachesize-property-ado"></a>CacheSize プロパティ (ADO)
レコードの数を示す、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)メモリにローカルにキャッシュされたオブジェクト。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**長い**値 0 より大きい必要があります。 既定値は 1 です。  
  
## <a name="remarks"></a>コメント  
 使用して、 **CacheSize**プロバイダーからのローカル メモリに一度に取得するレコードの数を制御するプロパティ。 たとえば場合、 **CacheSize** 10 が、最初に開く、**レコード セット**オブジェクト、プロバイダーがローカル メモリに最初の 10 個のレコードを取得します。 間を移動し、 **Recordset**オブジェクト、プロバイダーがローカル メモリ バッファーからデータを返します。 過去のキャッシュの最後のレコードを移動するとすぐに、プロバイダーは、キャッシュにデータ ソースから、次の 10 個のレコードを取得します。  
  
> [!NOTE]
>  **CacheSize**に基づいて、**開ける行の最大**プロバイダー固有のプロパティ (で、**プロパティ**のコレクション、 **Recordset**オブジェクト)。 設定することはできません**CacheSize**より大きい値に**開ける行の最大**します。 開くことができます、プロバイダーによって行の数を変更するには、次のように設定します。**開ける行の最大**します。  
  
 値**CacheSize**の有効期間中に調整できる、**レコード セット**データ ソースから次に、キャッシュ内のレコードの数にのみ影響、オブジェクトがこの値を変更します。 単独でプロパティ値を変更する場合は、キャッシュの現在の内容は変更されません。  
  
 も取得するレコードが少ない場合**CacheSize**を示す、プロバイダーは、残りのレコードを返し、エラーは発生しません。  
  
 A **CacheSize**ゼロに設定は許可されていませんし、エラーが返されます。  
  
 キャッシュから取得したレコードには、他のユーザーがソース データに対する同時変更が反映されていません。 キャッシュされたすべてのデータの更新プログラムを強制的には、使用、[再同期](../../../ado/reference/ado-api/resync-method.md)メソッド。  
  
 場合**CacheSize** 1 ナビゲーション メソッドよりも大きい値に設定されます ([移動](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst、MoveLast、MoveNext、MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) へのナビゲーションで発生する可能性があります、レコードを取得した後、削除が発生した場合、レコードが削除されます。 最初のフェッチ後に以降の削除は反映されませんデータ キャッシュ内の削除された行のデータ値にアクセスを試みるまで。 ただし、設定**CacheSize**いずれかに削除された行をフェッチできないために、この問題を排除します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [CacheSize プロパティの例 (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize プロパティの例 (vc++)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize プロパティの例 (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
