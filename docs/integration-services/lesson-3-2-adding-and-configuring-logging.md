---
title: 手順 2:ログ記録の追加および構成 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e2b43837de8617af559e2a810c89115e5a3963d3
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283270"
---
# <a name="lesson-3-2-add-and-configure-logging"></a>レッスン 3-2:ログ記録の追加および構成

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



ここでは、Lesson 3.dtsx パッケージのデータ フローのログを有効にします。 次に、PipelineExecutionPlan イベントと PipelineExecuteTrees イベントを記録するテキスト ファイル ログ プロバイダーを構成します。 テキスト ファイル ログ プロバイダーによって、表示や移行が容易なログが作成されます。 パッケージの基本テスト段階では、ログ ファイルのこのような簡潔性が便利です。 ログ エントリは、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[ログ イベント]** ウィンドウでも確認できます。  
  
## <a name="add-logging-to-the-package"></a>パッケージにログ機能を追加する  
  
1.  **[SSIS]** メニューの **[ログ記録]** を選択します。  
  
2.  **[SSIS ログの構成]** ダイアログの **[コンテナー]** ウィンドウで、一番上のパッケージ オブジェクトが選択されていることを確認します。 このオブジェクトはレッスン 3 のパッケージを表します。
  
3.  **[プロバイダーとログ]** タブで、 **[プロバイダーの種類]** ボックスの一覧から **[テキスト ファイルの SSIS ログ プロバイダー]** を選択し、 **[追加]** を選択します。  
  
    新しいテキスト ファイル ログ プロバイダーがパッケージに追加されます。このプロバイダーの既定の名前は "**テキスト ファイルの SSIS ログ プロバイダー**" です。 次に、この新しいログ プロバイダーを構成します。  
  
4.  **[名前]** 列に「**Lesson 3 Log File**」と入力します。  
  
5.  必要に応じて、 **[説明]** の内容を修正します。  
  
6.  **[構成]** 列で、 **[\<新しい接続>]** を選択し、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] がログ情報を書き込む場所を指定します。  
  
    **[ファイル接続マネージャー エディター]** ダイアログ ボックスで、 **[使用法の種類]** ボックスの一覧から **[ファイルの作成]** を選択し、 **[参照]** を選択します。 既定では、 **[ファイルの選択]** ダイアログにこのプロジェクトのフォルダーが表示されますが、ログ情報を別の場所に保存することもできます。  
  
7.  **[ファイルの選択]** ダイアログで、 **[ファイル名]** ボックスに「**TutorialLog.log**」と入力し、 **[開く]** を選択します。
  
8.  **[OK]** を選択して、 **[ファイル接続マネージャー エディター]** ダイアログを閉じます。  
  
9. **[コンテナー]** ペインで、パッケージ コンテナー階層のすべてのノードを展開します。次に、 **[Extract Sample Currency Data]** チェック ボックスも含めすべてのチェック ボックスをオフにします。 次に、このノードのイベントのみを取得するため、 **[Extract Sample Currency Data]** チェック ボックスをオンにします。  
  
    > [!NOTE]  
    > **[Extract Sample Currency Data]** チェック ボックスがオフの状態で淡色表示になっている場合は、親コンテナーのログ設定が使用され、この作業用にログ イベントを有効にすることはできません。 これを解決するには、親のチェック ボックスをオフにします。
  
10. **[詳細]** タブの **[イベント]** 列で、 **[PipelineExecutionPlan]** イベントと **[PipelineExecutionTrees]** イベントのチェック ボックスをオンにします。  
  
11. **[詳細設定]** を選択し、各イベントについて書き込まれるログ情報の詳細を確認します。 既定では、指定したイベントについて、すべての情報カテゴリが自動的に選択されます。  
  
12. **[標準]** を選択し、情報カテゴリを非表示にします。  
  
13. **[プロバイダーとログ]** タブで、 **[名前]** 列の **[Lesson 3 Log File]** をクリックします。 目的のパッケージのログ プロバイダーを作成したら、必要に応じてログの記録をオフにすることができます。ログ プロバイダーを削除し、再作成する必要はありません。  
  
14. **[OK]** を選択します。  
  
## <a name="go-to-next-task"></a>次の実習に進む  
[手順 3:レッスン 3 のパッケージのテスト](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
