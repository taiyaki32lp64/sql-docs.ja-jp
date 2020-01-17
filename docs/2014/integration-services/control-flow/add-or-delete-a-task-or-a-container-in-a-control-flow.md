---
title: 制御フローのタスクまたはコンテナーを追加または削除する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f13db8a1e22c88c4433cd8928479a6ed1af540f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833137"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>制御フローのタスクまたはコンテナーを追加または削除する
  制御フロー デザイナーでの作業中、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーのツールボックスには、パッケージの制御フローの作成用に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で用意されているタスクが一覧表示されます。 ツールボックスの詳細については、「 [SSIS ツールボックス](../ssis-toolbox.md)」を参照してください。  
  
 1 つのパッケージには、同じタスクのインスタンスを複数含めることができます。 タスクの各インスタンスは、パッケージ内で一意に識別され、各インスタンスは個別に構成できます。  
  
 タスクを削除すると、そのタスクを制御フロー内の別のタスクやコンテナーに連結する優先順位制約も、同様に削除されます。  
  
 次の手順では、パッケージの制御フローのタスクまたはコンテナーを追加または削除する方法について説明します。  
  
### <a name="to-add-a-task-or-a-container-to-a-control-flow"></a>制御フローにタスクまたはコンテナーを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  **[ツールボックス]** を開くには、 **[表示]** メニューの **[ツールボックス]** をクリックします。  
  
5.  **[制御フロー項目]** と **[メンテナンス タスク]** を展開します。  
  
6.  タスクとコンテナーを、 **[ツールボックス]** から **[制御フロー]** タブのデザイン画面にドラッグします。  
  
7.  パッケージの制御フロー内のタスクまたはコンテナーのコネクタをドラッグし、タスクまたはコンテナーを制御フロー内の別のコンポーネントに連結します。  
  
8.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-delete-a-task-or-a-container-from-a-control-flow"></a>制御フローからタスクまたはコンテナーを削除するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。 次のいずれかの操作を行います。  
  
    -   **[制御フロー]** タブをクリックし、削除するタスクまたはコンテナーを右クリックして **[削除]** をクリックします。  
  
    -   **パッケージ エクスプローラー**を開きます。 **[実行可能ファイル]** フォルダーで削除するタスクまたはコンテナーを右クリックし、 **[削除]** をクリックします。  
  
3.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [Integration Services コンテナー](integration-services-containers.md)   
 [[制御フロー]](control-flow.md)  
  
  
