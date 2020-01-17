---
title: コマンド オブジェクトの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef68a36f64fbaf72f18af9fba6f2e2781422574c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925857"
---
# <a name="command-object-overview"></a>Command オブジェクトの概要
**コマンド**オブジェクトを次を行うことができます。  
  
-   使用して (たとえば、SQL ステートメントまたはストアド プロシージャ) コマンドの実行可能ファイルのテキストを定義、 **CommandText**プロパティ。  
  
-   使用してパラメーター化クエリまたはストアド プロシージャの引数を定義する**パラメーター**オブジェクトと**パラメーター**コレクション。  
  
-   コマンドを実行し、返す、 **Recordset**オブジェクト、該当する場合を使用して、 **Execute**メソッド。  
  
-   使用してコマンドの種類を指定、 **CommandType**パフォーマンスを最適化するために実行する前にプロパティ。  
  
-   使用して、コマンド テキストに関する特定の情報を指定、**言語**のプロパティ、**コマンド**オブジェクト。  
  
-   プロバイダーを使用して実行する前に、コマンドの準備済み (またはコンパイル済み) のバージョンを保存するかどうかを制御、**準備**プロパティ。  
  
-   プロバイダーがコマンドを使用して実行を待機する秒数を設定、 **CommandTimeout**プロパティ。  
  
-   開いている接続を関連付ける、**コマンド**オブジェクトを設定してその**ActiveConnection**プロパティ。  
  
-   設定、**名前**プロパティを識別するために、**コマンド**オブジェクトに関連付けられているメソッドとして**接続**オブジェクト。  
  
-   渡す、**コマンド**オブジェクトを**ソース**のプロパティを**レコード セット**データを取得するためにします。  
  
-   渡す、 **Stream**コマンド (たとえば、XML コマンド) をサポートしているプロバイダーに格納しているオブジェクト。
