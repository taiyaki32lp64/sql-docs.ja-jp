---
title: MDX クエリ エディター (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.mdx.f1
helpviewer_keywords:
- Query Editor [MDX]
- MDX Query Editor
ms.assetid: 777f2c23-1c1c-4b72-9d19-48a4866551f8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 579af162998ffaa7c9483a6e6d29a87f98e96fac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077878"
---
# <a name="mdx-query-editor-analysis-services---multidimensional-data"></a>MDX クエリ エディター (Analysis Services - 多次元データ)
  MDX クエリ エディターを使用すると、多次元式 (MDX) 言語で記述されたステートメントおよびスクリプトを作成および実行できます。  
  
## <a name="features"></a>機能のインストール  
  
-   MDX クエリ エディターのクエリ エディター ペインに、スクリプトを入力します。  
  
-   スクリプトを実行するには、 **F5**キーを押すか、ツール バーの **[実行]** をクリックします。または、 **[クエリ]** メニューの **[実行]** をクリックします。 コードの一部だけが選択されている場合、その部分だけが実行されます。 コードが選択されていない状態では、MDX クエリ エディターの内容全体が実行されます。  
  
-   メタデータ ペインには、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースに格納されているキューブなどのオブジェクトのメタデータが表示されます。  
  
-   MDX 構文のヘルプを表示するには、MDX クエリ エディター内でキーワードを選択し、 **F1**キーを押します。  
  
-   MDX 構文のダイナミック ヘルプを表示するには、 **[ヘルプ]** メニューの **[ダイナミック ヘルプ]** をクリックしてダイナミック ヘルプ コンポーネントを開きます。 ダイナミック ヘルプの場合、キーワードをクエリ エディターに入力すると、ヘルプ トピックが **[ダイナミック ヘルプ]** ウィンドウに表示されます。  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>[SQL Server Analysis Services エディター] ツール バー  
 MDX クエリ エディターが開いているときは、次の表に示すボタンを備えた [[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] エディター] ツール バーが表示されます。  
  
|項目|定義|  
|----------|----------------|  
|**Connect**|**インスタンスへの接続を確立するための** [サーバーへの接続] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ダイアログ ボックスを開きます。|  
|**[接続解除]**|MDX クエリ エディターと [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスの接続を解除します。|  
|**[接続の変更]**|別の **インスタンスへの接続を確立するための** [サーバーへの接続] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ダイアログ ボックスを開きます。|  
|**[新しいクエリを現在の接続で実行]**|現在の MDX クエリ エディター ウィンドウの接続情報を使用して、新しい MDX クエリ エディター ウィンドウを開きます。|  
|**[使用できるデータベース]**|接続を同じインスタンス上の別の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースに変更します。|  
|**実行**|選択されているコードを実行します。コードが選択されていない場合は、MDX クエリ エディター内のコード全体を実行します。|  
|**解析**|選択されているコードの構文をチェックします。 コードが選択されていない場合は、MDX クエリ エディター ウィンドウ内のコード全体の構文をチェックします。|  
|**[クエリ実行のキャンセル]**|キャンセル要求をサーバーに送信します。 即座にキャンセルできないクエリもあります。そのようなクエリは、適切なキャンセル条件が整うまでキャンセルできません。 クエリが取り消されると、トランザクションがロールバックされる間に遅延が発生することがあります。|  
  
## <a name="mdx-query-editor-window"></a>MDX クエリ エディター ウィンドウ  
 MDX クエリ エディター ウィンドウでは、次の表に示すオプションを使用できます。  
  
|項目|定義|  
|----------|----------------|  
|**クエリ エディター ウィンドウ**|MDX クエリ エディターで実行される MDX ステートメントおよびスクリプトを入力します。<br /><br /> クエリ エディターのコンテキスト メニューには、次のオプションがあります。<br /><br /> **[切り取り]** :現在選択している部分をクリップボードにコピーし、その部分をクエリ エディター ウィンドウから削除します。<br /><br /> **[コピー]** :現在選択している部分をクリップボードにコピーします。<br /><br /> **[貼り付け]** :クリップボードの内容を現在の選択位置に貼り付けます。<br /><br /> **[接続]** :**インスタンスへの接続を確立するための** [サーバーへの接続] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ダイアログ ボックスを開きます。<br /><br /> **[接続解除]** :現在のクエリ エディターと [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスの接続を解除します。<br /><br /> **[すべてのクエリの切断]** :現在開いているクエリ エディターの接続をすべて解除します。<br /><br /> **[接続の変更]** :別の **インスタンスへの接続を確立するための** [サーバーへの接続] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ダイアログ ボックスを開きます。<br /><br /> **[オブジェクト エクスプローラーでサーバーを開く]** :[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクト エクスプローラー **で、現在のクエリ エディターの接続先の**インスタンスを開きます。<br /><br /> **[実行]** :選択されているコードを実行します。コードが選択されていない場合は、現在のクエリ エディター内のコード全体を実行します。<br /><br /> **[プロパティ]** ウィンドウ:現在のクエリ ウィンドウの **に** [プロパティ] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ウィンドウを表示します。<br /><br /> **[クエリ オプション]** : **[クエリ オプション]** ダイアログ ボックスを表示します。|  
|**[メタデータ] ウィンドウ**|現在接続されている [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースのメタデータを表示します。|  
|**Cube**|現在接続されている [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベース内のキューブを選択して、キューブに関連付けられているメタデータを **[メタデータ]** タブに表示します。|  
|**メタデータ**|**[キューブ]** で選択されているキューブのメタデータ (メジャー グループとメジャー、主要業績評価指標、ディメンション、階層、レベル、メンバー、およびメンバー プロパティなど) を表示します。 オブジェクトの完全修飾キーを取得するには、次のどちらかの操作を行います。<br /><br /> オブジェクトを **[メタデータ]** タブからクエリ ペインにドラッグします。<br /><br /> オブジェクトを右クリックし、 **[コピー]** をクリックします。次に、クエリ ペインを右クリックし、 **[貼り付け]** をクリックします。|  
|**関数**|MDSCHEMA_FUNCTIONS スキーマ行セットから取得された、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースで使用できる MDX 関数のメタデータを表示します。 関数の構文を取得するには、次のどちらかの操作を行います。<br /><br /> オブジェクトを **[関数]** タブからクエリ ペインにドラッグします。<br /><br /> 関数を右クリックし、 **[コピー]** をクリックします。次に、クエリ ペインを右クリックし、 **[貼り付け]** をクリックします。|  
|**結果ウィンドウ**|MDX ステートメントまたはスクリプトの結果がグリッドに表示されます。|  
|**[メッセージ] ウィンドウ**|MDX ステートメントまたはスクリプトの実行に関する情報が表示されます。 たとえば、実行中に発生したエラーや、実行後に取得されたセルの数などが表示されます。|  
  
  
