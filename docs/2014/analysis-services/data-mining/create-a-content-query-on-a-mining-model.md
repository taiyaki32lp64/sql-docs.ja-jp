---
title: マイニング モデルに対するコンテンツ クエリの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: a0ce837a-89ed-46cf-9ce1-801ccb75fa04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d2e3607426ecbc51b1d04dfc97b12f83faf328b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085579"
---
# <a name="create-a-content-query-on-a-mining-model"></a>マイニング モデルのコンテンツ クエリの作成
  AMO や XML/A を使用すると、プログラムでマイニング モデル コンテンツにクエリを実行できますが、DMX を使用してクエリを作成する方が簡単です。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスへの接続を確立し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]によって提供される DMV を使用してクエリを作成することにより、データ マイニング スキーマ行セットに対するクエリを作成することもできます。  
  
 次の手順では、DMX を使用してマイニング モデルに対するクエリを作成する方法と、データ マイニング スキーマ行セットに対するクエリを実行する方法について説明します。  
  
 XML/A を使用して類似のクエリを作成する方法の例については、「 [XMLA を使用したデータ マイニング クエリの作成](create-a-data-mining-query-by-using-xmla.md)」を参照してください。  
  
## <a name="querying-data-mining-model-content-by-using-dmx"></a>DMX を使用したデータ マイニング モデル コンテンツのクエリ  
  
#### <a name="to-create-a-dmx-model-content-query"></a>DMX モデル コンテンツ クエリを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[表示]** メニューの **[テンプレート エクスプローラー]** をクリックします。  
  
2.  **[テンプレート エクスプローラー]** ペインで、キューブ アイコンをクリックして一覧を変更し、Analysis Services テンプレートを表示します。  
  
3.  テンプレート カテゴリの一覧で、 **[DMX]** 、 **[モデル コンテンツ]** の順に展開し、 **[コンテンツ クエリ]** をダブルクリックします。  
  
4.  **[Analysis Services への接続]** ダイアログ ボックスで、クエリを実行するマイニング モデルを含むインスタンスを選択し、 **[接続]** をクリックします。  
  
     コード エディターに **[コンテンツ クエリ]** テンプレートが表示されます。 メタデータ ペインに、現在のデータベースで使用可能なモデルが一覧表示されます。 データベースを変更するには、 **[使用できるデータベース]** の一覧から別のデータベースを選択します。  
  
5.  行で、マイニング モデルの名前を入力します。 `FROM` [ *\<マイニング モデル, name, MyModel >* ]`.CONTENT`します。 マイニング モデル名にスペースが含まれる場合は、名前を角かっこで囲む必要があります。  
  
     名前を入力せずに、 **オブジェクト エクスプローラー** でマイニング モデルを選択してテンプレートにドラッグすることもできます。  
  
6.  行で、 `SELECT` *\<expr 一覧で、選択リストの\* >* 、マイニング モデル コンテンツ スキーマ行セット内の列の名前を入力します。  
  
     マイニング モデル コンテンツ クエリで返すことができる列の一覧については、「 [マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)によって提供される DMV を使用してクエリを作成することにより、データ マイニング スキーマ行セットに対するクエリを作成することもできます。  
  
7.  必要に応じて、テンプレートの WHERE 句に条件を入力し、特定のノードや値に対して返される行を制限します。  
  
8.  **[実行]** をクリックします。  
  
## <a name="querying-the-data-mining-schema-rowsets"></a>データ マイニング スキーマ行セットのクエリ  
  
#### <a name="to-create-a-query-against-the-data-mining-schema-rowset"></a>データ マイニング スキーマ行セットに対するクエリを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の **[新しいクエリ]** ツール バーで、 **[Analysis Services DMX クエリ]** または **[Analysis Services MDX クエリ]** をクリックします。  
  
2.  **[Analysis Services への接続]** ダイアログ ボックスで、クエリを実行するオブジェクトを含むインスタンスを選択し、 **[接続]** をクリックします。  
  
     コード エディターに **[コンテンツ クエリ]** テンプレートが表示されます。 メタデータ ペインに、現在のデータベースで使用可能なオブジェクトが一覧表示されます。 データベースを変更するには、 **[使用できるデータベース]** の一覧から別のデータベースを選択します。  
  
3.  クエリ エディターに次のように入力します。  
  
     `SELECT *`  
  
     `FROM $system.DMSCHEMA_MINING_MODEL_CONTENT`  
  
     `WHERE MODEL_NAME = '<model name>'`  
  
4.  **[実行]** をクリックします。  
  
     結果ペインにモデルのコンテンツが表示されます。  
  
    > [!NOTE]  
    >  を現在のインスタンスでクエリを実行できるすべてのスキーマ行セットの一覧を表示するには、このクエリを使用します。`SELECT * FROM $system.`DISCOVER_SCHEMA_ROWSETS します。 データ マイニング固有のスキーマ行セットの一覧については、「 [データ マイニング スキーマ行セット](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](mining-model-content-analysis-services-data-mining.md)   
 [データ マイニング スキーマ行セット](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
  
