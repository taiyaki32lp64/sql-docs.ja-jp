---
title: マイニング構造でドリルスルー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71212f81a2f42fbbff28e04b4632bc2120362089
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084579"
---
# <a name="drillthrough-on-mining-structures"></a>マイニング構造でのドリルスルー
  *ドリルスルー* とは、マイニング モデルまたはマイニング構造に対してクエリを実行し、モデルで公開されていない詳細データを取得する機能です。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] は、ケース データへのドリルスルーの 2 つのオプションを提供します。 マイニング モデルの作成に使用されたデータにドリルスルーすることも、マイニング構造のソース データにドリルスルーすることもできます。  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>モデル ケースへのドリルスルーと構造へのドリルスルー  
 **モデル ケース** へのドリルスルーは、モデル内のルール、パターン、またはクラスターに関する詳細情報を探すのに役立ちます。  
  
 対照的に、 **構造データへのドリルスルー** は、モデル内で使用できなかった情報へのアクセスを可能にすることが目的です。 たとえば、適切な権限がある場合は、モデルのトレーニングに使用されたデータ行とテストに使用されたデータ行を調べることができます。  
  
 構造定義に含まれていれば、分析で使用されなかったデータの属性を表示することもできます。 たとえば、マイニング構造では多くの異なる種類のモデルがサポートされることが多く、一部の構造列はデータ型に互換性がないかデータが分析に役立たないためにモデルから除外されていることがあります。 たとえば、クラスター モデルの顧客の連絡先情報はデータが構造に含まれていたとしても使用しませんが、データ ソースに対する個別のクエリを実行しなくても、ドリルスルーを有効にすることでこの情報にアクセスできます。  
  
## <a name="enabling-drillthrough-to-structure-data"></a>構造データへのドリルスルーの有効化  
 マイニング構造でドリルスルーを使用するには、次の条件が満たされている必要があります。  
  
-   モデルでのドリルスルーも有効にする必要があります。 既定では、両方の種類のドリルスルーが無効になっています。 データ マイニング ウィザードでドリルスルーを有効にするには、最終ページでモデル ケースへのドリルスルーを有効にするオプションを選択します。 `AllowDrillthrough` プロパティを変更することで、モデルのドリルスルー機能を後で追加することもできます。  
  
-   DMX を使用してマイニング構造を作成する場合は、WITH DRILLTHROUGH 句を使用します。 詳細については、「[CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)」を参照してください。  
  
-   マイニング構造を処理したときにキャッシュされたトレーニング ケースに関する情報が取得されることで、ドリルスルーが機能します。 そのため、変更することで、構造の処理後、キャッシュされたデータを消去した場合、<xref:Microsoft.AnalysisServices.MiningStructureCacheMode>プロパティを`ClearAfterProcessing`ドリルスルーは機能しません。 構造列へのドリルスルーを有効にするには、<xref:Microsoft.AnalysisServices.MiningStructureCacheMode> プロパティを `KeepTrainingCases` に変更してから構造を再処理する必要があります。  
  
-   マイニング構造とマイニング モデルの両方があることを確認して、 [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl)プロパティに設定`True`します。 さらに、構造とモデルの両方に対するドリルスルー権限を持つロールのメンバーである必要があります。  
  
## <a name="security-issues-for-drillthrough"></a>ドリルスルーのセキュリティに関する問題  
 ドリルスルー権限は、構造およびモデルで個別に設定されます。 構造で権限が与えられていない場合でも、モデル権限があればモデルからドリルスルーを行うことができます。 構造のドリルスルー権限がある場合は、[StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx) 関数を使用して、構造列をモデルからドリルスルー クエリに含めることもできます。  
  
 Analysis Services でロールを作成して権限を割り当てる方法については、「[ロール デザイナー &#40;Analysis Services - 多次元データ&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx)」を参照してください。  
  
> [!NOTE]  
>  マイニング構造とマイニング モデルの両方についてドリルスルーを有効にした場合、そのマイニング モデルに対するドリルスルー権限を持つロールのすべてのメンバー ユーザーが、マイニング構造内の列を表示できるようになります。これらの列がマイニング モデルに含まれていなかったとしても同様です。 したがって、機密データを保護するため、個人情報をマスクするデータ ソース ビューを設定し、マイニング構造に対するドリルスルー アクセスは必要な場合にのみ許可する必要があります。  
  
## <a name="related-tasks"></a>Related Tasks  
 マイニング モデルでドリルスルーを使用する方法の詳細については、次のトピックを参照してください。  
  
|||  
|-|-|  
|マイニング モデル ビューアーから構造へのドリルスルーの使用|[モデル ビューアーからのドリルスルーの使用](use-drillthrough-from-the-model-viewers.md)|  
|特定のモデルの種類に対するドリルスルー クエリの例|[データ マイニング クエリ](data-mining-queries.md)|  
|特定のマイニング構造とマイニング モデルに適用される権限の詳細|[データ マイニング構造およびデータ マイニング モデルに対する権限の付与 (Analysis Services)](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>参照  
 [マイニング モデルでのドリルスルー](drillthrough-on-mining-models.md)  
  
  
