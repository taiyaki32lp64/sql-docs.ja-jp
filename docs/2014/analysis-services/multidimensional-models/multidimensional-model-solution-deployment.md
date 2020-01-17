---
title: 多次元モデル ソリューションの配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, planning
- deploying [Analysis Services]
- deploying [Analysis Services], planning
ms.assetid: 7259c201-ff54-43e8-bda5-a6d51474e0e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ec674c1eb64f2e5191df600864fa38aa3da0749
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073550"
---
# <a name="multidimensional-model-solution-deployment"></a>多次元モデルのソリューションの配置
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの開発を完了したら、Analysis Services サーバーにデータベースを配置できます。 Analysis Services には、テスト サーバーまたは実稼働サーバーにデータベースを移動するために使用できる 6 つの配置方法が用意されています。 利点の順序にここで、メソッドの一覧します。AMO オートメーション、XMLA、配置ウィザード、配置ユーティリティは、ウィザード、バックアップと復元を同期します。  
  
 このトピックのセクションは次のとおりです。  
  
 [配置方法](#bkmk_meth)  
  
 [配置に関する考慮事項](#bkmk_considerations)  
  
 [関連タスク](#bkmk_rel)  
  
##  <a name="bkmk_meth"></a> 配置方法  
  
|方法|説明|リンク|  
|------------|-----------------|----------|  
|**分析管理オブジェクト (AMO) オートメーション**|AMO を使用すると、ソリューションの配置に使用できるコマンドを含む、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の完全なコマンド セットのプログラム インターフェイスを利用できます。 ソリューション配置の方法として最も柔軟に使用できるのは、AMO オートメーションですが、この方法ではプログラミング作業も必要になります。  AMO を使用する主な利点は、AMO アプリケーションでは SQL Server エージェントを使用して、あらかじめ設定したスケジュールに従って配置を実行できることです。|[分析管理オブジェクト &#40;AMO&#41; による開発](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、既存の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのメタデータの XMLA スクリプトを生成し、別のサーバーでそのスクリプトを実行して初期データベースを再作成します。 XMLA スクリプトは、配置プロセスを定義し、それをコード化して XMLA スクリプトに保存することにより、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で簡単に作成できます。 XMLA スクリプトをファイルに保存すると、簡単に、スケジュールに基づいてスクリプトを実行したり、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインスタンスに直接接続しているアプリケーションにスクリプトを埋め込んだりすることができます。<br /><br /> SQL Server エージェントを使用すると、XMLA スクリプトもあらかじめ設定したスケジュールに従って実行できますが、XMLA スクリプトには AMO ほどの柔軟性はありません。 AMO では、さまざまなすべての管理コマンドをホストすることにより、広範にわたる機能を実現しています。|[XMLA を使用したモデル ソリューションの配置](deploy-model-solutions-using-xmla.md)|  
|**配置ウィザード**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトによって生成された XMLA 出力ファイルを使用して、プロジェクトのメタデータを宛先サーバーに配置するには、配置ウィザードを使用します。 配置ウィザードを使用すると、プロジェクト ビルドの出力ディレクトリによって作成される [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ファイルからインスタンスを直接配置できます。<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の配置ウィザードを使用する主な利点は利便性です。 後で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で使用するために XMLA スクリプトを保存できるのと同様に、配置ウィザード スクリプトも保存できます。 配置ウィザードは、対話的に実行することも、配置ユーティリティを使用してコマンド プロンプトから実行することもできます。|[Deploy Model Solutions Using the Deployment Wizard](deploy-model-solutions-using-the-deployment-wizard.md)|  
|**配置ユーティリティ**|配置ユーティリティを使用すると、コマンド プロンプトから Analysis Services の配置エンジンを起動することができます。|[配置ユーティリティを使用したモデル ソリューションの配置](deploy-model-solutions-with-the-deployment-utility.md)|  
|**データベースの同期ウィザード**|2 つの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース間でメタデータとデータを同期するには、データベースの同期ウィザードを使用します。<br /><br /> 同期ウィザードを使用すると、コピー元のサーバーからコピー先のサーバーにデータとメタデータをコピーできます。 配置するデータベースのコピーが、コピー先のサーバーにない場合、新しいデータベースがコピー先のサーバーにコピーされます。 コピー先のサーバーに同じデータベースのコピーが既にある場合、コピー先サーバー上のデータベースは、ソース データベースのメタデータとデータを使用するように更新されます。|[Analysis Services データベースの同期](synchronize-analysis-services-databases.md)|  
|**バックアップと復元**|バックアップは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを転送する最も簡単な方法です。 **[バックアップ]** ダイアログ ボックスを使用すると、オプション構成を設定した後で、ダイアログ ボックスから直接バックアップを実行できます。 また、スクリプトを作成して保存し、必要なときに実行することもできます。<br /><br /> バックアップと復元は、他の配置方法ほど頻繁には使用されませんが、インフラストラクチャの要件を最小限に抑えながら配置をすばやく完了することができます。|[Analysis Services データベースのバックアップと復元](backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_considerations"></a> 配置に関する考慮事項  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを配置する前に、次のどの質問がソリューションに当てはまるかを検討し、関連するリンクを参照して問題の解決方法を確認してください。  
  
|考慮事項|詳細情報へのリンク|  
|-------------------|------------------------------|  
|このソリューションにはどのようなハードウェアおよびソフトウェア リソースが必要か。|[Analysis Services の配置に関する要件と注意点](requirements-and-considerations-for-analysis-services-deployment.md)|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のパッケージ、レポート、リレーショナル データベース スキーマなど、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトの範囲外にある関連オブジェクトをどのように配置するか。||  
|配置した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースでデータをどのように読み込んで更新するか。<br /><br /> 配置した [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内のメタデータ (計算など) をどのように更新するか。|このトピックの「[配置方法](#bkmk_meth) 」を参照してください。|  
|インターネット経由での [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データへのアクセスをユーザーに許可するか。|[インターネット インフォメーション サービス (IIS) 8.0 上の Analysis Services への HTTP アクセスの構成](../instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データへの連続クエリ アクセスを提供するか。|[Analysis Services の配置に関する要件と注意点](requirements-and-considerations-for-analysis-services-deployment.md)|  
|リンクされているオブジェクトまたはリモート パーティションを使用して、分散環境にオブジェクトを配置するか。|[ローカル パーティションの作成と管理 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)[リモート パーティションの作成と管理 (Analysis Services)](create-and-manage-a-remote-partition-analysis-services.md) および [リンク メジャー グループ](linked-measure-groups.md)。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データをどのように保護するか。|[オブジェクトと操作へのアクセスの承認 (Analysis Services)](authorizing-access-to-objects-and-operations-analysis-services.md)|  
  
##  <a name="bkmk_rel"></a> 関連タスク  
 [Analysis Services の配置に関する要件と注意点](requirements-and-considerations-for-analysis-services-deployment.md)  
  
 [XMLA を使用したモデル ソリューションの配置](deploy-model-solutions-using-xmla.md)  
  
 [配置ウィザードを使用したモデル ソリューションの配置](deploy-model-solutions-using-the-deployment-wizard.md)  
  
 [配置ユーティリティを使用したモデル ソリューションの配置](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
