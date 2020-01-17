---
title: 'レッスン 3: Market Basket マイニング構造の処理 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce2c2e6944d524a38edc331d2cd128ca7cf7d419
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653864"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>レッスン 3: Market Basket マイニング構造の処理
  このレッスンでは、使用、 [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx)ステートメントと vAssocSeqLineItems および vAssocSeqOrders から、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]マイニング構造とマイニング処理のサンプル データベースをモデル化します。作成した[レッスン 1。Market Basket マイニング構造を作成する](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)と[レッスン 2。Market Basket マイニング構造にマイニング モデルの追加](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)します。  
  
 マイニング構造の処理では、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] でソース データが読み込まれ、マイニング モデルをサポートする構造が構築されます。 マイニング モデルを処理すると、選択したデータ マイニング アルゴリズム使用して、マイニング構造で定義されているデータが渡されます。 このアルゴリズムでは傾向とパターンが検索され、結果の情報がマイニング モデルに保存されます。 したがって、マイニング モデルには、実際のソース データではなく、アルゴリズムで検出された情報が含まれます。 マイニング モデルの処理の詳細については、次を参照してください。[処理の要件と考慮事項&#40;データ マイニング&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)します。  
  
 マイニング構造の再処理は、構造列またはソース データを変更した場合にのみ必要です。 処理済みのマイニング構造にマイニング モデルを追加する場合は、`INSERT INTO MINING MODEL` ステートメントを使用して既存のデータに対して新しいマイニング モデルをトレーニングできます。  
  
 Market Basket マイニング構造には入れ子になったテーブルが含まれるため、入れ子になったテーブル構造でトレーニングするようにマイニング列を定義する必要があります。また、`SHAPE` コマンドを使用して、ソース テーブルからトレーニング データを抽出するクエリを定義する必要があります。  
  
## <a name="insert-into-statement"></a>INSERT INTO ステートメント  
 Market Basket マイニング構造とその関連マイニング モデルをトレーニングするために使用して、 [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx)ステートメント。 ステートメントのコードは次の部分に分けることができます。  
  
-   マイニング構造の指定  
  
-   マイニング構造の列の一覧  
  
-   `SHAPE` によるトレーニング データの定義  
  
 `INSERT INTO` ステートメントの汎用例を次に示します。  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],'<nested SELECT statement>')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 コードの最初の行では、トレーニングするマイニング構造を指定します。  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 コードの次の数行では、マイニング構造で定義される列を指定します。 ここではマイニング構造の各列を指定する必要があります。各列はソース クエリ データ内の列にマップされている必要があります。 `SKIP` を使用すると、ソース データに存在するがマイニング構造に存在しない列を無視できます。 使用する方法の詳細についての`SKIP`を参照してください[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)します。  
  
```  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
```  
  
 コードの最後の行では、マイニング構造のトレーニングに使用されるデータを定義します。 ソース データは 2 つのテーブルに格納されているため、`SHAPE` を使用してテーブルを関連付けます。  
  
```  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],''<nested SELECT statement>'')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 このレッスンでは、`OPENQUERY` を使用してソース データを定義します。 ソース データに対してクエリを定義するその他の方法については、次を参照してください。 [&#60;ソース データ クエリ&#62;](/sql/dmx/source-data-query)します。  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
 このレッスンでは、次のタスクを実行します。  
  
-   Market Basket マイニング構造を処理します。  
  
## <a name="processing-the-market-basket-mining-structure"></a>Market Basket マイニング構造の処理  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>INSERT INTO を使用してマイニング構造を処理するには  
  
1.  **オブジェクト エクスプ ローラー**のインスタンスを右クリックして[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、をポイント**新しいクエリ**、をクリックし、 **DMX**します。  
  
     クエリ エディターが開き、新しい空のクエリが表示されます。  
  
2.  上の INSERT INTO ステートメントの汎用例を空のクエリにコピーします。  
  
3.  次の部分を探します。  
  
    ```  
    [<mining structure>]  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    Market Basket  
    ```  
  
4.  次の部分を探します。  
  
    ```  
    <mining structure columns>  
    [<nested table>]  
    ( SKIP, <skipped column> )  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    [OrderNumber],  
    [Products]   
    (SKIP, [Model])  
    ```  
  
     このステートメントでは、`Products` は SHAPE ステートメントで定義される Products テーブルを参照します。 `SKIP` は、ソース データにキーとして存在する Model 列を無視するために使用します。マイニング構造に対しては使用できません。  
  
5.  次の部分を探します。  
  
    ```  
    SHAPE {  
      OPENQUERY([<datasource>],'<SELECT statement>') }  
    APPEND  
    (   
      {OPENQUERY([<datasource>],'<nested SELECT statement>')  
    }  
    RELATE [<case key>] TO [<foreign key>]  
    ) AS [<nested table>]  
    ```  
  
     これを次の文字列に置き換えます。  
  
    ```  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
     ソース クエリの参照、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]で定義されているデータ ソース、[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]サンプル プロジェクト。 ソース クエリはこのデータ ソースを使用して、vAssocSeqLineItems ビューと vAssocSeqOrders ビューにアクセスします。 これら 2 つのビューには、マイニング モデルのトレーニングに使用されるソース データが含まれます。 このプロジェクトやこれらのビューを作成していない場合は、次を参照してください。 [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)します。  
  
     `SHAPE` コマンド内では、`OPENQUERY` を使用して 2 つのクエリを定義します。 最初のクエリでは親テーブルを定義し、2 つ目のクエリでは入れ子になったテーブルを定義します。 2 つのテーブルは、両方のテーブルに存在する OrderNumber 列を使用して関連付けられます。  
  
     最終的なステートメントは次のようになります。  
  
    ```  
    INSERT INTO MINING STRUCTURE [Market Basket]  
    (  
       [OrderNumber],[Products] (SKIP, [Model])  
    )  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
6.  **ファイル** メニューのをクリックして**付けて DMXQuery1.dmx を保存**します。  
  
7.  **付けて** ダイアログ ボックスで、適切なフォルダーを参照し、ファイル名前`Process Market Basket.dmx`します。  
  
8.  ツールバーの**Execute**ボタンをクリックします。  
  
 クエリの実行終了後、見つかったパターンとアイテムセットを表示したり、関連付けを表示したり、アイテムセット、確率、または重要度でフィルタリングしたりできます。 この情報を表示する[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]、データ モデルの名前を右クリックし、クリックして**参照**します。  
  
 次のレッスンでは、Market Basket 構造に追加したマイニング モデルに基づいて、いくつかの予測を作成します。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 4:マーケット バスケット予測の実行](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
