---
title: SSMS 出力ウィンドウ | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Output Window [SQL Server Management Studio]
- Activity Monitor [SQL Server Management Studio]
- Object Explorer [SQL Server Management Studio]
ms.assetid: a2ce1a07-b4e2-471c-87d2-b8de5e6c6864
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cee27bc499a00fc77dd022ffa6c29f0173a2a571
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262234"
---
# <a name="output-window-in-sql-server-management-studio"></a>SQL Server Management Studio の出力ウィンドウ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
出力ウィンドウは、[表示] メニューから開くことも、Ctrl + Alt + O キーの組み合わせを使用して開くこともできます。 複数の出力チャネルが使用できます。

次の表に、各出力チャネルに関連付けられている各種メッセージの概要を示します。

|Channel|[説明]|
|-----------|---------------|  
|**テレメトリ**|テレメトリは、Microsoft によって収集された[匿名機能の使用状況データ](sql-server-management-studio-ssms.md)のストリームです。 これらのイベントは、SSMS の使用状況を独自に記録する場合に役立つ可能性があります。 展開したオブジェクト エクスプローラー ノードと、出力ウィンドウが開いていたとき SSMS セッション中に実行したコマンドを容易に特定することができます。|
|**[オブジェクト エクスプローラー]**|このチャネルでは、オブジェクト エクスプローラーでノードを展開するのに必要とされる SQL クエリのクエリ テキストと経過時間を出力します。 各クエリは、クエリの開始およびクエリの終了イベントを記録します。 各イベントには、クエリ対象のエンティティに関連付けられたタイムスタンプと URN が含まれています。 [URN](https://technet.microsoft.com/library/microsoft.sqlserver.management.smo.urn(v=sql.90).aspx) は基になる SQL 管理オブジェクトを参照し、XPath スタイル階層で構成されます。 たとえば、サーバー "MyServer" 上のデータベース "Db" の "Table1" という名前のテーブルの URN の場合は、"Server[@Name='MyServer']/Database[@Name='Db']/Table[/@Name='Table1']" となります。 オブジェクト エクスプローラーで 1 つのノードを展開すると、このようなクエリを複数、それぞれ異なるパラメーターで実行することができます。 クエリの終了イベントには、TSQL テキストと共にクエリの経過時間が含まれます。 オブジェクト エクスプローラーが特定のノードを展開するのにいつもより時間がかかるような場合、このクエリ データがサーバー パフォーマンスの分析に有用な場合があります。 **注** - 展開時にオブジェクト エクスプローラー内のすべてのノードが、このレベルの詳細なクエリを提供するわけではありません。|
|**利用状況モニター**|このチャネルは、サーバーに対して[利用状況モニターが開く](https://docs.microsoft.com/sql/relational-databases/performance-monitor/activity-monitor)と開始されます。 このストリームには、各クエリのクエリ テキストおよびタイムスタンプ、エラー メッセージ、および接続の問題のため一時停止中のモニターの通知を部分的に示すイベントが含まれています。 利用状況モニターがアイドル状態、あるいは更新されない状況にあると思われる場合、詳細については、この出力チャネルを確認してください。|





