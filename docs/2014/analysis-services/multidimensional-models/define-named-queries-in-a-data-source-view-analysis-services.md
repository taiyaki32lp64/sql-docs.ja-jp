---
title: データ ソース ビュー (Analysis Services) で名前付きクエリの定義 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- named queries [Analysis Services], creating
- modifying named queries
- data source views [Analysis Services], named queries
ms.assetid: f09ba8aa-950e-4c0d-961e-970de13200be
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bbb792ac4e86ae563f80f35f04854f16501b34a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075560"
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>データ ソース ビューでの名前付きクエリの定義 (Analysis Services)
  名前付きクエリは、テーブルとして表現されている SQL 式です。 名前付きクエリでは、1 つ以上のデータ ソースの 1 つ以上のテーブルから返される行および列を選択する SQL 式を指定できます。 名前付きクエリは、式に基づいていることを除いて、行とリレーションシップを持つデータ ソース ビュー (DSV) 内の他のテーブルに似ています。  
  
 名前付きクエリを使用すると、基になるデータ ソースを変更せずに、DSV 内の既存のテーブルのリレーショナル スキーマを拡張できます。 たとえば、一連の名前付きクエリを使用して、複雑なディメンション テーブルを、データベース ディメンション用により小さく単純なディメンション テーブルに分割できます。 名前付きクエリは、1 つ以上のデータ ソースの複数のデータベース テーブルを 1 つのデータ ソース ビュー テーブルに結合するために使用することもできます。  
  
## <a name="creating-a-named-query"></a>名前付きクエリの作成  
  
> [!NOTE]  
>  名前付き計算を名前付きクエリに追加したり、名前付き計算を含んでいるテーブルに基づいて名前付きクエリを作成したりすることはできません。  
  
 名前付きクエリを作成するときは、名前と、テーブルの列およびデータを返す SQL クエリを指定します。必要に応じて、名前付きクエリの説明を入力します。 SQL 式は、データ ソース ビュー内の他のテーブルを参照できます。 名前付きクエリを定義すると、名前付きクエリ内の SQL クエリがデータ ソースのプロバイダーに送信され、すべて検証されます。 プロバイダーによって SQL クエリでエラーが検出されなければ、列がテーブルに追加されます。  
  
 SQL クエリで参照されるテーブルと列は、修飾しないか、修飾する場合はテーブル名によってのみ修飾します。 たとえば、テーブルの SaleAmount 列を参照するには、 `SaleAmount` または `Sales.SaleAmount` は有効ですが、 `dbo.Sales.SaleAmount` ではエラーが発生します。  
  
 **注**   [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 のデータ ソースに対してクエリを実行する名前付きクエリを定義する場合、相関サブクエリおよび GROUP BY 句を含む名前付きクエリは失敗します。 詳細については、 [サポート技術情報の「](https://support.microsoft.com/kb/274729) 相関サブクエリと GROUP BY を含む SELECT ステートメントでバグ: 内部エラー [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
## <a name="add-or-edit-a-named-query"></a>名前付きクエリの追加または編集  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でプロジェクトを開くか、名前付きクエリを追加するデータ ソース ビューが含まれているデータベースに接続します。  
  
2.  ソリューション エクスプローラーで、 **[データ ソース ビュー]** フォルダーを展開し、データ ソース ビューをダブルクリックします。  
  
3.  **[テーブル]** ペインまたは **ダイアグラム** ペインの空いている領域を右クリックし、 **[新しい名前付きクエリ]** をクリックします。  
  
4.  **[名前付きクエリの作成]** ダイアログ ボックスで、次の操作を行います。  
  
    1.  **[名前]** ボックスにクエリ名を入力します。  
  
    2.  必要に応じて、 **[説明]** ボックスにクエリの説明を入力します。  
  
    3.  **[データ ソース]** ボックスの一覧で、名前付きクエリを実行するデータ ソースを選択します。  
  
    4.  下のペインでクエリを入力するか、グラフィカルなクエリ作成ツールを使用してクエリを作成します。  
  
    > [!NOTE]  
    >  クエリ作成ユーザー インターフェイス (UI) はデータ ソースによって異なります。 グラフィカルな UI ではなく、テキスト ベースの一般的な UI を入手できます。 これらのさまざまな UI の機能は同じですが、使用方法は異なります。 詳細については、「[[名前付きクエリの作成] または [名前付きクエリの編集] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](../create-or-edit-named-query-dialog-box-analysis-services-multidimensional-data.md)」をご覧ください。  
  
5.  **[OK]** をクリックします。 重なった 2 つのテーブルを示すアイコンがテーブル ヘッダーに表示され、そのテーブルが名前付きクエリに置換されたことを示します。  
  
## <a name="see-also"></a>参照  
 [多次元モデルのデータ ソース ビュー](data-source-views-in-multidimensional-models.md)   
 [データ ソース ビューでの名前付き計算の定義 (Analysis Services)](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
