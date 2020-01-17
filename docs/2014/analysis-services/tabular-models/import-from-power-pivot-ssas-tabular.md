---
title: PowerPivot (SSAS テーブル) からのインポート |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 941155a5e434457cdf9c79bd25c653c7207937a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067015"
---
# <a name="import-from-powerpivot-ssas-tabular"></a>PowerPivot からのインポート (SSAS テーブル)
  このトピックでは、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] の PowerPivot からのインポート プロジェクト テンプレートを使用して PowerPivot ブックからメタデータおよびデータをインポートし、新しい表形式モデル プロジェクトを作成する方法を説明します。  
  
## <a name="create-a-new-tabular-model-from-a-powerpivot-for-excel-file"></a>Excel ファイルの PowerPivot から表形式の新しいモデルを作成します。  
 PowerPivot ブックからのインポートにより新しいテーブル モデル プロジェクトを作成すると、ブックの構造を定義するメタデータが使用され、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] にテーブル モデルの構造が作成および定義されます。 テーブル、列、メジャー、リレーションシップなどのオブジェクトは、PowerPivot ブックにあるとおりにテーブル モデル プロジェクトで保持および表示されます。 .xlsx ブック ファイルに対する変更は行われません。  
  
> [!NOTE]  
>  リンク テーブルは、テーブル モデルではサポートされません。 リンク テーブルを含む PowerPivot ブックからインポートするとき、リンク テーブル データはコピー/貼り付けデータとして取り扱われ、Model.bim ファイルに保存されます。 コピー/貼り付けテーブルのプロパティを表示するとき、 **ソース データ** プロパティは無効であり、 **[テーブル]** メニューの **[テーブルのプロパティ]** ダイアログは無効です。  
>   
>  モデルに埋め込まれているデータに追加できる行数は 10,000 行に制限されています。 PowerPivot からモデルをインポートして、ときに、"データが切り捨てられました。 貼り付けられたテーブルには、10000 個を超える行を含めることはできません"SQL Server でのテーブルなど、別のデータ ソースに埋め込みデータを移動することによって、PowerPivot モデルを変更し、再インポートする必要があります。  
  
 ワークスペース データベースが、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] と同じコンピューター (ローカル) の Analysis Services インスタンスにあるか、リモートの Analysis Services インスタンスにあるかにより、特に注意する点が変わります。  
  
 ワークスペース データベースが、Analysis Services のローカル インスタンスにある場合は、メタデータとデータの両方を PowerPivot ブックからインポートできます。 メタデータはブックからコピーされて、テーブル モデル プロジェクトを作成するために使用されます。 データがブックからコピーし、(コピー/貼り付けデータを除き、Model.bim ファイルに格納されている)、プロジェクトのワークスペース データベースに格納します。  
  
 ワークスペース データベースが、Analysis Services のリモート インスタンスにある場合は、PowerPivot for Excel ブックからデータをインポートできません。 ブックのメタデータはインポートできますが、インポートすると、スクリプトがリモートの Analysis Services インスタンスで実行されます。 信頼できる PowerPivot ブックからのみメタデータをインポートする必要があります。 データは、データ ソース接続に定義されたソースからインポートする必要があります。 PowerPivot ブックのコピー/貼り付けデータとリンク テーブル データは、テーブル モデル プロジェクトにコピーして貼り付ける必要があります。  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-powerpivot-for-excel-file"></a>PowerPivot for Excel ファイルから新しいテーブル モデル プロジェクトを作成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]の **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。  
  
2.  **新しいプロジェクト**ダイアログ ボックスで、**インストールされたテンプレート**、 をクリックして**Business Intelligence**、 をクリックし、 **PowerPivotからインポート**.  
  
3.  **[名前]** にプロジェクトの名前を入力し、場所とソリューション名を指定してから、 **[OK]** をクリックします。  
  
4.  **[ファイルを開く]** ダイアログ ボックスで、インポートするモデル メタデータおよびデータを含む [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] ファイルを選択し、 **[開く]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ワークスペース データベース &#40;SSAS テーブル&#41;](workspace-database-ssas-tabular.md)   
 [データのコピーと貼り付け &#40;SSAS テーブル&#41;](../copy-and-paste-data-ssas-tabular.md)  
  
  
