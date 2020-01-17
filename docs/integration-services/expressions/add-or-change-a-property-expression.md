---
title: プロパティ式を追加または変更する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], creating
- expressions [Integration Services], property expressions
ms.assetid: cb5da499-065f-4fa6-9f6d-5bc5f385241e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f3aef5f587e590dcad0ab0490679a480529387a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290500"
---
# <a name="add-or-change-a-property-expression"></a>プロパティ式を追加または変更する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  パッケージ、タスク、Foreach ループ コンテナー、For ループ コンテナー、シーケンス コンテナー、イベント ハンドラー、パッケージおよびプロジェクト レベルの接続マネージャー、およびログ プロバイダーに対してプロパティ式を作成できます。  
  
 プロパティ式を作成または変更するには、 **[プロパティ式エディター]** か **[式ビルダー]** を使用します。 **[プロパティ式エディター]** には、タスクおよびコンテナーで使用可能なカスタム エディターか、 **[プロパティ]** ウィンドウからアクセスできます。 **[式ビルダー]** には、 **[プロパティ式エディター]** 内からアクセスできます。 **[プロパティ式エディター]** または **[式ビルダー]** のいずれかで式を作成することができますが、 **[式ビルダー]** には、複雑な式の作成を容易にするグラフィカル ツール セットが備わっています。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が提供する構文、演算子、および関数の詳細については、「[ &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)」および「[ &#40;SSIS 式&#41;](../../integration-services/expressions/functions-ssis-expression.md)」を参照してください。 各演算子または関数のトピックには、式で演算子や関数を使用する例が含まれます。 複雑な式の例については、「 [パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)」を参照してください。  
  
### <a name="to-create-or-change-a-property-expression"></a>プロパティ式を作成または変更するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージが含まれているプロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開き、次のいずれかの操作を行います。  
  
    -   アイテムがタスクまたはコンテナーの場合は、アイテムをダブルクリックし、エディターの **[式]** をクリックします。  
  
    -   アイテムを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[式]** ボックス内でクリックし、省略記号 [...] をクリックします。  
  
4.  **[プロパティ式エディター]** で、 **[プロパティ]** ボックスの一覧からプロパティを選択し、次のいずれかの操作を行います。  
  
    -   **[式]** 列で直接プロパティ式を入力するか変更し、 **[OK]** をクリックします。  
  
         \- または -  
  
    -   プロパティの式の行の省略記号 [...] をクリックし、 **[式ビルダー]** ダイアログ ボックスを開きます。  
  
5.  (省略可能) **[式ビルダー]** での次のタスクのいずれかを実行します。  
  
    -   システム変数およびユーザー定義変数にアクセスするには、 **[変数]** を展開します。  
  
    -   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 式言語で提供される関数、キャスト、および演算子にアクセスするには、 **[数学関数]** 、 **[文字列関数]** 、 **[日付/時刻関数]** 、 **[NULL 関数]** 、 **[型キャスト]** 、および **[演算子]** を展開します。  
  
    -   **[式ビルダー]** で式を作成または変更するには、変数、列、関数、演算子、およびキャストを **[式]** ボックスにドラッグするか、または式をボックスに入力します。  
  
    -   式の評価結果を表示するには、 **[式ビルダー]** の **[式の評価]** をクリックします。  
  
         式が有効でない場合は、式の構文エラーを示す警告が出力されます。  
  
        > [!NOTE]  
        >  式の評価を行っても、評価結果はプロパティに割り当てられません。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; 式](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Integration Services &#40;SSIS&#41; パッケージ](../../integration-services/integration-services-ssis-packages.md)   
 [Integration Services コンテナー](../../integration-services/control-flow/integration-services-containers.md)   
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services &#40;SSIS&#41; のイベント ハンドラー](../../integration-services/integration-services-ssis-event-handlers.md)   
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Integration Services &#40;SSIS&#41; のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
