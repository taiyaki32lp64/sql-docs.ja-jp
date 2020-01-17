---
title: ダイアグラム ペイン (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 00f4257a78b06d9f0ce3c21cb16ef04514eda76d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263854"
---
# <a name="diagram-pane-visual-database-tools"></a>ダイアグラム ペイン (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
ダイアグラム ペインには、データ接続で選択したテーブルまたはテーブル値オブジェクトが、グラフィカルに表示されます。 また、テーブル間の結合リレーションシップも示されます。  
  
ダイアグラム ペインでは、次の作業を行うことができます。  
  
-   テーブルおよびテーブル値オブジェクトを追加または削除し、出力するデータ列を指定する。  
  
-   テーブル間およびテーブル値オブジェクト間の結合を作成または変更する。  
  
ダイアグラム ペインで内容を変更すると、抽出条件ペインと SQL ペインはその変更に合わせて更新されます。 たとえば、ダイアグラム ペインのテーブルまたはテーブル値オブジェクトのウィンドウで出力する列を選択した場合、クエリおよびビュー デザイナーは、抽出条件ペインおよび SQL ペインの SQL ステートメントに、そのデータ列を追加します。  
  
ダイアグラム ペインでは、各テーブルまたはテーブル値オブジェクトは、独立したウィンドウとして表示されます。 各ウィンドウ (四角形) のタイトル バーに表示されるアイコンは、その四角形に表示されているオブジェクトの種類を示しています。各アイコンの意味は次のとおりです。  
  
## <a name="options"></a>オプション  
**テーブル**  
ダイアグラム ペインに追加できるテーブルが一覧表示されます。 テーブルを追加するには、テーブルを選択して **[追加]** をクリックします。 複数のテーブルを一度に追加するには、それらのテーブルを選択して **[追加]** をクリックします。  
  
**ビュー**  
ダイアグラム ペインに追加できるビューが一覧表示されます。 ビューを追加するには、ビューを選択して **[追加]** をクリックします。 複数のビューを一度に追加するには、それらのビューを選択して **[追加]** をクリックします。  
  
**関数**  
ダイアグラム ペインに追加できるユーザー定義関数が一覧表示されます。 関数を追加するには、関数を選択して **[追加]** をクリックします。 複数の関数を一度に追加するには、それらの関数を選択して **[追加]** をクリックします。  
  
**[ローカル テーブル]**  
データベースに属するクエリ以外のクエリで作成されたテーブルが一覧表示されます。  
  
**シノニム**  
ダイアグラム ペインに追加できるシノニムが一覧表示されます。 シノニムを追加するには、シノニムを選択して **[追加]** をクリックします。 複数のシノニムを一度に追加するには、それらのシノニムを選択して **[追加]** をクリックします。  
  
|アイコン|オブジェクトの種類|  
|--------|---------------|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbi1.gif "Visual Database Tools のアイコン")|テーブル|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbi2.gif "Visual Database Tools のアイコン")|クエリまたはビュー|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbi3.gif "Visual Database Tools のアイコン")|リンク テーブル|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dvudficon.gif "Visual Database Tools のアイコン")|ユーザー定義関数|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbi5.gif "Visual Database Tools のアイコン")|リンク ビュー|  
  
各四角形には、テーブルまたはテーブル値オブジェクトのデータ列が表示されます。 列の名前の横に表示されるチェック ボックスと記号は、その列がクエリでどのように使われるかを示しています。 ツール ヒントには、列のデータ型やサイズなどの情報が表示されます。  
  
テーブルまたはテーブル値オブジェクトの四角形で使用されるチェック ボックスと記号は、次の表のとおりです。  
  
