---
title: テンプレートから単一予測クエリの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- singleton query predictions [DMX]
ms.assetid: e0a68ab0-bece-4d25-b464-47f1719302e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15dcb2c8241b8b4cf7cdb2780ed532e863cf52ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085491"
---
# <a name="create-a-singleton-prediction-query-from-a-template"></a>テンプレートからの単一予測クエリの作成
  単一クエリは、外部入力データ セットにマップしたり一括予測を行う必要はありませんが、使用、予測に使用するモデルがある場合に便利です。 単一クエリでは、モデルに 1 つまたは複数の値を提供し、予測される値を即時に参照できます。  
  
 たとえば、次の DMX クエリは、メーリング対象モデル TM_Decision_Tree に対する単一クエリを表しています。  
  
```  
SELECT * FROM [TM_Decision_tree] ;  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 次の手順では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でテンプレート エクスプローラーを使用してこのクエリを迅速に作成する方法について説明します。  
  
### <a name="to-open-the-analysis-services-templates-in-sql-server-management-studio"></a>SQL Server Management Studio で Analysis Services テンプレートを開くには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[表示]** メニューの **[テンプレート エクスプローラー]** をクリックします。  
  
2.  キューブ アイコンをクリックして、 **[分析サーバー]** テンプレートを開きます。  
  
### <a name="to-open-a-prediction-query-template"></a>予測クエリ テンプレートを開くには  
  
1.  **[テンプレート エクスプローラー]** の分析サーバー テンプレートの一覧から **[DMX]** を展開し、 **[予測クエリ]** を展開します。  
  
2.  **[単一予測]** をダブルクリックします。  
  
3.  **[Analysis Services への接続]** ダイアログ ボックスで、クエリの対象であるマイニング モデルを含む [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのあるサーバー名を入力します。  
  
4.  **[接続]** をクリックします。  
  
5.  指定したデータベースでテンプレートが開き、データ マイニング関数と、データ マイニング構造および関連するモデルの一覧を示す、マイニング モデルのオブジェクト ブラウザーが表示されます。  
  
### <a name="to-customize-the-singleton-query-template"></a>単一クエリ テンプレートをカスタマイズするには  
  
1.  テンプレートで、 **[使用できるデータベース]** ドロップダウン リストをクリックし、一覧から Analysis Services インスタンスをクリックします。  
  
2.  **[マイニング モデル]** ボックスの一覧から、クエリの対象とするマイニング モデルをクリックします。  
  
     マイニング モデルの列の一覧がオブジェクト ブラウザーの **[メタデータ]** ペインに表示されます。  
  
3.  **[クエリ]** メニューの **[テンプレート パラメーターの値の指定]** をクリックします。  
  
4.  **select list** 行に「*」と入力するとすべての列が返され、列と式のコンマ区切りの一覧を入力すると特定の列が返されます。  
  
     「*」と入力すると、予測可能列と、手順 6. で新しい値を指定する列が返されます。  
  
     このトピックの冒頭に示したサンプル コードでは、 **select list** 行を * に設定していました。  
  
5.  **mining model** 行には、 **オブジェクト エクスプローラー**に表示されるマイニング モデルの一覧からマイニング モデルの名前を入力します。  
  
     このトピックの冒頭に示したサンプル コードについては、**マイニング モデル**行は、名前に設定された`TM_Decision_Tree`します。  
  
6.  **value** 行には、予測を行う新しいデータを入力します。  
  
     このトピックの冒頭に示したサンプル コードについては、**値**行に設定された`2`自転車の購買世帯の子供の数に基づく行動を予測します。  
  
7.  **column** 行には、新しいデータをマップするマイニング モデルの列名を入力します。  
  
     このトピックの冒頭に示したサンプル コードについては、**列**行に設定された`Number Children at Home`します。  
  
    > [!NOTE]  
    >  **[テンプレート パラメーターの値の指定]** ダイアログ ボックスを使用する場合、列名を角かっこで囲む必要はありません。 角かっこは自動的に追加されます。  
  
8.  ままに、**入力のエイリアス**として`t`します。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. クエリのテキスト ペインで、コンマと省略記号の下に構文エラーを示す赤い波線がある箇所を見つけます。 省略記号を削除し、必要なクエリ条件を追加します。 他の条件を追加しない場合はコンマを削除します。  
  
     このトピックの冒頭に示したサンプル コードでは、追加のクエリ条件として `'45' as [Age]` を設定していました。  
  
11. **[実行]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [予測の作成 &#40;基本的なデータ マイニング チュートリアル&#41;](../../tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
  
