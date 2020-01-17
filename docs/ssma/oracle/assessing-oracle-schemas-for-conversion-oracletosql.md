---
title: 変換 (OracleToSQL) のための Oracle スキーマの評価 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 0ff56be1b7da0376250c7ed021ae78d7144a7645
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264550"
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>変換のための Oracle Schemas へのアクセス (OracleToSQL)
オブジェクトを読み込むし、データを移行する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、複雑な移行されるとどれ時間だけを決定する必要があります、移行にかかる時間します。 SSMA は、正常に変換されるオブジェクトの割合を示す評価レポートを作成できます。 SSMA では、変換エラーが発生する特定の問題を表示することもできます。  
  
## <a name="creating-assessment-reports"></a>評価レポートを作成します。  
SSMA が選択されている Oracle データベースのオブジェクトを変換します、この評価レポートの作成時に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文とし、結果を示しています。  
  
**評価レポートを作成するには**  
  
1.  Oracle メタデータ エクスプ ローラーでは、評価するスキーマを選択します。  
  
2.  個々 のオブジェクトを省略するには、その横のチェック ボックスをオフにします。  
  
3.  右クリックして**スキーマ**、し、**レポートの作成**です。  
  
    、オブジェクトを右クリックして選択し、個々 のオブジェクトを分析することもできます。**レポートの作成**です。  
  
    SSMA は、ウィンドウの下部にあるステータス バーに進行状況が表示されます。 [出力] ペインが表示されている場合は、出力ウィンドウ内のメッセージも表示されます。  
  
    評価が完了すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle:評価レポート ウィンドウが表示されます。  
  
## <a name="using-assessment-reports"></a>評価レポートを使用します。  
評価レポート ウィンドウには、3 つのペインが含まれています。  
  
-   左側のウィンドウには、評価レポートに含まれているオブジェクトの階層が含まれています。 階層を参照し、オブジェクトと変換の統計情報とコードを表示するオブジェクトのカテゴリを選択できます。  
  
-   右側のウィンドウの内容は、左側のウィンドウで選択されている項目に依存します。  
  
    オブジェクトのグループが選択されている場合このようなスキーマでは、右側のペインがカテゴリ ウィンドウで、変換の統計ペインと、オブジェクトを表示するテーブルが選択されている場合またはします。 変換の統計ペインには、選択したオブジェクトの変換の統計情報が表示されます。 カテゴリ ウィンドウで、オブジェクトは、オブジェクトまたはオブジェクトのカテゴリの変換統計を表示します。  
  
    関数、パッケージ、プロシージャ、シーケンス、またはビューを選択すると、統計、ソース コード、およびターゲット コード右側のウィンドウが含まれます。  
  
    -   上部の領域には、オブジェクトの全体的な統計情報が表示されます。 展開する必要があります**統計**この情報を表示します。  
  
    -   ソース領域には、左側のウィンドウで選択されているオブジェクトのソース コードが表示されます。 強調表示された領域では、問題のあるソース コードを示します。  
  
    -   ターゲット領域には、変換後のコードが表示されます。 赤いテキストでは、問題のコードとエラー メッセージが表示されます。  
  
-   下部ペインには、メッセージ番号によってグループ化変換のメッセージが表示されます。 クリックすることができます**エラー**、**警告**、または**情報**メッセージのカテゴリを表示し、メッセージのグループを展開します。 左側のウィンドウで、オブジェクトを選択し、右側のウィンドウで詳細を表示する個々 のメッセージをクリックします。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>評価レポートを使用した変換の問題の分析  
変換の統計ペインには、変換の統計情報が表示されます。 任意のカテゴリの割合が 100% 未満の場合は、理由、変換に失敗しましたを決定する必要があります。  
  
**変換の問題を表示するには**  
  
1.  評価レポートを作成するには、前の手順で、手順を使用します。  
  
2.  左側のウィンドウで、スキーマまたは赤いエラー アイコンが表示されているフォルダーを展開します。 変換に失敗した個々 の項目を選択するまで項目を展開を続行します。  
  
3.  ソース ウィンドウの上部にある次のようにクリックします。**次の問題**します。  
  
    ターゲットのナビゲーション ウィンドウで、関連するコードは、問題のあるコードが強調表示されます。  
  
4.  すべてのエラー メッセージを確認し、変換の問題の原因となったオブジェクトで実行する内容を決定します。  
  
    -   SSMA で Oracle の構文を更新します。 プロシージャ、関数、トリガー、関数をパッケージおよびパッケージ化されたプロシージャの構文を更新することができます。 構文を更新するには、Oracle メタデータ エクスプ ローラー ペインで、オブジェクトを選択 をクリックして、 **SQL**タブをクリックし、SQL コードを変更します。 項目から移動するときに、更新された構文を保存する促されます。 オブジェクトの報告されたエラーを表示することができます、**レポート**タブ。  
  
    -   Oracle では、削除または問題のあるコードを変更するには Oracle のオブジェクトを変更できます。 SSMA に更新されたコードを読み込むには、メタデータを更新する必要があります。 詳細については、次を参照してください。 [Oracle データベースに接続する&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)します。  
  
    -   オブジェクトは、移行から除外できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーと Oracle メタデータ エクスプ ローラーにオブジェクトを読み込む前に、項目の横にあるチェック ボックスをオフ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と Oracle からデータを移行します。  
  
## <a name="next-step"></a>次の手順  
[Oracle スキーマの変換&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