|チェック ボックスまたは記号|[説明]|  
|-----------------------|---------------|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbi7.gif "Visual Database Tools のアイコン")<br /><br />![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbi8.gif "Visual Database Tools のアイコン")<br /><br />![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbi9.gif "Visual Database Tools のアイコン")<br /><br />![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbia.gif "Visual Database Tools のアイコン")|データ列をクエリの結果セットに表示するかどうか (選択クエリ)、または更新クエリ、結果の挿入クエリ、テーブルの作成クエリ、値の挿入クエリで使用するかどうかを指定します。 結果に列を追加するには、その列のチェック ボックスをオンにします。 **[すべての列]** を選択すると、すべてのデータ列が出力に表示されます。<br /><br />チェック ボックスに表示されるアイコンは、作成するクエリの種類によって変わります。 削除クエリを作成するときは、列を個別に選択することはできません。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbib.gif "Visual Database Tools のアイコン")<br /><br />![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbic.gif "Visual Database Tools のアイコン")|クエリ結果の並べ替えに使用される (ORDER BY 句の一部である) データ列を示します。 並べ替え順序が昇順の場合はアイコンに A-Z と表示されます。降順の場合は Z-A と表示されます。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbid.gif "Visual Database Tools のアイコン")|集計クエリで結果セットをグループ化するために使用される (GROUP BY 句の一部である) データ列を示します。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbie.gif "Visual Database Tools のアイコン")|クエリの検索条件に含まれる (WHERE 句または HAVING 句の一部である) データ列を示します。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbif.gif "Visual Database Tools のアイコン")|データ列の内容が出力のときに集約される (SUM、AVG、または他の集計関数に含まれる) ことを示します。|  
  
> [!NOTE]  
> テーブルまたはテーブル値オブジェクトに対して十分なアクセス権がない場合、またはデータベース ドライバーがこれらのオブジェクトに関する情報を返すことができない場合、クエリおよびビュー デザイナーにはこれらのオブジェクトのデータ列が表示されません。 この場合は、テーブルまたはテーブル構造オブジェクトのタイトル バーだけが表示されます。  
  
## <a name="joined-tables-on-the-diagram-pane"></a>ダイアグラム ペインでの結合テーブル  
クエリに結合が含まれる場合は、結合に関係するデータ列の間に結合の線が表示されます。 結合されるデータ列が表示されていない場合 (テーブルまたはテーブル値オブジェクトのウィンドウが最小化されている場合や、結合に式が含まれる場合など)、クエリおよびビュー デザイナーは、テーブルまたはテーブル値オブジェクトを表す四角形のタイトル バーに結合線を表示します。 結合条件ごとに 1 本の結合線が表示されます。  
  
結合線の中央に表示されるアイコンの形は、テーブルまたはテーブル構造オブジェクトの結合方法を示しています。 等号 (=) 以外の演算子が結合句で使われている場合は、その演算子が結合線のアイコンに表示されます。 結合線に表示されるアイコンは、次の表のとおりです。  
  
|結合線のアイコン|[説明]|  
|------------------|---------------|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbih.gif "Visual Database Tools のアイコン")|内部結合 (等号を使って作成)。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbii.gif "Visual Database Tools のアイコン")|"大なり" 演算子 (>) による内部結合 (結合線アイコンの内部には、結合で使われる演算子が表示されます)。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbij.gif "Visual Database Tools のアイコン")|外部結合。右側のテーブルに一致する行があるかどうかにかかわらず、左側のテーブルのすべての行が含められます。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbik.gif "Visual Database Tools のアイコン")|外部結合。左側のテーブルに一致する行があるかどうかにかかわらず、右側のテーブルのすべての行が含められます。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbil.gif "Visual Database Tools のアイコン")|完全外部結合。関連テーブルに一致する行があるかどうかにかかわらず、両方のテーブルのすべての行が含められます。|  
  
結合線の端に表示されるアイコンは、結合の種類を示しています。 結合の種類と結合線の端に表示されるアイコンは、次の表のとおりです。  
  
|結合線の端のアイコン|[説明]|  
|-----------------------------|---------------|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbim.gif "Visual Database Tools のアイコン")|一対一結合|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbin.gif "Visual Database Tools のアイコン")|一対多結合|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbio.gif "Visual Database Tools のアイコン")|クエリおよびビュー デザイナーが種類を特定できない結合|  
  
## <a name="see-also"></a>参照  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[抽出条件ペイン (Visual Database Tools)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[クエリ結果の並べ替えおよびグループ化 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
