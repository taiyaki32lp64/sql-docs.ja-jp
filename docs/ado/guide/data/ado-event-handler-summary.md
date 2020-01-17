---
title: ADO イベント ハンドラーの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4fef63ff610ad85e353c2ef1dc0f8e5987c74ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926198"
---
# <a name="ado-connection-and-recordset-events"></a>ADO 接続とレコード セットのイベント
ADO の 2 つのオブジェクトは、イベントを発生させることができます。[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトと[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト。 **ConnectionEvent**ファミリに関連で操作する、**接続**オブジェクト、および**RecordsetEvent**ファミリが上の操作に関連、 **レコード セット**オブジェクト。

-   **接続イベント**:接続でトランザクションを開始がコミットされ、またはロールバック時に; イベントが発行されます。ときに、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)実行されます。 警告が発生した場合、**接続イベント**操作です。 または、**接続**開始または終了します。

-   **レコード セットのイベント**:非同期のフェッチ操作の周囲および内の行を移動するときにイベントが発行された、**レコード セット**オブジェクト、行のフィールドを変更、**レコード セット**、内の行を変更、 **レコード セット**、オープン、**レコード セット**、サーバー側カーソルを閉じる、**レコード セット**、または一切のいずれかが変更する、**レコード セット**します。

 次の表は、イベントとその説明をまとめたものです。

|ConnectionEvent|説明|
|---------------------|-----------------|
|[BeginTransComplete、CommitTransComplete、RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**トランザクション管理**-接続の現在のトランザクションが開始すると、通知がコミットまたはロールバックします。|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)、 [ConnectComplete、切断](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**接続の管理**-現在の接続が開始すると、通知が開始または終了しました。|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)、 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**コマンドの実行管理**-接続の現在のコマンドの実行が開始または終了したことを通知します。|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**情報**-現在の操作に関する追加情報があることを通知します。|

|RecordsetEvent|説明|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)、 [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**取得状況**-データの取得操作の進行状況の通知のほか、取得操作が完了したことです。 これらのイベントは使用可能な場合、**レコード セット**クライアント側カーソルを使用して開いた。|
|[WillChangeField、FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**フィールドの変更管理**-現在のフィールドの値は変更または変更されたことを通知します。|
|[WillMove、MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)、 [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**ナビゲーションの管理**-で、現在の行の位置が通知を**レコード セット**変更は、変更がまたはの末尾に達した、**レコード セット**します。|
|[WillChangeRecord、RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**行の変更管理**-の現在の行で何かを通知、 **Recordset** 、変更、または変更しました。|
|[WillChangeRecordset、RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**レコード セットの変更管理**-現在のものを通知**Recordset** 、変更、または変更しました。|

## <a name="see-also"></a>関連項目
 [ADO イベントのインスタンス化言語で](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO イベント](../../../ado/reference/ado-api/ado-events.md)[イベント パラメーター](../../../ado/guide/data/event-parameters.md) [イベント ハンドラーがどのように連携](../../../ado/guide/data/how-event-handlers-work-together.md)[イベントの種類](../../../ado/guide/data/types-of-events.md)
