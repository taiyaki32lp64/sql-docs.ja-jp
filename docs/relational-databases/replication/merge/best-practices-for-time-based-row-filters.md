---
title: 時間ベースの行フィルターの推奨事項 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- best practices
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6182b480c83b8e6b2d0f0a50217823fd14f30c30
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033355"
---
# <a name="best-practices-for-time-based-row-filters"></a>時間ベースの行フィルターの推奨事項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  アプリケーションのユーザーは、テーブルに対して時間ベースのデータ サブセットを要求することがよくあります。 たとえば、販売員が先週の注文データを必要としたり、イベント プランナーが次週のイベントのデータを必要とする場合などです。 多くの場合、アプリケーションでは、 **GETDATE()** 関数を含むクエリを使用して、この処理を実行します。 次の行フィルター ステートメントについて考えてみましょう。  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 このタイプのフィルターを使用すると、マージ エージェントの実行時には、2 つの処理 (このフィルターに適合する行をサブスクライバーにレプリケートする処理と、このフィルターに適合しない行をサブスクライバー側でクリーンアップする処理) が常に発生すると推測するのが普通です (**HOST_NAME()** によるフィルター処理の詳細については、「[パラメーター化された行フィルター](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」を参照してください。)ところがマージ レプリケーションでは、データに対して行フィルターをどのように定義したかに関係なく、前回の同期以降に変更されたデータのレプリケートおよびクリーンアップのみが行われます。  
  
 マージ レプリケーションで行を処理するには、行内のデータが行フィルターに適合していて、前回の同期以降にデータが変更されている必要があります。 **SalesOrderHeader** テーブルでは、行が挿入されると **OrderDate** が入力されます。 挿入はデータ変更なので、行は、期待どおりにサブスクライバーにレプリケートされます。 ただし、フィルターに適合しなくなった行 (7 日前以前の注文の行) がサブスクライバー側にある場合、他のなんらかの理由で更新されていない限り、その行はサブスクライバーから削除されません。  
  
 イベント プランナーの事例では、このようなフィルター処理に伴う問題がさらに強く浮き彫りになります。 **Events** テーブルに対する次のフィルターについて考えてみましょう。  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 イベントを格納しているテーブルでは、イベント当日のかなり前に挿入が行われることがあります。 次週のイベントの挿入が 1 か月前に行われ、別の理由で行が更新されなかった場合、行フィルターに適合していても、行はサブスクライバーにレプリケートされません。  
  
 また、パブリケーションの構成方法によって、マージ レプリケーションがフィルターを評価するタイミングはさまざまです。  
  
-   パブリケーションが事前計算済みパーティションを使用している場合 (既定)、行の挿入時および更新時に、フィルターが評価されます。  
  
-   パブリケーションが事前計算済みパーティションを使用していない場合、マージ エージェントの実行時に、フィルターが評価されます。  
  
 事前計算済みパーティションの詳細については、[事前計算済みパーティションによるパラメーター化されたフィルター パフォーマンスの最適化](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)に関するページを参照してください。 フィルターが評価されるタイミングは、どのデータがフィルターに適合するかということに影響します。 たとえば、パブリケーション側で事前計算済みパーティションが使用されており、2 日ごとにデータを同期する場合、販売員のデータのサブセットには、予期した日付よりも最高 2 日分古い行が含まれている可能性があります。  
  
## <a name="recommendations-for-using-time-based-row-filters"></a>時間ベースの行フィルターを使用するための推奨事項  
 次に示す方法は、時間に基づいてフィルター処理を行う際の強力でわかりやすいアプローチです。  
  
-   テーブルに、データ型 **bit**の列を追加する。 この列は、行をレプリケートするかどうかを示すために使用します。  
  
-   時間ベースの列ではなく新しい列を参照する行フィルターを使用する。  
  
-   スケジュールでマージ エージェントが実行される前に列を更新する SQL Server エージェント ジョブ (または別のメカニズムでスケジュールされたジョブ) を作成する。  
  
 この方法を使用すると、 **GETDATE()** などの時間ベースの方法を使用した場合の欠点を補い、パーティションに対してフィルターが評価されるタイミングを決める問題を回避できます。 **Events** テーブルの次の例を考えてみましょう。  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**[レプリケート]**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|1|  
|2|Dinner|112|2006-10-10|0|  
|3|Party|112|2006-10-11|0|  
|4|Wedding|112|2006-10-12|0|  
  
 このテーブルの行フィルターは、次のようになります。  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 SQL Server エージェント ジョブは、各マージ エージェントを実行する前に、次のような [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを実行できます。  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 1 行目では、 **Replicate** 列を **0**に再設定しています。2 行目では、今後 7 日以内に発生するイベントの列を **1** に設定しています。 この [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントが 2006 年 10 月 7 日に実行されると、テーブルが次のように更新されます。  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**[レプリケート]**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|0|  
|2|Dinner|112|2006-10-10|1|  
|3|Party|112|2006-10-11|1|  
|4|Wedding|112|2006-10-12|1|  
  
 次週のイベントは、レプリケート準備済みとしてフラグが付けられています。 イベント コーディネーター 112 が使用するサブスクリプションでマージ エージェントが次に実行されると、1 行目以外の行がサブスクライバーにダウンロードされ、1 行目がサブスクライバーから削除されます。  
  
## <a name="see-also"></a>参照  
 [GETDATE (Transact-SQL)](../../../t-sql/functions/getdate-transact-sql.md)   
 [ジョブの実装](../../../ssms/agent/implement-jobs.md)   
 [パラメーター化された行フィルター](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
