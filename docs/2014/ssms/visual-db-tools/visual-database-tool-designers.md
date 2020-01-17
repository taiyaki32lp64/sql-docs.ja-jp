---
title: Visual Database Tools のデザイナー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- data sources [SQL Server]
- View Designer
- Visual Database Tools [SQL Server]
- Database Diagram Designer
- Query Designer [SQL Server]
- design tools [Visual Database Tools]
- Table Designer
- Visual Database Tools [SQL Server], designers
- Properties window [Visual Database Tools]
ms.assetid: bd0ca68e-6f69-42dd-bcb5-ce511673769c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 773ceb4aedddd6a39df6487bd36b47b83f7fa9a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63227042"
---
# <a name="visual-database-tool-designers"></a>Visual Database Tools のデザイナー
  Visual Database Tools は、データ ソースの処理に使用できるデザイン ツールの組み合わせです。 デザイン ツールを使用して、クエリの作成、データベース構造のデザインまたは変更、データの更新を実行できます。 ツールには、データベース ダイアグラム デザイナー、テーブル デザイナー、クエリおよびビュー デザイナーがあります。  
  
## <a name="properties-window"></a>[プロパティ] ウィンドウ  
 プロパティ ウィンドウは、Visual Database Tools に固有ではありませんが、このウィンドウを使用してさまざまな変更を実行できます。 プロパティ ウィンドウには、現在選択されている項目 (テーブルなど) のプロパティが表示され、そのプロパティ名や列の照合順序などのすべてのプロパティを編集できます。 プロパティ ウィンドウに表示できても、変更するには別のツールが必要になるプロパティもあります。  
  
## <a name="database-diagram-designer"></a>データベース ダイアグラム デザイナー  
 データベース ダイアグラム デザイナーには、データベース内のテーブルとリレーションシップを視覚的に作成、編集、および表示できるウィンドウが用意されています。  
  
 データベース ダイアグラム デザイナーを表示するには、既存のダイアグラムを開くか、オブジェクト エクスプローラーのデータベース ノードを右クリックして、ドロップダウン メニューの **[新しいデータベース ダイアグラム]** を選択します。  
  
 デザイナーが開くと、メイン メニューに **[データベース ダイアグラム]** メニューが表示されます。 このメニューから、デザイナーの特殊な機能にアクセスできます。  
  
> [!NOTE]  
>  このデザイナーは、Microsoft SQL Server データベースに使用します。  
>   
>  このバージョンの Visual Database Tools では、Microsoft SQL Server バージョン 7 以前はサポートされていません。  
  
## <a name="table-designer"></a>テーブル デザイナー (Table Designer)  
 テーブル デザイナーは、接続している Microsoft SQL Server データベースに含まれる 1 つのテーブルをデザインおよび視覚的にデザインできるビジュアル ツールです。  
  
 テーブル デザイナーには 2 つのペインがあります。 上の部分にはグリッドが表示されて、グリッドの各行はデータベースの 1 つの列を表しています。 グリッドの部分には、列名、データ型、null 値を許可するかどうかの設定など、各データベース列の基本的な属性が表示されます。  
  
 テーブル デザイナーの下部にある [列のプロパティ] タブには、上部で強調表示されている列の追加属性が表示されます。  
  
 テーブル デザイナーからは、グリッド セクションを右クリックしてダイアログ ボックスにアクセスし、テーブルのリレーションシップ、制約、インデックス、およびキーを作成したり変更したりできます。  
  
 テーブル デザイナーを表示するには、既存のテーブルを開くか、オブジェクト エクスプローラーの **[テーブル]** ノードを右クリックして、ドロップダウン メニューの **[新しいテーブルの追加]** を選択します。  
  
 デザイナーが開くと、メイン メニューに [テーブル デザイナー] メニューが表示されます。 このメニューから、デザイナーの特殊な機能にアクセスできます。  
  
> [!NOTE]  
>  このデザイナーは、Microsoft SQL Server データベースに使用します。  
>   
>  このバージョンの Visual Database Tools では、Microsoft SQL Server バージョン 7 以前はサポートされていません。  
  
## <a name="query-and-view-designer"></a>クエリおよびビュー デザイナー  
 クエリおよびビュー デザイナーは、実際には 2 つのツールで、よく似た動作をします。 主な違いの一部を次に示します。  
  
-   ビューはデータベースと共に保存されますが、クエリは Visual Studio データベース プロジェクトと共に保存されます。  
  
-   クエリ デザイナーはほぼすべてのデータ ソースに使用できますが、ビュー デザイナーは SQL Server だけに使用できます。  
  
-   クエリ デザイナーでは、SELECT、INSERT、UPDATE、および DELETE の DML ステートメントをデザインできますが、ビューで使用できるのは SELECT ステートメントだけです。  
  
### <a name="view-designer"></a>ビュー デザイナー  
 ビュー デザイナーを使用すると、既存のビューをデザインして視覚化したり、接続する Microsoft SQL Server データベースに新しいビューを作成したりできます。  
  
 ビュー デザイナーには、ダイアグラム ペイン、抽出条件ペイン、SQL ペイン、および結果ペインの 4 つのペインがあります。 これらのペインのそれぞれの詳細については、「[クエリおよびビュー デザイナー ツール (Visual Database Tools)](visual-database-tools.md)」を参照してください。  
  
 ビュー デザイナーを表示するには、既存のビューを開くか、オブジェクト エクスプローラーの **[ビュー]** ノードを右クリックして、ドロップダウン メニューの **[新しいビューの追加]** を選択します。  
  
 デザイナーが開くと、メイン メニューに **[クエリ デザイナー]** メニューが表示されます。 このメニューから、デザイナーの特殊な機能にアクセスできます。  
  
> [!NOTE]  
>  このデザイナーは、Microsoft SQL Server データベースに使用します。  
>   
>  このバージョンの Visual Database Tools では、Microsoft SQL Server バージョン 7 以前はサポートされていません。  
  
## <a name="see-also"></a>関連項目  
 [データベース ダイアグラムのデザイン&#40;Visual Database Tools&#41;](design-database-diagrams-visual-database-tools.md)   
 [テーブルのデザイン&#40;Visual Database Tools&#41;](design-tables-visual-database-tools.md)   
 [クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
