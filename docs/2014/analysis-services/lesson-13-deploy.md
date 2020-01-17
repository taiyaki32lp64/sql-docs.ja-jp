---
title: レッスン 14:展開 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96ffa6445d46f1e68efa907330d0945a499bf3b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079136"
---
# <a name="lesson-14-deploy"></a>レッスン 14:配置
  このレッスンでは、配置プロパティを構成します。具体的には、テーブル モードで実行されている Analysis Services の配置サーバー インスタンスと、配置するモデルの名前を指定します。 その後、そのインスタンスにモデルを配置します。 配置が完了すると、ユーザーはレポート クライアント アプリケーションを使用してモデルに接続できるようになります。 詳細については、[「テーブル モデル ソリューションの配置 (SSAS テーブル)」](tabular-models/tabular-model-solution-deployment-ssas-tabular.md)を参照してください。  
  
 このレッスンを完了するまでに時間を推定するには。**5 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 13:Excel で分析](lesson-12-analyze-in-excel.md)します。  
  
## <a name="deploy-the-model"></a>モデルの配置  
  
#### <a name="to-configure-deployment-properties"></a>配置プロパティを構成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] の**ソリューション エクスプローラー**で、**Adventure Works Internet Sales Tabular Model** プロジェクトを右クリックし、コンテキスト メニューの **[プロパティ]** をクリックします。  
  
2.  **[AW Internet Sales Tabular Model プロパティ ページ]** ダイアログ ボックスで、 **[配置サーバー]** の **[サーバー]** プロパティに、テーブル モードで実行されている Analysis Services インスタンスの名前を入力します。 これが、モデルの配置先のインスタンスになります。  
  
    > [!IMPORTANT]  
    >  配置を行うには、リモート Analysis Services インスタンスに対する管理権限が必要です。  
  
3.  確認、**クエリ モード**プロパティに設定されて**インメモリ**します。  
  
    > [!NOTE]  
    >  このチュートリアルを使用して作成されたモデルは、DirectQuery モードではサポートされません。  
  
4.  **データベース**プロパティに「`Adventure Works Internet Sales Model`します。  
  
5.  **キューブ**名前プロパティに「`Adventure Works Internet Sales Model`します。  
  
6.  選択内容を確認し、 **[OK]** をクリックします。  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Adventure Works Internet Sales テーブル モデルを配置するには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で、 **[ビルド]** メニューをクリックし、 **[AW Internet Sales Tabular Model の配置]** をクリックします。  
  
     [配置] ダイアログ ボックスが表示され、メタデータの配置状況と、モデルに含まれる各テーブルが表示されます。  
  
## <a name="conclusion"></a>まとめ  
 おめでとうございます! 最初の Analysis Services テーブル モデルの作成と配置が完了しました。 このチュートリアルでは、テーブル モデルを作成する際の、最も一般的なタスクについて説明しました。 Adventure Works Internet Sales Model が配置されたので、SQL Server Management Studio を使用してモデルを管理したり、プロセス スクリプトやバックアップ計画を作成できるようになりました。 ユーザーは、Microsoft Excel や [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] などのレポート クライアント アプリケーションを使用して、モデルに接続できます。  
  
## <a name="additional-resources"></a>その他のリソース  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] レポートをサポートするテーブル モデル プロパティの詳細については、[「Power View レポート プロパティ (SSAS テーブル)」](tabular-models/properties-ssas-tabular.md) を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [DirectQuery モード &#40;SSAS テーブル&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [既定のデータ モデルと配置プロパティの構成 &#40;SSAS テーブル&#41;](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [表形式モデルのデータベース (SSAS 表形式)](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
