---
title: "制御フローのタスクまたはコンテナーを追加または削除する | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "コンテナー [Integration Services], 追加"
  - "タスクの追加"
  - "コンテナーの追加"
  - "タスク [Integration Services], 追加"
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# 制御フローのタスクまたはコンテナーを追加または削除する
  制御フロー デザイナーでの作業中、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーのツールボックスには、パッケージの制御フローの作成用に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で用意されているタスクが一覧表示されます。 ツールボックスの詳細については、「[SSIS ツールボックス](../../integration-services/ssis-toolbox.md)」を参照してください。  
  
 1 つのパッケージには、同じタスクのインスタンスを複数含めることができます。 タスクの各インスタンスは、パッケージ内で一意に識別され、各インスタンスは個別に構成できます。  
  
 タスクを削除すると、そのタスクを制御フロー内の別のタスクやコンテナーに連結する優先順位制約も、同様に削除されます。  
  
 次の手順では、パッケージの制御フローのタスクまたはコンテナーを追加または削除する方法について説明します。  
  
### 制御フローにタスクまたはコンテナーを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  **[ツールボックス]** を開くには、**[表示]** メニューの **[ツールボックス]** をクリックします。  
  
5.  **[制御フロー項目]** と **[メンテナンス タスク]** を展開します。  
  
6.  タスクとコンテナーを、**[ツールボックス]** から **[制御フロー]** タブのデザイン画面にドラッグします。  
  
7.  パッケージの制御フロー内のタスクまたはコンテナーのコネクタをドラッグし、タスクまたはコンテナーを制御フロー内の別のコンポーネントに連結します。  
  
8.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### 制御フローからタスクまたはコンテナーを削除するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。 次のいずれかの操作を行います。  
  
    -   **[制御フロー]** タブをクリックし、削除するタスクまたはコンテナーを右クリックして **[削除]** をクリックします。  
  
    -   **パッケージ エクスプローラー**を開きます。 **[実行可能ファイル]** フォルダーで削除するタスクまたはコンテナーを右クリックし、**[削除]** をクリックします。  
  
3.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## 参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services コンテナー](../../integration-services/control-flow/integration-services-containers.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  