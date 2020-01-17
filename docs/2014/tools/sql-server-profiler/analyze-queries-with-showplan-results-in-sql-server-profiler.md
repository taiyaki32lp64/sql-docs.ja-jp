---
title: SQL Server Profiler での Showplan 結果を使用したクエリの分析 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], Showplan
- Profiler [SQL Server Profiler], Showplan results
- SQL Server Profiler, Showplan results
ms.assetid: 6a2f7727-141c-4f59-8613-2e452bc78467
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0eb13d2997c9b2b29c85489f30a161a96f64c70c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211106"
---
# <a name="analyze-queries-with-showplan-results-in-sql-server-profiler"></a>SQL Server Profiler での Showplan 結果を使用したクエリの分析
  Showplan イベント クラスをトレース定義に追加することで、クエリ プランに関する情報を [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のトレースで収集して表示できます。 また、トレースで収集した他のイベントから Showplan イベントを抽出し、これらの Showplan イベントを個別の XML ファイルに保存することもできます。  
  
 トレースから Showplan イベントを抽出するために使用できる方法は、次のとおりです。  
  
-   トレースの構成時に、 **[イベント抽出の設定]** タブを使用する。このタブは、 **[イベントの選択]** タブでいずれかの Showplan イベントを選択するまで表示されないことに注意してください。  
  
-   **[ファイル]** メニューの **[SQL Server イベントの抽出]** オプションを使用する。  
  
-   特定のイベントを右クリックして **[イベント データの抽出]** をクリックすることにより、個々のイベントを抽出して保存します。  
  
## <a name="showplan-events"></a>Showplan イベント  
 次の表に、各種の Showplan トレース イベントとその説明を示します。  
  
|イベント名|説明|  
|----------------|-----------------|  
|**Performance statistics**|コンパイル済みの Showplan が初めてキャッシュされたとき、再コンパイルされたとき、およびプラン キャッシュから削除されたときを示します。 **TextData** 列には、XML 形式の Showplan が含まれます。 詳細については、「 [Performance Statistics イベント クラス](../../relational-databases/event-classes/performance-statistics-event-class.md)」を参照してください。|  
|**Showplan All**|実行された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのコンパイルに関する完全な詳細情報が含まれたクエリ プランを表示します。 たとえば、コストの見積りと列リストを表示できます。 詳細については、「 [Showplan All イベント クラス](../../relational-databases/event-classes/showplan-all-event-class.md)」を参照してください。|  
|**Showplan All For Query Compile**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でクエリがコンパイルまたは再コンパイルされたときに発生します。 このイベントは、 **Showplan All** イベントに相当するコンパイル時のイベントです。 **Showplan All** イベントは、クエリが実行されたときに発生します。 **Showplan All For Query Compile** イベントは、クエリがコンパイルされたときに発生します。 詳細については、「 [Showplan All for Query Compile イベント クラス](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)」を参照してください。|  
|**Showplan Statistics Profile**|各操作で渡される実際の行数など、実行されている [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行時の完全な詳細情報が含まれたクエリ プランを表示します。 詳細については、「 [Showplan Statistics Profile イベント クラス](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)」を参照してください。|  
|**Showplan Text**|実行されている [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのクエリ プラン ツリーをバイナリ データとして表示します。 詳細については、「 [Showplan Text イベント クラス](../../relational-databases/event-classes/showplan-text-event-class.md)」を参照してください。|  
|**Showplan Text (Unencoded)**|実行されている [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのクエリ プラン ツリーをテキストとして表示します。 このイベント クラスでは、バイナリ データではなくテキストが表示されるという点を除いては、Showplan Text と同じ情報が表示されます。 詳細については、「[Showplan Text &#40;Unencoded&#41; イベント クラス](../../relational-databases/event-classes/showplan-text-unencoded-event-class.md)」を参照してください。|  
|**Showplan XML**|クエリの最適化中に収集された完全なデータが含まれたクエリ プランを表示します。 このイベントは、クエリ プランが最適化されたときに生成されます。 詳細については、「 [Showplan XML イベント クラス](../../relational-databases/event-classes/showplan-xml-event-class.md)」を参照してください。|  
|**Showplan XML For Query Compile**|クエリがコンパイルされたときにクエリ プランを表示します。 詳細については、「 [Showplan XML for Query Compile イベント クラス](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)」を参照してください。|  
|**Showplan XML Statistics Profile**|実行時の完全な詳細情報が含まれたクエリ プランを XML 形式で表示します。 たとえば、このイベント クラスでは、実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの各操作に渡される行数をキャプチャします。 詳細については、「 [Showplan XML Statistics Profile イベント クラス](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)」を参照してください。|  
  
## <a name="see-also"></a>関連項目  
 [Performance イベント カテゴリ](../../relational-databases/event-classes/performance-event-category.md)  
  
  
