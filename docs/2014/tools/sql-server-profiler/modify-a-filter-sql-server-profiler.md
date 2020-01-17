---
title: Modify a Filter (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db6d6220fbb0f756b539e63dc2496d9ddb46d9f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228492"
---
# <a name="modify-a-filter-sql-server-profiler"></a>フィルターの変更 (SQL Server Profiler)
  トレース定義を保持するトレース テンプレートにフィルターを追加して、トレースで収集するイベントの数を制限します。 収集するイベントの数を制限すると、トレースによるパフォーマンスの影響を軽減できます。 トレース テンプレートにフィルターを設定していても、そのトレースで必要な種類の情報が収集されていないことが判明した場合は、そのフィルターを編集できます。  
  
### <a name="to-modify-a-filter"></a>フィルターを変更するには  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で、変更するトレース フィルターのテンプレートを開きます。 **[ファイル]** メニューの **[テンプレート]** をポイントし、 **[テンプレートの編集]** をクリックします。  
  
2.  **[トレース テンプレートのプロパティ]** ダイアログ ボックスの **[全般]** タブで、 **[テンプレート名の選択]** ボックスの一覧からテンプレートを選択します。  
  
3.  **[イベントの選択]** タブをクリックします。  
  
     **[イベントの選択]** タブにはグリッド コントロールがあります。 グリッド コントロールは、トレース可能な各イベント クラスを含んでいるテーブルです。 このテーブルには、各イベント クラスが 1 行で表示されます。 イベント クラスは、接続先のサーバーの種類やバージョンによって多少異なる場合があります。 イベント クラスは、グリッドの **[イベント]** 列で識別され、イベント カテゴリ別に分類されています。 残りの列には、各イベント クラスに対応するデータ列が表示されます。  
  
4.  **[列フィルター]** をクリックします。  
  
5.  **[フィルターの編集]** ダイアログ ボックスで、編集する比較演算子に対応した値をクリックし、新しい値を入力するか、既存の値を削除します。 また、新しいフィルターを追加することもできます。  
  
6.  **[OK]** をクリックしてテンプレートを保存します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
