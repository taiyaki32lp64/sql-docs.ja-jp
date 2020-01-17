---
title: コンテキスト接続
description: コンテキスト接続について説明します。
ms.date: 08/15/2019
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: b5ebd0b1b7357a385507d1ab528adde4023092da
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452268"
---
# <a name="the-context-connection"></a>コンテキスト接続

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

内部データへのアクセスに関する問題は、ごく一般的なものです。 内部データにアクセスすることは、CLR (共通言語ランタイム) ストアド プロシージャや関数を実行しているサーバーへのアクセスを考えることです。 これを実現する 1 つの選択肢として、<xref:Microsoft.Data.SqlClient.SqlConnection> を使用して接続を作成し、ローカル サーバーを指す接続文字列を指定して、接続を開く方法があります。 これには、ログインのための資格情報を指定することが必要になります。 接続が、ストアド プロシージャや関数とは別のデータベース セッションにある場合、`SET` オプションが異なっている場合、別のトランザクションに存在している場合、一時テーブルを認識しない場合なども考えられます。 マネージド ストアド プロシージャや関数のコードが SQL Server プロセスで実行されているということは、だれかがそのサーバーに接続して、マネージド コードを呼び出す SQL ステートメントを実行したことを意味します。 このような場合、その接続のコンテキストで、その接続のトランザクションや `SET` オプションと共存する形で、ストアド プロシージャまたは関数を実行することを考えます。 これを "コンテキスト接続" と呼びます。  
  
コンテキスト接続を使用すると、コードを最初に呼び出したのと同じコンテキストで Transact-SQL ステートメントを実行することができます。 詳細については、「SQL Server オンラインブックからの[コンテキスト接続](https://go.microsoft.com/fwlink/?LinkId=115395)」を参照してください。
