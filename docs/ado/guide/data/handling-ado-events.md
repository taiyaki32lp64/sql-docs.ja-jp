---
title: ADO イベントの処理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 452259b6e4e406d7a406211a9e9b42ebbf60da53
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925224"
---
# <a name="handling-ado-events"></a>ADO イベントの処理
ADO イベント モデルを発行する特定同期および非同期 ADO 操作をサポートしています*イベント*、または、操作を開始する前に、または完了後に、通知します。 イベントは、実際には、アプリケーションで定義するイベント ハンドラー ルーチンの呼び出しです。  
  
 グループの操作を開始する前に発生するイベントのハンドラー関数またはプロシージャを指定する場合は、確認または操作に渡されたパラメーターを変更できます。 まだ実行されていないが、ため、操作を取り消すかを完了することを許可します。  
  
 操作の完了後に発生するイベントは、非同期的に ADO を使用する場合に特に重要です。 たとえば、非同期に開始するアプリケーション[Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)操作には、操作の終了時の実行完了イベントで通知します。  
  
 ADO イベント モデルを使用して、アプリケーションにいくつかのオーバーヘッドを追加しますが、監視などの非同期操作の処理の他の方法よりはるかに柔軟性を提供します、[状態](../../../ado/reference/ado-api/state-property-ado.md)ループが発生するオブジェクトのプロパティ。  
  
> [!NOTE]
>  イベントを処理するために、ADO は、メッセージ ポンプまたはシングル スレッド アパートメント (STA) モデルで使用する必要があります。 ADO イベントは、非表示のウィンドウを作成して内部的に処理されます。 ADO では、イベントを発生させる必要がある場合に、このウィンドウにメッセージを送信します。 呼び出したスレッドにイベントが送信されることを確認します。 これは、 **iconnectionpoint::advise**接続ポイント。 このアーキテクチャで、通知を受け取る必要のあるスレッドがウィンドウ メッセージをポンプしていないときに、問題が生じる場合があります。 潜在的な問題には、スレッドとタイムアウトになっていると、システム全体をダウン遅くなる可能性があります、非表示のウィンドウでは、メッセージを処理しないため、グローバル ウィンドウ ブロードキャストに配信されない ADO イベントが含まれます。 STA スレッドでは、実行されているため、この問題は見られません STA スレッドでメッセージ ポンプ通常があります。 MTA スレッド、ただし、通常ありませんメッセージ ポンプ、問題は、通常現れます MTA スレッドのため。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [イベントの種類](../../../ado/guide/data/types-of-events.md)  
  
-   [イベント パラメーター](../../../ado/guide/data/event-parameters.md)  
  
-   [複数のイベント ハンドラーの連携方法](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [言語別の ADO イベントのインスタンス化](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>関連項目  
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [言語で ADO イベントのインスタンス化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO イベント](../../../ado/reference/ado-api/ado-events.md)   
 [イベント パラメーター](../../../ado/guide/data/event-parameters.md)   
 [イベントの種類](../../../ado/guide/data/types-of-events.md)
