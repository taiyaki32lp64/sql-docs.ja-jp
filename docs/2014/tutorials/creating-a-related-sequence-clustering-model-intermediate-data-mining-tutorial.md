---
title: 関連するシーケンス クラスター モデル (中級者向けデータ マイニング チュートリアル) を作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71db7ba5246e151bbca8a52972a2ba835b80ddb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62855877"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>関連するシーケンス クラスター モデルの作成 (中級者向けデータ マイニング チュートリアル)
  シーケンス クラスター モデルの検証により、Region や Income などの他の属性がモデルに大きな影響を与えていることがわかりました。そのため、シーケンスについての理解を深めるために、関連するシーケンス クラスター モデルを作成し、顧客の人口統計に関連する属性を削除します。  
  
 この作業では、地域別のシーケンス クラスター モデルのコピーを作成し、そのモデルからシーケンスに直接関連しない列を削除します。  
  
 新しいモデルには基になるマイニング モデルと同じすべての列が含まれますが、 マイニング構造から列を削除する必要はありません。新しいマイニング モデルで列を無視するように指定するだけです。  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>シーケンス クラスター モデルのコピーを作成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、データ マイニング デザイナーでクリックして、**マイニング モデル**タブ。  
  
2.  コピー、および選択するモデルを右クリックして**マイニング モデルの新しい**します。  
  
3.  **マイニング モデルの新しい**ダイアログ ボックスで、モデルの名前を入力し、Microsoft を選択`Sequence Clustering`します。  
  
     このチュートリアルでは、名前を入力`Sequence Clustering`します。  
  
4.  **[OK]** をクリックします。  
  
### <a name="to-remove-columns-from-the-mining-model"></a>マイニング モデルから列を削除するには  
  
1.  **マイニング モデルの**] タブの [Sequence Clustering という名前の新しいモデルの列の行をクリックして、 **Income Group**属性、および選択**無視**します。  
  
2.  属性のこの手順を繰り返します**リージョン**します。  
  
3.  テーブル名の横にプラス記号をクリックします。 **v Assoc Seq Line Items**テーブルを展開すると、入れ子になったテーブルから列を表示します。  
  
     新しいモデルの列は、次の列だけになります。  
  
     **順序 NumberKey**  
  
     **行番号のキー**  
  
     **モデルを予測します。**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>新しいシーケンス クラスター モデルを処理するには  
  
1.  **マイニング モデルの** タブで、という名前の新しいモデルを右クリックして`Sequence Clustering`、選択および**プロセス モデル**します。  
  
     新しいマイニング モデルは処理済みの構造に基づく簡略化されたモデルであるため、構造を再処理する必要はありません。 新しいマイニング モデルのみを処理できます。  
  
2.  クリックして**はい**サーバーに更新されたデータ マイニング プロジェクトを配置します。  
  
3.  **マイニング モデルの処理**ダイアログ ボックスで、をクリックして**実行**します。  
  
4.  をクリックして**閉じます**を閉じる、**処理の進行状況** ダイアログ ボックスをクリック**閉じます**で再度、**マイニング モデルの処理** ダイアログ ボックス。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [シーケンス クラスター モデルで予測の作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>関連項目  
 [処理の要件および注意事項 &#40;データ マイニング&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
