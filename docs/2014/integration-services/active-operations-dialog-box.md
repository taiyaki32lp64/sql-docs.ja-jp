---
title: アクティブな操作 ダイアログ ボックス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f930a2e6f3ce84c330a4b7292ebaaba3b2ab871e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062221"
---
# <a name="active-operations-dialog-box"></a>[アクティブな操作] ダイアログ ボックス
  配置、検証、パッケージの実行など、 **サーバー上で現在実行中の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 操作の状態を表示するには、** [アクティブな操作][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ダイアログ ボックスを使用します。 このデータは、SSISDB カタログに格納されます。  
  
 関連 [!INCLUDE[tsql](../includes/tsql-md.md)] ビューの詳細については、「[catalog.operations (SSISDB データベース)](/sql/integration-services/system-views/catalog-operations-ssisdb-database)」、「[catalog.validations (SSISDB データベース)](/sql/integration-services/system-views/catalog-validations-ssisdb-database)」、「[catalog.executions (SSISDB データベース)](/sql/integration-services/system-views/catalog-executions-ssisdb-database)」を参照してください。  
  
 **目的に合ったトピックをクリックしてください**  
  
1.  [[アクティブな操作] ダイアログ ボックスを開く](#open_dialog)  
  
2.  [オプションの構成](#options)  
  
##  <a name="open_dialog"></a> [アクティブな操作] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]を開きます。  
  
2.  Microsoft SQL Server データベース エンジンに接続します。  
  
3.  オブジェクト エクスプローラーで、 **[Integration Services]** ノードを展開します。 **[SSISDB]** を右クリックし、 **[アクティブな操作]** をクリックします。  
  
##  <a name="options"></a> オプションの構成  
  
### <a name="options"></a>および  
 **型**  
 操作の種類を指定します。 可能な値を次に、**型**フィールドと、TRANSACT-SQL の operations_type 列に対応する値`catalog.operations`ビュー。  
  
|||  
|-|-|  
|Integration Services の初期化|1|  
|操作のクリーンアップ (SQL エージェント ジョブ)|2|  
|プロジェクト バージョンのクリーンアップ (SQL エージェント ジョブ)|3|  
|プロジェクトの配置|101|  
|プロジェクトの復元|106|  
|パッケージ実行の作成および開始|200|  
|操作の停止 (検証または実行の停止)|202|  
|プロジェクトの検証|300|  
|パッケージの検証|301|  
|カタログの構成|1000|  
  
 **[停止]**  
 現在実行中の操作を停止する場合にクリックします。  
  
  
