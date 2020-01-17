---
title: 'SQL Server: SQL Statistics オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:SQL Statistics
- SQL Statistics object
ms.assetid: da7dbb4b-f632-45a0-b1ab-c35cc2695c86
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 7841fef89ae4eb0600dcc62c1561bff769500a47
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995654"
---
# <a name="sql-server-sql-statistics-object"></a>SQL Server: SQL Statistics オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **SQLServer:SQL Statistics** オブジェクトには、コンパイルの動作や、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに送信された要求の種類を監視するためのカウンターが用意されています。 クエリのコンパイルと再コンパイルの回数、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが受信するバッチの数を監視すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がユーザー クエリを処理する速度や、クエリ オプティマイザーによるクエリ処理の効果がわかります。  
  
 コンパイルは、クエリのターンアラウンド時間の大半を占めます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、コンパイルのコストを節約するために、コンパイル済みのクエリ プランがクエリ キャッシュに保存されます。 キャッシュを使用して、コンパイル済みのクエリを再使用のために保存すると、後から実行するときに再コンパイルの必要がなくなるので、コンパイルを減らすことができます。 ただし、一意のクエリはすべて、少なくとも 1 回コンパイルする必要があります。 クエリの再コンパイルは、次の要因によって生じることがあります。  
  
-   テーブルへの列またはインデックスの追加など、ベース スキーマの変更を含むスキーマの変更、またはテーブルに大量の行を挿入したり、テーブルから大量の行を削除することなどの統計スキーマの変更。  
  
-   環境 (SET ステートメント) の変更。 ANSI_PADDING や ANSI_NULLS などのセッション設定の変更によって、クエリが再コンパイルされることがあります。  
  
 簡易パラメーター化と強制パラメーター化の詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Statistics** カウンターを次に示します。  
  
|SQL Server SQL Statistics カウンター|[説明]|  
|----------------------------------------|-----------------|  
|**Auto-Param Attempts/sec**|1 秒あたりの自動パラメーター化が実行された数。 総数は、失敗した試行、安全な試行、および安全ではない試行の合計でなければなりません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにより、いくつかのリテラルをパラメーターに置き換えることによって [!INCLUDE[tsql](../../includes/tsql-md.md)] 要求のパラメーター化が試行されると、自動パラメーター化が発生します。複数の類似した要求で、結果としてキャッシュされた実行プランの再使用を可能にするためです。 自動パラメーター化は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新しいバージョンでは簡易パラメーター化とも呼ばれています。 このカウンターには、強制パラメーター化は含まれません。|  
|**Batch Requests/sec**|1 秒あたりに受信した [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドのバッチの数。 この統計値はすべての制約の影響を受けます。制約とは、I/O、ユーザー数、キャッシュ サイズ、要求の複雑さなどです。 バッチ要求の数が多いことは、スループットが優れていることを意味します。|  
|**Failed Auto-Params/sec**|1 秒あたりの失敗した自動パラメーター化を実行した回数。 これは小さな値でなければなりません。 自動パラメーター化は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の最新バージョンでは簡易パラメーター化とも呼ばれています。|  
|**Forced Parameterizations/sec**|強制パラメーター化に成功した 1 秒あたりの回数。|  
|**Guided Plan Executions/sec**|プラン ガイドを使用してクエリ プランが生成された、1 秒あたりのプラン実行回数。|  
|**Misguided Plan Executions/sec**|プランの生成中にプラン ガイドが適用できなかった、1 秒あたりのプラン実行回数。 このプラン ガイドは無視され、通常のコンパイルを使用して実行済みプランが生成されています。|  
|**Safe Auto-Params/sec**|1 秒あたりの安全な自動パラメーター化を実行した回数。 安全とは、キャッシュされた実行プランを、さまざまな類似する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント間で共有できるという判断のことを言います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 多くの自動パラメーター化が試行され、そのうちのいくつかは安全という結果になり、その他は安全ではないという結果になります。 自動パラメーター化は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の最新バージョンでは簡易パラメーター化とも呼ばれています。 これには、強制的なパラメーター化は含まれません。|  
|**SQL Attention rate**|1 秒あたりのアテンションの数。 アテンションは、現在実行している要求を終了するために、クライアントから要求されます。|  
|**SQL Compilations/sec**|1 秒あたりの SQL コンパイルの回数。 コンパイル コード パスが入力された回数を示します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のステートメントレベルの再コンパイルによって発生したコンパイル回数を含みます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のユーザー利用状況が安定化すると、この値は定常状態に到達します。|  
|**SQL Re-Compilations/sec**|1 秒あたりのステートメントの再コンパイル回数。 ステートメントの再コンパイルがトリガーされた回数をカウントします。 一般に、再コンパイルは少なくする必要があります。|  
|**Unsafe Auto-Params/sec**|1 秒あたりの安全でない自動パラメーター化の回数。 たとえば、クエリには、キャッシュされたプランを共有できないいくつかの特性があります。 これらは、安全ではないと見なされています。 これは、強制パラメーター化の数としてはカウントされません。|  
  
## <a name="see-also"></a>参照  
 [SQL Server の Plan Cache オブジェクト](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
