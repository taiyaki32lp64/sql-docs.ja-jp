---
title: パーティション (SSAS テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5dd80a1f6645e7d1c766e88de653fa1e8f1f4cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066901"
---
# <a name="partitions-ssas-tabular"></a>パーティション (SSAS テーブル)
  パーティションは、テーブルを論理的な部分に分割します。 各パーティションは、他のパーティションとは個別に処理 (更新) できます。 モデル作成時に [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] の [パーティション] ダイアログ ボックスを使用して作成されたパーティションは、モデル ワークスペース データベースに適用されます。 モデルが配置されたときに、モデル ワークスペース データベースに定義されたパーティションが配置済み model データベースで複製されます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の [パーティション] ダイアログ ボックスを使用して、配置済みモデル データベースのパーティションをさらに作成し管理できます。  このトピックでは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の [パーティション マネージャー] ダイアログ ボックスを使用してモデルを作成するときに作成されたパーティションについて説明します。 配置済みモデルのパーティションの作成と管理の詳細については、「[テーブル モデル パーティションの作成および管理 (SSAS テーブル)](create-and-manage-tabular-model-partitions-ssas-tabular.md)」を参照してください。  
  
 このトピックのセクション:  
  
-   [利点](#bkmk_benefits)  
  
-   [関連タスク](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 利点  
 テーブル モデルでは、パーティションがテーブルを論理パーティション オブジェクトに分割します。 各パーティションは、他のパーティションとは個別に処理できます。 たとえば、あるテーブルにはめったに変更されないデータを含む所定の行セットが含まれている場合がありますが、他の行セットには頻繁に変更されるデータがあるとします。 このような場合は、データの一部を処理するときにデータ全体を処理する必要はありません。 パーティションを使用すると、めったに処理されないデータから頻繁に処理する必要のあるデータ部分を分割できます。  
  
 効率的なモデル設計によるパーティションの活用によって、不必要な処理とその後の Analysis Services サーバーでのプロセッサ負荷が排除されます。同時に、データ ソースの大部分の最新のデータを反映できる頻度でデータが処理され更新されるようになります。 モデル作成時にパーティションをどのように実装し利用するかは、配置済みモデルでパーティションがどのように実装され利用されているかによって大幅に異なる場合があります。 モデル作成段階では、最終的に配置済みモデルに入るデータのサブセットのみを操作している可能性があるということに注意してください。  
  
### <a name="processing-partitions"></a>パーティションの処理  
 配置済みモデルでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用するか、プロセス コマンドを含み処理のオプションと設定を指定するスクリプトを実行して、処理が行われます。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]を使用してモデルを作成するとき、[モデル] メニューまたはツール バーの [処理] を使用して、処理操作を実行できます。 処理操作は、パーティション、テーブル、またはすべてに対して指定できます。  
  
 処理操作を実行するときは、データ接続を使用してデータ ソースへの接続が行われます。 モデル テーブルに新しいデータがインポートされると、各テーブルに対してリレーションシップと階層が再構築され、計算済みの列およびメジャーでの計算が再計算されます。  
  
 テーブルを論理パーティションにさらに分割することで、各パーティション内のどのデータを、どのタイミングで、どのように処理するかを、選択的に決めることができます。 モデルを配置するとき、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の [パーティション] ダイアログ ボックスを使用するか、プロセス コマンドを実行するスクリプトを使用して、パーティションの処理を手動で完了できます。  
  
### <a name="partitions-in-the-model-workspace-database"></a>モデル ワークスペース データベースのパーティション  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]内の Partition Manager を使用して、新しいパーティションの作成、パーティションの編集、マージ、または削除が可能です。 パーティション マネージャーは、テーブル、行、およびパーティションの列を選択するための 2 つのモードを提供します。テーブルのプレビュー モードと SQL クエリ モード。 すべてのパーティションは SQL クエリを使用して定義しますが、テーブル プレビュー モードを使用すると、パーティションに含めるデータをプレビューして選択できます。 SQL クエリが自動的に作成され、検証されます。 テーブル プレビュー モードは [テーブルのプロパティの編集] ダイアログ ボックスおよびテーブルのインポート ウィザードの [テーブルのプレビュー] ページと同じテーブル プレビューであるため、プレビューの最大行数は 50 です。  
  
### <a name="partitions-in-a-deployed-model-database"></a>配置済みモデル データベースのパーティション  
 モデルを配置するとき、配置済みモデル データベースのパーティションは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のデータベース オブジェクトとして表示されます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の [パーティション] ダイアログ ボックスを使用して、配置済みモデルのパーティションを作成、編集、マージ、および削除できます。 このトピックでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] での配置済みモデルのパーティションの管理については説明しません。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でのパーティション管理については、「[テーブル モデル パーティションの作成および管理 (SSAS テーブル)](create-and-manage-tabular-model-partitions-ssas-tabular.md)」を参照してください。  
  
##  <a name="bkmk_related_tasks"></a> 関連タスク  
  
|トピック|説明|  
|-----------|-----------------|  
|[ワークスペース データベースのパーティションの作成と管理 (SSAS テーブル)](workspace-database-ssas-tabular.md)|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で Partition Manager を使用して、モデル ワークスペース データベースでパーティションを作成し管理する方法について説明します。|  
|[ワークスペース データベースでパーティションを処理&#40;SSAS 表形式&#41;](process-partitions-in-the-workspace-database-ssas-tabular.md)|モデル ワークスペース データベースでのパーティションの処理 (更新) 方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [DirectQuery モード &#40;SSAS テーブル&#41;](directquery-mode-ssas-tabular.md)   
 [データの処理 (SSAS テーブル)](../process-data-ssas-tabular.md)  
  
  
