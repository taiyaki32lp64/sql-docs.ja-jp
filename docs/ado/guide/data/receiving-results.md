---
title: 結果の受信 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b861553e9a71ce56377f8d87bba0f9e26e929c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924522"
---
# <a name="receiving-results"></a>結果の受信
ADO ではほとんどのコマンドは、呼び出し元に返される情報はいくつかの結果します。 行セットを返すコマンドの結果を受信してで、**レコード セット**でおそらく、最も使用されている ADO オブジェクトのあるオブジェクト。  
  
 いくつかの方法でデータを受信する、 **Recordset**次の呼び出しなど、データ ソースからのオブジェクト。  
  
-   [Connection.Execute メソッド](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Execute メソッド](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open メソッド](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 内のデータの受信、**レコード セット**オブジェクトでの参加で、データの取得のプロセスは終了です、**接続**オブジェクトと**コマンド**オブジェクトを暗黙的にまたは明示的にします。 一般的なクライアント/サーバー アプリケーション システムでのデータの取得のプロセス全体が必要ですラウンド トリップ ネットワーク経由で入力ごとに**Recordset**します。  
  
 カプセル化されている各データ セットのいずれかと、ネットワーク経由でいくつかのようにすることになることを意味ラウンド トリップを 1 つ以上の結果セットが表示される、 **Recordset**オブジェクト。 低速または混雑しているネットワークでは、ラウンド トリップの数を減らすことに役立つアプリケーションのパフォーマンスを向上します。 一部のプロバイダーが複数の受信のサポートを提供するそのため、 **Recordset**1 回のラウンド トリップで s。 これは、次のトピックについて説明します。  
  
-   [複数のレコードセットの受信](../../../ado/guide/data/receiving-multiple-recordsets.md)
