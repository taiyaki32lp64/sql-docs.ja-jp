---
title: 準備とコマンドの実行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2295d421f8b802f2f3b531d7de3fc086e43ad572
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924560"
---
# <a name="preparing-and-executing-commands"></a>準備とコマンドの実行
コマンドは、基になるデータ ソースに対していくつかの操作を実行するプロバイダーに発行する手順です。 たとえば、SQL ステートメントは、Microsoft SQL データ プロバイダーにコマンドです。 ADO では、コマンドは通常によって表される**コマンド**オブジェクトからのシンプルなコマンドを発行することもが**接続**または**レコード セット**オブジェクト。  
  
 使用することができます、**コマンド**プロバイダーがコマンド文字列を正しく解釈できることと仮定すると、プロバイダーからサポートされているあらゆる種類の操作を要求するオブジェクト。 データ プロバイダーの一般的な操作がデータベースを照会して、レコードを取得するには、 **Recordset**オブジェクトで、結果と、結果を表示するためのツールを保持するコンテナーとして考えることができます。 ADO オブジェクトの多くといくつか**コマンド**オブジェクトのコレクション、メソッド、またはプロパティは、プロバイダーの機能に応じて、参照したときにエラーを生成可能性があります。  
  
 使用するだけでなく**コマンド**オブジェクトを使用することができます、 **Execute**メソッドを**接続**オブジェクトまたは**オープン**メソッド**レコード セット**コマンドを発行して、それを実行するオブジェクト。 ただし、使用する必要があります、**コマンド**オブジェクトのコードでのコマンドを再利用する必要がある場合、または、コマンドを使用してパラメーターの詳細な情報を渡す必要がある場合。 これらのシナリオについては、このセクションの後半で説明しています。  
  
> [!NOTE]
>  特定**コマンド**s は、1 つとして、またはバイナリ ストリームとしての設定の結果を返すことができます**レコード**ではなく同様、**レコード セット**これは、プロバイダーによってサポートされて 場合。 また、いくつか**コマンド**s は結果セットのすべての (たとえば、SQL Update クエリ) を返すものでありません。 このセクションでは、最も一般的なシナリオをただしに説明します。 実行**コマンド**s として結果を返す、**レコード セット**オブジェクト。 結果を返すの詳細については**レコード**s または**Stream**s を参照してください[レコードとストリーム](../../../ado/guide/data/records-and-streams.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Command オブジェクトの概要](../../../ado/guide/data/command-object-overview.md)  
  
-   [簡単なコマンドの作成と実行](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command オブジェクトのパラメーター](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Command を使用してストアド プロシージャを呼び出す](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [接続オブジェクトのメソッドとしてストアド プロシージャの呼び出し](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [名前付きコマンド](../../../ado/guide/data/named-commands.md)  
  
-   [名前付きコマンドにパラメーターを渡す](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
