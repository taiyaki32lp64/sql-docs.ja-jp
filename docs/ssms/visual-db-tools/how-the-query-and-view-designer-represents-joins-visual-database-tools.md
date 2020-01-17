---
title: クエリおよびビュー デザイナーでの結合の表示方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL pane [Visual Database Tools]
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 20a99dcb-83bd-4aa6-9139-92e2e5ba4887
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6318dfe2cc886e3ea2ea10d089023325ff074c95
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68254438"
---
# <a name="how-the-query-and-view-designer-represents-joins-visual-database-tools"></a>クエリおよびビュー デザイナーでの結合の表示方法 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
テーブルを結合すると、 [クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) は、 [ダイアグラム ペイン](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) にその結合をグラフィカル表示します。また、SQL 構文を使用して [SQL ペイン](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)にも表示します。  
  
## <a name="diagram-pane"></a>ダイアグラム ペイン  
ダイアグラム ペインでは、結合に関係するデータ列の間に結合線が引かれます。 結合条件ごとに 1 本の結合線が表示されます。 たとえば、次の図には結合された 2 つのテーブル間の結合線が示されています。  
  
![2 つのテーブル間のリレーションシップを示す結合線](../../ssms/visual-db-tools/media/dv3wbig.gif "2 つのテーブル間のリレーションシップを示す結合線")  
  
複数の結合条件を使用してテーブルが結合されている場合は、次の図に示すように、複数の結合線が表示されます。  
  
![複数の結合条件を使用して結合されたテーブル](../../ssms/visual-db-tools/media/dv3w9n1.gif "複数の結合条件を使用して結合されたテーブル")  
  
結合されたデータ列が表示されていない場合 (テーブルまたはテーブル構造オブジェクトを表す四角形が最小化されている場合や、結合に式が含まれる場合など)、クエリおよびビュー デザイナーは、テーブルまたはテーブル構造オブジェクトを表す四角形のタイトル バーに結合線を表示します。  
  
結合線の中央に表示されるアイコンの形は、テーブルまたはテーブル構造オブジェクトの結合方法を示しています。 等号 (=) 以外の演算子が結合句で使用されている場合は、その演算子が結合線のアイコンに表示されます。 結合線に表示されるアイコンは、次の表のとおりです。  
  
|**結合線のアイコン**|**[説明]**|  
|----------------------|-------------------|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbih.gif "Visual Database Tools のアイコン")|内部結合 (等号を使用して作成)。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbii.gif "Visual Database Tools のアイコン")|"大なり" 演算子 (>) による内部結合|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbij.gif "Visual Database Tools のアイコン")|外部結合。右側のテーブルに一致する行があるかどうかにかかわらず、左側のテーブルのすべての行が含められます。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbik.gif "Visual Database Tools のアイコン")|外部結合。左側のテーブルに一致する行があるかどうかにかかわらず、右側のテーブルのすべての行が含められます。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbil.gif "Visual Database Tools のアイコン")|完全外部結合。関連テーブルに一致する行があるかどうかにかかわらず、両方のテーブルのすべての行が含められます。|  
  
結合線の端に表示される記号は、結合の種類を示しています。 結合の種類と結合線の端に表示されるアイコンは、次の表のとおりです。  
  
|**結合線の端のアイコン**|**結合の種類**|  
|---------------------------------|--------------------|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbim.gif "Visual Database Tools のアイコン")|一対一結合。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbin.gif "Visual Database Tools のアイコン")|一対多結合。|  
|![Visual Database Tools のアイコン](../../ssms/visual-db-tools/media/dv3wbio.gif "Visual Database Tools のアイコン")|クエリおよびビュー デザイナーが特定できない種類の結合です。 この状態は、結合を手動で作成した場合に多く発生します。|  
  
## <a name="sql-pane"></a>SQL ペイン  
SQL ステートメントでは、さまざまな方法で結合を表現できます。 正確な構文は、使用するデータベースおよび結合を定義する方法によって異なります。  
  
テーブルの結合に使用する構文オプションは、次のとおりです。  
  
-   **FROM 句の JOIN 修飾子**。   キーワード INNER および OUTER で結合の種類を指定します。 この構文は、ANSI 92 SQL の標準です。  
  
    たとえば、 `publishers` テーブルと `pub_info` テーブルを両方のテーブルの `pub_id` 列に基づいて結合する場合、SQL ステートメントは次のようになります。  
  
    ```  
    SELECT *  
    FROM publishers INNER JOIN pub_info ON  
       publishers.pub_id = pub_info.pub_id  
    ```  
  
    外部結合を作成する場合は、INNER の代わりに LEFT OUTER または RIGHT OUTER というキーワードが使用されます。  
  
-   **WHERE 句による両テーブルの列の比較**。   データベースが JOIN 構文をサポートしていない場合、またはユーザーが自分で入力した場合には、WHERE 句が使用されます。 WHERE 句で結合が作成される場合は、FROM 句で両方のテーブルの名前が指定されます。  
  
    たとえば、 `publishers` テーブルと `pub_info` テーブルを結合するステートメントは、次のようになります。  
  
    ```  
    SELECT *  
    FROM publishers, pub_info  
    WHERE publishers.pub_id = pub_info.pub_id  
    ```  
  
## <a name="see-also"></a>参照  
[結合を使用したクエリ (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[[結合] ダイアログ ボックス (Visual Database Tools)](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
