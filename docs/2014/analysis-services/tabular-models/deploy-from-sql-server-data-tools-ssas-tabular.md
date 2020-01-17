---
title: SQL Server Data Tools (SSAS テーブル) からのデプロイ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deploystatus.f1
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6429fb7f30c748c7ac0a8ab69bc16c3d63b4d3ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067300"
---
# <a name="deploy-from-sql-server-data-tools-ssas-tabular"></a>SQL Server データ ツールからの配置 (SSAS テーブル)
  このトピックのタスクは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の Deploy コマンドを使用してテーブル モデル ソリューションを配置するために使用します。  
  
 このトピックのセクション:  
  
-   [配置オプションおよび配置サーバー プロパティの構成](#bkmk_deploy)  
  
-   [テーブル モデル ソリューションの配置](#bkmk_deploy_proc)  
  
-   [配置状態](#bkmk_deploy_status)  
  
##  <a name="bkmk_deploy"></a> 配置オプションおよび配置サーバー プロパティの構成  
 テーブル モデル ソリューションを配置する前に、まず、配置オプションと配置サーバーのプロパティを指定する必要があります。 配置のプロパティおよび設定の詳細については、「 [テーブル モデル ソリューションの配置 (SSAS テーブル)](tabular-model-solution-deployment-ssas-tabular.md)の Deploy コマンドを使用してテーブル モデル ソリューションを配置するために使用します。  
  
#### <a name="to-configure-deployment-options-and-deployment-server-properties"></a>配置オプションおよび配置サーバー プロパティを構成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]の **ソリューション エクスプローラー**で、プロジェクト名を右クリックして、 **[プロパティ]** をクリックします。  
  
2.  **\<プロジェクト名 > プロパティ**ダイアログで、**展開オプション**既定の設定と異なる場合は、プロパティの設定を指定します。  
  
    > [!NOTE]  
    >  キャッシュ モードのモデルの場合、 **[クエリ モード]** は常に **[In-Memory]** です。  
  
    > [!NOTE]  
    >  DirectQuery モードのモデルの場合、 **[権限借用設定]** は指定できません。  
  
3.  **[配置サーバー]** で、 **[サーバー]** (名前)、 **[エディション]** 、 **[データベース]** (名前)、 **[キューブ名]** の各プロパティの設定を指定し (既定の設定と異なる場合)、 **[OK]** をクリックします。  
  
> [!NOTE]  
>  作成した新しいプロジェクトが指定したサーバーに自動的に配置されるように、既定の配置サーバー プロパティの設定を指定することもできます。 詳細については、「[既定のデータ モデルと配置プロパティの構成 &#40;SSAS テーブル&#41;](properties-ssas-tabular.md)」を参照してください。  
  
##  <a name="bkmk_deploy_proc"></a> テーブル モデル ソリューションの配置  
  
#### <a name="to-deploy-a-tabular-model-solution"></a>テーブル モデル ソリューションを配置するには  
  
-   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]の**ビルド** メニューのをクリックして**デプロイ\<プロジェクト名 >** します。  
  
     **[配置]** ダイアログ ボックスが表示され、メタデータの配置の状態とモデルに含まれる各テーブルの処理が示されます ([処理オプション] プロパティが [処理しない] に設定されている場合を除きます)。 配置プロセスが完了したら、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、Analysis Services インスタンスに接続し、新しい model データベース オブジェクトが作成されていることを確認するか、クライアント レポート アプリケーションを使用して配置済みモデルと接続します。  
  
##  <a name="bkmk_deploy_status"></a> 配置状態  
 **[配置]** ダイアログ ボックスでは、配置操作の進行状況を監視できます。 配置操作を停止することもできます。  
  
 **ステータス**  
 配置操作が正常に行われたかどうかを示します。  
  
 **詳細**  
 配置されたメタデータ項目と各メタデータ項目の状態を一覧表示し、何か問題があればメッセージを表示します。  
  
 **[展開の停止]**  
 クリックすると、配置操作が停止されます。 このオプションは、配置操作に時間がかかりすぎる場合や、エラーが多すぎる場合に有効です。  
  
## <a name="see-also"></a>参照  
 [テーブル モデル ソリューションの配置 (SSAS テーブル)](tabular-model-solution-deployment-ssas-tabular.md)   
 [既定のデータ モデルと配置プロパティの構成 (SSAS テーブル)](properties-ssas-tabular.md)  
  
  
