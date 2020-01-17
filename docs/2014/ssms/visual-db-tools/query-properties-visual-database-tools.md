---
title: クエリのプロパティ (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e9232f5de2172c7dfbe503a26188fdf4d05550c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011477"
---
# <a name="query-properties-visual-database-tools"></a>クエリのプロパティ (Visual Database Tools)
  クエリおよびビュー デザイナーでクエリを開くと、これらのプロパティが [プロパティ] ウィンドウに表示されます。 特に断りのない限り、このプロパティを [プロパティ] ウィンドウで編集できます。  
  
> [!NOTE]  
>  このトピックでは、アルファベット順ではなくカテゴリ別にプロパティが示されています。  
  
## <a name="options"></a>および  
 **[IDENTITY] カテゴリ**  
 展開して **[オブジェクト名]** プロパティを表示します。  
  
 **名前**  
 現在のクエリの名前を表示します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]では変更できません。  
  
 **データベース名**  
 選択したテーブルのデータ ソースの名前が表示されます。  
  
 **[サーバー名]**  
 データ ソースのサーバーの名前を表示します。  
  
 **[クエリ デザイナー] カテゴリ**  
 展開すると、その他のプロパティが表示されます。  
  
 **[ターゲット テーブル]**  
 データを挿入するテーブルの名前を指定します。 この一覧は、INSERT クエリまたは MAKE TABLE クエリを作成する場合に表示されます。 INSERT クエリの場合は、一覧でテーブル名を選択します。  
  
 MAKE TABLE クエリの場合は、新しいテーブルの名前を入力します。 テーブルを別のデータ ソースに作成する場合は、データ ソースの名前、所有者 (必要な場合)、テーブルの名前を含めた、完全修飾テーブル名を指定します。  
  
> [!NOTE]  
>  クエリ デザイナーは、名前が既に使用されているか、テーブルを作成する権限があるかなどの確認はしません。  
  
 **[一意の値]**  
 クエリが結果セットから重複した値を取り除くように指定します。 このオプションは、テーブルの一部の列だけを使用するときに、使用する列に重複した値が含まれる可能性のある場合、または 2 つ以上のテーブルを結合するプロセスによって結果セットに重複した行が生成される場合に便利です。 このオプションを選択することは、SQL ペインでステートメントに DISTINCT という単語を挿入することと同じです。  
  
 **[GROUP BY 拡張子]**  
 集計クエリに基づくクエリの追加オプションが使用できるように指定します。 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にのみ適用されます)。  
  
 **[すべての列を出力]**  
 現在のクエリのすべてのテーブルからすべての列を結果セットに含めるように指定します。 このオプションを選択することは、SQL ステートメントの SELECT キーワードの後でそれぞれの列名の代わりにアスタリスク (*) を指定することと同じです。  
  
 **[パラメーター リストのクエリ]**  
 クエリ パラメーターを表示します。 パラメーターを編集するには、プロパティをクリックして、プロパティの右側にある省略記号 ( **[...]** ) をクリックします。 汎用 OLE DB だけに適用されます。  
  
 **[SQL コメント]**  
 SQL ステートメントの説明を表示します。 説明全体を表示したり、説明を編集したりするには、説明をクリックして、プロパティの右側にある省略記号 ( **[...]** ) をクリックします。 クエリの使用者やクエリをいつ使用するかなどの情報をコメントに含めることもできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 以降のデータベースだけに適用されます。  
  
 **[Top の指定] カテゴリ**  
 展開すると、 **[Top]** 、 **[パーセント]** 、 **[式]** 、および **[With Ties]** の各プロパティが表示されます。  
  
 **[[(Top)]]**  
 クエリに TOP 句が含まれるように指定します。この場合、最初の *n* 行または最初の *n* % の行だけが結果セットに返されます。 既定では、クエリは最初の 10 行を結果セットに返します。  
  
 このボックスは、返される行数を変更するか、異なるパーセントを指定する場合に使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以降だけに適用されます。  
  
 **[式]**  
 クエリが返す行の数または割合を指定します。 **[パーセント]** を [はい] に設定すると、この数値はクエリが返す行の割合を表し、 **[パーセント]** を [いいえ] に設定すると、この数値はクエリが返す行の数を表します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 以降だけに適用されます。  
  
 **[パーセント]**  
 クエリが最初の *n* % の行だけを結果セットに返すように指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 以降だけに適用されます。  
  
 **[With Ties]**  
 ビューに WITH TIES 句を含むことを指定します。 WITH TIES は、ビューに ORDER BY 句とパーセンテージに基づく TOP 句が含まれる場合に便利です。 このオプションを設定すると、ORDER BY 句の列で同一の値を持つ行がセットになり、セットの一部の行がパーセンテージによる制限で切り捨てられてしまう場合は、すべての行が含まれるように、クエリで指定されるパーセンテージが増やされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 以降だけに適用されます。  
  
## <a name="see-also"></a>参照  
 [パラメーターを持つクエリ&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
