---
title: CacheSize を使用する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2e3a67e9ad0f1f26f804ecb38e960041863fad9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923576"
---
# <a name="using-cachesize"></a>CacheSize を使用する
使用して、 **CacheSize**プロバイダーからのローカル メモリに一度に取得するレコードの数を制御するプロパティ。 たとえば場合、 **CacheSize** 10 が、最初に開く、**レコード セット**オブジェクト、プロバイダーがローカル メモリに最初の 10 個のレコードを取得します。 間を移動し、 **Recordset**オブジェクト、プロバイダーがローカル メモリ バッファーからデータを返します。 過去のキャッシュの最後のレコードを移動するとすぐに、プロバイダーは、キャッシュにデータ ソースから、次の 10 個のレコードを取得します。  
  
> [!NOTE]
>  **CacheSize**に基づいて、**開ける行の最大**プロバイダー固有のプロパティ (で、**プロパティ**のコレクション、 **Recordset**オブジェクト)。 設定することはできません**CacheSize**より大きい値に**開いている行の最大数。** プロバイダーで開くことができる行の数を変更するには、設定**開ける行の最大**します。  
  
 値**CacheSize**の有効期間中に調整できる、**レコード セット**データ ソースから次に、キャッシュ内のレコードの数にのみ影響、オブジェクトがこの値を変更します。 単独でプロパティ値を変更する場合は、キャッシュの現在の内容は変更されません。  
  
 も取得するレコードが少ない場合**CacheSize**を示す、プロバイダーは、残りのレコードを返し、エラーは発生しません。  
  
 A **CacheSize**ゼロに設定は許可されていませんし、エラーが返されます。  
  
 キャッシュから取得したレコードには、他のユーザーがソース データに対する同時変更は反映されません。 キャッシュされたすべてのデータの更新プログラムを強制的には、使用、[再同期](../../../ado/reference/ado-api/resync-method.md)メソッド。  
  
 場合**CacheSize**ナビゲーション方法 1 より大きい値に設定されます ([移動](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst、MoveLast、MoveNext、MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) へのナビゲーションを削除された可能性がありますレコードを取得した後、削除が発生した場合に記録します。 最初のフェッチ後に以降の削除は反映されませんデータ キャッシュ内の削除された行のデータ値にアクセスを試みるまで。 ただし、設定**CacheSize**を 1 に削除された行をフェッチできないためにこの問題を排除します。
