---
title: 変換 (AccessToSQL) のための Access データベース オブジェクトの評価 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4c2f5bc6953ab0e96397ca728391cbe22a73dd50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910690"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>変換 (AccessToSQL) のための Access データベース オブジェクトの評価
オブジェクトを読み込むし、データを移行する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、確認してどの程度の移行は成功するになります、変換にどのくらいの時間がかかります。 SSMA を正常に変換されたオブジェクトの割合を示す評価レポートを作成できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の構文と時刻の評価、移行を実行します。 SSMA では、変換エラーの原因となった特定の問題を表示することもできます。  
  
## <a name="creating-assessment-reports"></a>評価レポートを作成します。  
SSMA 変換を選択した Access データベース オブジェクトで、評価レポートの作成時に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure の構文またはと結果を示しています。  
  
**評価レポートを作成するには**  
  
1.  メタデータ エクスプ ローラーでのアクセス、または、対象とする複数のデータベースを選択します。  
  
2.  個々 のオブジェクトを省略するには、評価したくないオブジェクトの横にあるチェック ボックスをオフにします。  
  
3.  右クリックして**データベース**、し、**レポートの作成**です。  
  
    オブジェクトを右クリックして選択し、個々 のオブジェクトを分析することもできます。**レポートの作成**です。  
  
    SSMA では、ウィンドウの下部にあるステータス バーで進行状況を示しています。 [出力] ペインが表示されている場合は、出力ウィンドウ内のメッセージも表示されます。  
  
評価が完了すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Access:評価レポート ウィンドウが表示されます。  
  
## <a name="using-assessment-reports"></a>評価レポートを使用します。  
評価レポート ウィンドウには、3 つのペインが含まれています。 エクスプ ローラー、詳細ウィンドウ、およびメッセージ ウィンドウ。  
  
-   エクスプ ローラー ペインを使用して、評価されたオブジェクトを参照できます。 個々 のテーブル、インデックス、およびキーにドリルダウンするには、このウィンドウ内の項目をクリックすることができます。  
  
-   詳細ウィンドウには、選択したオブジェクトの変換の統計情報が表示されます。  
  
-   メッセージ ウィンドウには、エラー、警告、および変換の情報メッセージが表示されます。 し、移行と個々 のエラー修正の手順を実行する時間を推定します。  
  
評価レポートを再実行したり、スキーマを変換したりする前に、エラーを修正する必要があります。 エラーを調べるには、**エラー** [メッセージ] ウィンドウで、ボタンをクリックし、エラーが発生したオブジェクトの一覧を表示するには、各エラーの順に展開します。 [メッセージ] ウィンドウ内のオブジェクトをクリックすると、すべてのエラーとそのオブジェクトの警告の詳細ウィンドウで表示されます。  
  
## <a name="next-step"></a>次の手順  
[Access データベース オブジェクトの変換](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
