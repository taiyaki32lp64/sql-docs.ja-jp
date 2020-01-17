---
title: 手順 4:パッケージにデータ フロー タスクを追加する | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a98437a88fc81d83c98ec2c3417df6d38bc1b421
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283822"
---
# <a name="lesson-1-4-add-a-data-flow-task-to-the-package"></a>レッスン 1-4:データ フロー タスクをパッケージに追加する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



移動元データおよび異動先データに対する接続マネージャーを作成した後は、パッケージにデータ フロー タスクを追加します。 データ フロー タスクでは、移動元と移動先の間でデータを移動するデータ フロー エンジンが定義されており、移動するデータの変換、クリーニング、修正を行う機能が提供されています。 抽出、変換、読み込み (ETL) プロセスのほとんどが、このデータ フロー タスクで実行されます。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、データ フローと制御フローが切り離されています。  
  
## <a name="add-a-data-flow-task"></a>データ フロー タスクを追加する  
  
1.  **[制御フロー]** タブを選択します。  
  
2.  **[SSIS ツールボックス]** ペインで **[お気に入り]** を展開し、 **[データ フロー タスク]** を **[制御フロー]** タブのデザイン画面上にドラッグします。  
  
    > [!NOTE]  
    > SSIS ツールボックスが表示されていない場合は、 **[SSIS]** メニューを選択してから、 **[SSIS ツールボックス]** を選択して SSIS ツールボックスを表示します。  

3.  **[制御フロー]** デザイン画面で、新しい**データ フロー タスク**を右クリックし、 **[名前の変更]** を選択して、名前を「**Extract Sample Currency Data**」に変更します。  
  
    デザイン画面に追加するすべてのコンポーネントに一意な名前を付けます。 使いやすさと管理しやすさを考慮し、各コンポーネントの機能がわかるような名前を付けます。 このような方法で名前を付けておけば、自己文書化された [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを作成できます。 パッケージを文書化するには、注釈を使用する方法もあります。 注釈の詳細については、「[パッケージで注釈を使用する](../integration-services/use-annotations-in-packages.md)」を参照してください。  
  
4.  データ フロー タスクを右クリックして **[プロパティ]** を選択し、[プロパティ] ウィンドウで **LocaleID** プロパティが **[英語 (米国)]** に設定されていることを確認します。  
  
## <a name="go-to-next-task"></a>次のタスクに進む
[手順 5:フラット ファイルの変換元を追加し、構成する](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>参照  
[データ フロー タスク](../integration-services/control-flow/data-flow-task.md)  
  
  
  
