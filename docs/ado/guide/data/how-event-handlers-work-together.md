---
title: イベント ハンドラーの連携 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b744dbd464aedbd9b87d22aa74277787fcc3c7a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925049"
---
# <a name="how-event-handlers-work-together"></a>複数のイベント ハンドラーの連携方法
Visual Basic でのすべてのイベント ハンドラーでプログラミングしている場合を除き、**接続**と**Recordset**かどうか実際に処理するすべてのイベントに関係なく、イベントを実装する必要があります。 行う必要がある実装の作業の量は、使用するプログラミング言語に依存します。 詳細については、次を参照してください。[言語で ADO イベントのインスタンス化](../../../ado/guide/data/ado-event-instantiation-by-language.md)します。  
  
## <a name="paired-event-handlers"></a>1 対のイベント ハンドラー  
 各はイベント ハンドラーが関連付けられている**完了**イベント ハンドラー。 アプリケーションが、フィールドの値に変更されたときに、たとえば、 **WillChangeField**イベント ハンドラーが呼び出されます。 変更が許容される場合は、アプリケーションのまま、 **adStatus**パラメーターが変更されず、操作を実行します。 操作の完了時、 **FieldChangeComplete**イベントは、アプリケーション、操作が完了したことを通知します。 場合は、正常に完了した**adStatus**が含まれています**adStatusOK**、それ以外の**adStatus**を含む**adStatusErrorsOccurred**と確認する必要があります、**エラー**エラーの原因を特定するオブジェクト。  
  
 ときに**WillChangeField**が呼び出されるとなるように、変更が適用されませんする必要があります。 この場合は、 **adStatus**に**adStatusCancel します。** 操作が取り消されると、 **FieldChangeComplete**イベントを受け取る、 **adStatus**の値**adStatusErrorsOccurred**。 **エラー**オブジェクトを含む**adErrOperationCancelled**ように、 **FieldChangeComplete**ハンドラーは、操作がキャンセルされたことを認識します。 ただしの値を確認する必要があります、 **adStatus**パラメーターを設定するために、それを変更する前に**adStatus**に**adStatusCancel**パラメーターが設定されている場合は、効果がありません**adStatusCantDeny**プロシージャへのエントリにします。  
  
 場合があります操作は、1 つ以上のイベントを発生させることができます。 たとえば、**レコード セット**オブジェクトがイベントをペアになって**フィールド**変更と**レコード**変更します。 アプリケーションでの値が変更されたとき、**フィールド**、 **WillChangeField**イベント ハンドラーが呼び出されます。 操作を続行になっていることを判断した場合、 **WillChangeRecord**イベント ハンドラーにも発生します。 このハンドラーは、引き続きイベントも許可している場合は、変更、および**FieldChangeComplete**と**RecordChangeComplete**イベント ハンドラーが呼び出されます。 特定の操作がイベント ハンドラーが呼び出される順序は定義されませんハンドラーを呼び出すことで、特定のシーケンスが依存するコードを記述しないようにします。  
  
 インスタンスはの複数のイベントが発生した場合は、保留中の操作インストールをキャンセル イベントのいずれかの可能性があります。 アプリケーションがの値に変更されたときに、たとえば、**フィールド**の両方を**WillChangeField**と**WillChangeRecord**イベント ハンドラーは通常呼び出されます。 ただし、それに関連付けられた最初イベント ハンドラーで、操作が取り消されたかどうか**完了**ハンドラーがすぐにという**adStatusOperationCancelled**します。 2 番目のハンドラーは呼び出されません。 ただし、最初のイベント ハンドラーは、イベントの続行を許可している場合は、その他のイベント ハンドラーが呼び出されます。 場合は、操作をキャンセルし、両方とも**完了**前の例のように、イベントが呼び出されます。  
  
## <a name="unpaired-event-handlers"></a>対になっていないイベント ハンドラー  
 イベントがない状態に渡される限り**adStatusCantDeny**を返すことによって、イベントのイベント通知をオフにできます**adStatusUnwantedEvent**で、*状態*パラメーター。 たとえば、ときに、**完了**返すことができますイベント ハンドラーは、初めて呼び出されると、 **adStatusUnwantedEvent**します。 のみを受信後**は**イベント。 ただし、1 つ以上の理由で一部のイベントをトリガーできます。 その場合は、イベントが必要があります、*理由*パラメーター。 戻ったら**adStatusUnwantedEvent**、その特定の理由で発生した場合にのみ、そのイベントの通知の受信を停止できます。 つまり、イベントが発生する可能性が考えられる各理由の通知を受け取るは可能性のあります。  
  
 1 つ**は**操作で使用されるパラメーターを確認するときに、イベント ハンドラーが役に立ちます。 これらの操作パラメーターを変更したり、操作をキャンセルできます。  
  
 または、**完了**イベント通知を有効にします。 最初はイベント ハンドラーが呼び出されると、返す**adStatusUnwantedEvent**します。 のみを受信後**完了**イベント。  
  
 1 つ**完了**イベント ハンドラーが非同期操作の管理に役立つことができます。 各非同期操作が適切な**完了**イベント。  
  
 大規模な入力に長い時間がかかることなど[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 開始することができます、アプリケーションが適切に書き込まれる場合、`Recordset.Open(...,adAsyncExecute)`操作し、その他の処理を続行します。 いずれときの通知、**レコード セット**によって設定されますが、 **ExecuteComplete**イベント。  
  
## <a name="single-event-handlers-and-multiple-objects"></a>1 つのイベント ハンドラーと複数のオブジェクト  
 Microsoft Visual C++® などのプログラミング言語の柔軟性を使用すると、複数のオブジェクトからのイベント ハンドラー プロセス イベントがあることができます。 たとえば、1 つがある可能性があります**切断**イベント ハンドラーがイベントをいくつか処理**接続**オブジェクト。 接続のいずれかが終了した場合、**切断**イベント ハンドラーが呼び出されます。 指示するため、対応するイベント ハンドラー オブジェクトのパラメーターを設定すると、どの接続がイベントを発生させた**接続**オブジェクト。  
  
> [!NOTE]
>  この手法は、その言語は、イベント ハンドラーを 1 つのオブジェクトを関連付けることができるため、Visual Basic では使用できません。  
  
## <a name="see-also"></a>参照  
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [言語で ADO イベントのインスタンス化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [イベント パラメーター](../../../ado/guide/data/event-parameters.md)   
 [イベントの種類](../../../ado/guide/data/types-of-events.md)
