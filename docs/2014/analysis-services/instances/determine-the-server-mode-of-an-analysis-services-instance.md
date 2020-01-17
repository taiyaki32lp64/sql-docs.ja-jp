---
title: Services インスタンスのサーバー モードの分析の決定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9e556fb1-ca37-4f06-8f8f-f187cb0fdb37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff9ac19c0b605266de5eca69dd0f410f0d8fbdd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080061"
---
# <a name="determine-the-server-mode-of-an-analysis-services-instance"></a>Analysis Services インスタンスのサーバー モードの決定
  Analysis Services は、次の 3 つのサーバー モードのいずれかでインストールできます。多次元および PowerPivot for SharePoint、および表形式データ マイニングのユニット (既定値)。 Analysis Services インスタンスのサーバー モードは、セットアップ時にサーバーのインストール オプションを選択するときに決定します。  
  
 サーバー モードによって、作成および配置するソリューションの種類が決まります。 自分でサーバー ソフトウェアをインストールしなかった場合に、サーバーがインストールされたモードを確認するには、このトピックの情報を使用してモードを判別できます。 特定のモードで使用できる機能の詳細については、「[テーブル ソリューションと多次元ソリューションの比較 &#40;SSAS&#41;](../comparing-tabular-and-multidimensional-solutions-ssas.md)」を参照してください。  
  
 インストールした際のサーバー モードを使用しない場合は、ソフトウェアをアンインストールしてから、必要なモードを選択して再インストールする必要があります。 または、同じコンピューターに Analysis Services のもう 1 つのインスタンスをインストールして、複数のインスタンスを異なるモードで実行させることもできます。  
  
## <a name="server-icons-in-object-explorer"></a>オブジェクト エクスプローラーでのサーバー アイコン  
 サーバー モードを判別する最も簡単な方法は、SQL Server Management Studio でサーバーに接続し、オブジェクト エクスプローラーのサーバー名の横にあるアイコンを確認する方法です。 次の図に、多次元、テーブル、および PowerPivot の各モードで配置された Analysis Services の 3 つのインスタンスを示します。  
  
 ![オブジェクト エクスプ ローラーのアイコンの各サーバー モード](../media/ssas-ssms-servermodes.gif "サーバー モードごとのオブジェクト エクスプ ローラーのアイコン")  
  
## <a name="viewing-deploymentmode-property-in-msmdsrvini-file"></a>MSMDSRV.INI ファイルの DeploymentMode プロパティの表示  
 すべての Analysis Services インスタンスに含まれる msmdsrv.ini ファイルで `DeploymentMode` プロパティをチェックすることもできます。 このプロパティの値によってサーバー モードが示されます。 有効な値は、0 (多次元)、1 (SharePoint)、または 2 (テーブル) です。 msmdsrv.ini ファイルを開くには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理者 (つまり、サーバー ロールのメンバー) である必要があります。 このファイルには、構造化された XML が含まれています。 メモ帳または他のテキスト エディターでファイルを閲覧できます。  
  
> [!CAUTION]  
>  `DeploymentMode` プロパティの値は変更しないでください。 サーバーのインストール後の手動でのプロパティ変更はサポートされていません。  
  
## <a name="about-the-deploymentmode-property"></a>DeploymentMode プロパティについて  
 `DeploymentMode` プロパティは、Analysis Services サーバー インスタンスの操作コンテキストを指定します。 このプロパティは、ダイアログ ボックス、メッセージ、およびドキュメントの「サーバー モード」と呼ばれます。 このプロパティは、Analysis Services のインストール方法に基づいてセットアップによって初期化されます。 このプロパティは内部使用のみと見なしてください。常にセットアップによって指定された値が使用されます。  
  
 このプロパティの有効値を以下に示します。  
  
|値|Description|  
|-----------|-----------------|  
|0|これが既定値です。 MOLAP、HOLAP、ROLAP の各ストレージ、およびデータ マイニング モデルを使用する多次元データベースの処理に使用される多次元モードを指定します。|  
|1|PowerPivot for SharePoint 配置の一部としてインストールされた Analysis Services インスタンスを指定します。 PowerPivot for SharePoint インストールの一部である Analysis Services インスタンスの配置モード プロパティは変更しないでください。 モードを変更すると、PowerPivot データがサーバー上で実行されなくなります。|  
|2|インメモリ ストレージまたは DirectQuery ストレージを使用するテーブル モデル データベースをホストするために使用するテーブル モードを指定します。|  
  
 各モードは、他のモードと相互に排他的です。 テーブル モード用に構成されたサーバーでは、キューブおよびディメンションを含む Analysis Services データベースを実行できません。 基になるコンピューターのハードウェアでサポートできる場合は、Analysis Services の複数のインスタンスを同じコンピューターにインストールし、さまざまな配置モードを使用するように各インスタンスを構成できます。 Analysis Services はリソースを大量に消費するアプリケーションであることに注意してください。 同じシステム上に複数のインスタンスを配置する構成は、ハイエンド サーバーの場合のみお勧めします。  
  
## <a name="see-also"></a>参照  
 [表形式モードで Analysis Services をインストールします。](install-windows/install-analysis-services.md)   
 [多次元モードおよびデータ マイニング モードでの Analysis Services のインストール](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [PowerPivot for SharePoint 2010 のインストール](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Analysis Services への接続](connect-to-analysis-services.md)   
 [テーブル モデル ソリューション &#40;SSAS テーブル&#41;](../tabular-model-solutions-ssas-tabular.md)   
 [多次元モデル ソリューション &#40;SSAS&#41;](../multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [マイニング モデル &#40;Analysis Services - データ マイニング&#41;](../data-mining/mining-models-analysis-services-data-mining.md)  
  
  
