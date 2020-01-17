---
title: 変換 (SybaseToSQL) 用の SAP ASE データベース オブジェクトの評価 |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c65c19ee3b95303afb0e1ae0a950efe548c8f0af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083529"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>評価の SAP ASE データベース オブジェクトの変換 (SybaseToSQL)
オブジェクトを読み込むし、データを移行する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]判断した Azure SQL、または方法、移行の複雑さとどれだけ時間かかります。 SSMA は、オブジェクトとを正常に変換されるプロシージャの割合を示す評価レポートを作成できます[!INCLUDE[tsql](../../includes/tsql-md.md)]します。 SSMA では、変換エラーを引き起こす可能性のある特定の問題を表示することもできます。  
  
## <a name="create-assessment-reports"></a>評価レポートを作成します。  
この評価レポートを作成するには、SSMA、選択した SAP Adaptive Server Enterprise (ASE) データベース オブジェクトに変換します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL の構文、し、結果を表示しています。  
  
**評価レポートを作成するには**  
  
1.  Sybase メタデータ エクスプ ローラーでは、評価対象のデータベースを選択します。  
  
2.  個々 のオブジェクトを省略するには、評価したくないオブジェクトの横にあるチェック ボックスをオフにします。  
  
3.  右クリックして**データベース**、し、**レポートの作成**です。  
  
    、オブジェクトを右クリックして選択し、個々 のオブジェクトを分析することもできます。**レポートの作成**です。  
  
    SSMA では、ウィンドウの下部にあるステータス バーで進行状況を示しています。 [出力] ペインが表示されている場合は、関連するメッセージも表示されます。  
  
    評価が完了すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Sybase:評価レポート ウィンドウが表示されます。  
  
## <a name="use-assessment-reports"></a>評価レポートの使用  
評価レポート ウィンドウには、3 つのペインが含まれています。  
  
-   左側のウィンドウには、評価レポートに含まれているオブジェクトの階層が含まれています。 階層を参照し、オブジェクトと変換の統計情報とコードを表示するオブジェクトのカテゴリを選択できます。  
  
-   右側のウィンドウの内容は、左側のウィンドウで選択されたアイテムに基づいて異なります。  
  
    (スキーマ) などのオブジェクトまたはテーブルのグループが選択されている場合、右側のウィンドウには、2 つのペインが表示されます。 **変換統計**ウィンドウには、選択したオブジェクトの変換の統計情報が表示されます。 **カテゴリごとのオブジェクトの**ウィンドウには、オブジェクトまたはオブジェクトのカテゴリの変換の統計情報が表示されます。  
  
    ストアド プロシージャ、ビュー、またはトリガーを選択すると、統計、ソース コード、およびターゲット コード右側のウィンドウが含まれます。  
  
    -   上部の領域には、オブジェクトの全体的な統計情報が表示されます。 展開する必要があります**統計**この情報を表示します。 
    -   ソース領域には、左側のウィンドウで選択されているオブジェクトのソース コードが表示されます。 強調表示された領域では、問題のあるソース コードを示します。  
    -   ターゲット領域には、変換後のコードが表示されます。 赤いテキストでは、問題のコードとエラー メッセージが表示されます。  
  
-   下部ペインには、メッセージ番号によってグループ化変換のメッセージが表示されます。 選択**エラー**、**警告**、または**情報**メッセージのカテゴリを表示し、メッセージのグループを展開します。 右側のウィンドウで詳細を表示し、左側のウィンドウで、オブジェクトを選択する個々 のメッセージをクリックします。  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>評価レポートを使用して、変換の問題を分析します。  
**変換統計ペイン**変換統計情報を示します。 任意のカテゴリの割合が 100% 未満の場合は、理由、変換に失敗しましたを決定する必要があります。  
  
**変換の問題を表示するには**  
  
1.  評価レポートを作成するには、前の手順で、手順を使用します。  
  
2.  左側のウィンドウで、スキーマまたは赤いエラー アイコンが表示されているフォルダーを展開します。 変換に失敗した個々 の項目を選択するまで項目を展開を続行します。  
  
3.  ソース ウィンドウの上部にある次のように選択します。**次の問題**します。  
    問題のあるコードが強調表示され、関連のコードでは、**ターゲット ナビゲーション**ウィンドウ。  
  
4.  すべてのエラー メッセージを確認し、変換の問題の原因となったオブジェクトで実行する内容を決定します。  
  
    -   SSMA で ASE の構文を更新します。 ストアド プロシージャとトリガーのみに対して構文を更新することができます。 構文を更新するには、Sybase メタデータ エクスプ ローラー ペインで、オブジェクトを選択 をクリックして、 **SQL**タブをクリックし、SQL コードを編集します。 項目から移動するときに、更新された構文を保存するように求められます。 オブジェクトの報告されたエラーを表示、**レポート**タブ。  
  
    -   ASE では、削除または問題のあるコードを変更するには ASE オブジェクトを変更できます。 SSMA に更新されたコードを読み込むには、メタデータを更新する必要があります。 詳細については、次を参照してください。 [Sybase ASE への接続&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)します。  
  
    -   オブジェクトは、移行から除外できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL のメタデータ エクスプ ローラーと Sybase メタデータ エクスプ ローラーにオブジェクトを読み込む前に、項目の横にあるチェック ボックスをオフに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL と ASE からデータを移行します。
  
## <a name="next-steps"></a>次の手順  
[SAP ASE データベース オブジェクトの変換&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>参照  
[SQL Server - Azure SQL DB への SAP ASE データベースの移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
