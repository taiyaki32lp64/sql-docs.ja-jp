---
title: フィルターの変更 (SQL Server プロファイラー) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ee101f13c7856b2701a02d1446a0ad8e5a4e2d24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074905"
---
# <a name="modify-a-filter-sql-server-profiler"></a>フィルターの変更 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
