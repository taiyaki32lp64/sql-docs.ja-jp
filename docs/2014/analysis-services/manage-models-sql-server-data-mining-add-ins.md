---
title: モデル (SQL Server データ マイニング アドイン) の管理 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, importing
- mining models, deleting
- mining models, managing
- mining models, training
- mining models, processing
- mining models, exporting
ms.assetid: c11380f0-7c24-4668-9cdf-9c53e4aff665
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d5f0619e7291cc08b1750c0b35f9639cb7a9872
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078035"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>モデルの管理 (SQL Server データ マイニング アドイン)
  ![モデルの管理 ボタン、データ マイニング リボン](media/dmc-manage.gif "モデルの管理 ボタン、データ マイニング リボン")  
  
 **モデルの管理** ダイアログ ボックスでは、既存のマイニング モデルおよびマイニング構造に格納されていると対話することができます、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]は現在接続されているサーバー。 さらに、現在のセッション中に作成された一時的な構造およびモデルを表示および管理できます。 セッション モデルおよびサーバー上に格納されているモデルをこれまでに使用している場合、ダイアログ ボックスにこれらのモデルが表示されます。  
  
## <a name="using-the-manage-models-wizard"></a>モデルの管理ウィザードの使用  
 クリックすると**モデルの管理**、**管理マイニング構造およびモデル** ダイアログ ボックスが開いたら、既存のデータ マイニング モデルおよび構造を管理するため、次の機能へのアクセスを提供します。  
  
-   マイニング モデルまたは構造の名前を変更する。  
  
-   マイニング モデルまたは構造を削除する。  
  
-   マイニング モデルまたは構造を消去する。  
  
-   新しいデータまたは既存のデータを使用してマイニング構造を処理する。  
  
-   マイニング モデルまたは構造をエクスポートまたはインポートする。  
  
> [!NOTE]  
>  このダイアログ ボックスを使用してクエリまたはモデルを作成することはできません。 新しいマイニング構造を作成するには、Excel、または使用のデータ マイニング クライアントに表示されるウィザードの 1 つを使用、**データ マイニング詳細クエリ エディター**します。  
  
### <a name="requirements"></a>要件  
 データ マイニング モデルを管理するには、最初に [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスへの接続を作成する必要があります。 一時ファイルに保存されているセッション モデルを操作する場合も同様です。 作成または接続を変更する方法の詳細については、次を参照してください。[ソース データへの接続&#40;Excel 用データ マイニング クライアント&#41;](connect-to-source-data-data-mining-client-for-excel.md)します。  
  
 接続先の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスに既存のデータ マイニング構造またはデータ マイニング モデルがない場合は、ウィザードまたはこのアドインに用意されているその他のツールを使用して、データ マイニング構造またはデータ マイニング モデルを作成できます。 使用して、新しいモデルを作成することも、**データ マイニング モデルの高度なエディター**します。  
  
## <a name="see-also"></a>参照  
 [マイニング モデルを文書化&#40;データ マイニング Excel 用アドイン&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [展開して、マイニング モデルのスケーリング&#40;データ マイニング Excel 用アドイン&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
