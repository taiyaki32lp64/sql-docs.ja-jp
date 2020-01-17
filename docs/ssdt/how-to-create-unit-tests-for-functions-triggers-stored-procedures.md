---
title: 方法:関数、トリガー、ストアド プロシージャに対する SQL Server の単体テストを作成する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e1320cf0f6a0b27c1571d63c0432040294e8c68b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897180"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>方法:関数、トリガー、およびストアド プロシージャに対する SQL Server の単体テストを作成する
任意のデータベース オブジェクトに対する変更を評価する単体テストを作成できます。 ただし、SQL Server Data Tools には、SQL Server オブジェクト エクスプローラーのデータベース プロジェクト ノードから、データベースの関数、トリガー、およびストアド プロシージャのテストを作成するための追加サポートが含まれています。 Transact\-SQL コード スタブを自動的に生成して、カスタマイズすることができます。  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>関数、トリガー、またはストアド プロシージャから SQL Server の単体テストを作成するには  
  
1.  ストアド プロシージャの単体テストを追加する例については、「[チュートリアル:SQL Server の単体テストの作成と実行](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)」の「ストアド プロシージャに対して SQL Server の単体テストを作成するには」セクションを参照してください。  
  
    結果不確定のテスト条件は、すべてのテストに追加される既定の条件です。 このテスト条件は、テストの検証が実装されていないことを示すために含まれています。 このテスト条件は、他のテスト条件を追加した後に、テストから削除します。 詳細については、「[ソフト NUMA を使用するようにSQL Server の単体テストにテスト条件を追加する方法](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[方法:空の SQL Server の単体テストを作成する方法](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
