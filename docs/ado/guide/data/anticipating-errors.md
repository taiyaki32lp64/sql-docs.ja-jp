---
title: エラーの予測 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d92d96e3b8cdfea5cacea35d852e8859de65dbd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925980"
---
# <a name="anticipating-errors"></a>エラーの予測
エラーの防止は、少なくともエラー処理と同程度に重要です。 この最後のセクションには、エラーが発生する可能性が低くするため、アプリケーションがかかるの予防措置の短い一覧が含まれています。  
  
 値をチェックして、オブジェクトの状態を確認、**状態**プロパティ オブジェクトを使用して、操作を実行する前にします。 例では、アプリケーションがグローバルに使用する場合の**接続**、確認、**状態**プロパティを呼び出す前に開いているかどうかには既に参照してください、**を開く**メソッド。  
  
-   任意のプログラムをユーザーからのデータを受け入れるには、データ ストアに送信する前にそのデータを検証するコードを含める必要があります。 データ ストア、プロバイダー、ADO、または問題の通知も使用するプログラミング言語に依存できません。 データは、そのフィールドの種類が正しいことと、必要なフィールドが空ではないことを確認、ユーザーが入力したすべてのバイト数を確認する必要があります。  
  
 データ ストアにデータを記述する前に、データを確認します。 これを行う最も簡単な方法は、処理するためには、 **WillMove**イベントまたは**WillUpdateRecordset**イベント。 ADO イベントの処理の詳細については、次を参照してください。 [ADO イベントの処理](../../../ado/guide/data/handling-ado-events.md)します。  
  
 確認します**Recordset**の境界外のオブジェクトが、**レコード セット**レコード ポインターを移動する前にします。 しようとする場合**MoveNext**とき**EOF** true または**MovePrev**とき**BOF** true の場合は、エラーが発生します。 いずれかを実行する場合、**移動**メソッドと両方**EOF**と**BOF** True は、エラーが生成されます。  
  
 などの操作を実行しようとする場合に、エラーも発生は**シーク**と**検索**、空で**Recordset**します。
