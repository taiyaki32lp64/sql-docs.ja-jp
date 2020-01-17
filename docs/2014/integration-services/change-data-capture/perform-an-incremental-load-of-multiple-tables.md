---
title: 複数のテーブルの増分読み込みを実行する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],multiple tables
ms.assetid: 39252dd5-09c3-46f9-a17b-15208cfd336d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d1549b8fa0979bba109c84485a89384722c82e7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835408"
---
# <a name="perform-an-incremental-load-of-multiple-tables"></a>複数のテーブルの増分読み込みを実行する
  「[変更データ キャプチャによる増分読み込みの向上](change-data-capture-ssis.md)」の図は、1 つのみのテーブルの増分読み込みを実行する基本的なパッケージを示しています。 ただし、1 つのテーブルの読み込みよりも、複数のテーブルの増分読み込みを実行する必要がある場合の方が一般的です。  
  
 複数のテーブルの増分読み込みを実行する場合の手順には、すべてのテーブルに対して一度実行する必要があるものと、ソース テーブルごとに繰り返し実行する必要があるものがあります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]でこれらの手順を実装する方法は複数あります。  
  
-   親パッケージと子パッケージを使用する。  
  
-   1 つのパッケージ内の複数のデータ フロー タスクを使用する。  
  
## <a name="loading-multiple-tables-by-using-a-parent-package-and-multiple-child-packages"></a>親パッケージと複数の子パッケージを使用した複数のテーブルの読み込み  
 親パッケージを使用して、一度実行するだけで済む手順を実行できます。 子パッケージでは、ソース テーブルごとに実行する必要がある手順を実行します。  
  
#### <a name="to-create-a-parent-package-that-performs-those-steps-that-only-have-to-be-done-once"></a>一度実行するだけで済む手順を実行する親パッケージを作成するには  
  
1.  親パッケージを作成します。  
  
2.  制御フローで、SQL 実行タスクまたは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式を使用してエンドポイントを計算します。  
  
     エンドポイントの計算方法の例については、「 [変更データの間隔を指定する](specify-an-interval-of-change-data.md)」を参照してください。  
  
3.  必要に応じて、選択した期間の変更データが準備できるまで実行を遅延させる For ループ コンテナーを使用します。  
  
     このような For ループ コンテナーの例については、「 [データの変更の準備ができているかどうかを判断する](determine-whether-the-change-data-is-ready.md)」を参照してください。  
  
4.  複数のパッケージ実行タスクを使用して、読み込むテーブルごとに子パッケージを実行します。 親パッケージ変数の構成を使用して、親パッケージで計算したエンドポイントを各子パッケージに渡します。  
  
     詳細については、「 [パッケージ実行タスク](../control-flow/execute-package-task.md) 」および「 [子パッケージでの変数およびパラメーターの値の使用](../use-the-values-of-variables-and-parameters-in-a-child-package.md)」を参照してください。  
  
#### <a name="to-create-child-packages-to-perform-those-steps-that-have-to-be-done-for-each-source-table"></a>ソース テーブルごとに実行する必要がある手順を実行する子パッケージを作成するには  
  
1.  ソース テーブルごとに子パッケージを作成します。  
  
2.  制御フローで、スクリプト タスクまたは SQL 実行タスクを使用して、変更をクエリで確認するために使用する SQL ステートメントを作成します。  
  
     クエリの作成方法の例については、「 [変更データのクエリを準備する](prepare-to-query-for-the-change-data.md)」を参照してください。  
  
3.  子パッケージごとに 1 つのデータ フロー タスクを使用して、変更データを読み込んで変換先に適用します。 次の手順に従って、データ フローを構成します。  
  
    1.  データ フローで、変換元コンポーネントを使用して、選択したエンドポイント内にある変更をクエリで変更テーブルから取得します。  
  
         変更テーブルに対するクエリの実行方法の例については、「 [変更データを取得および理解する](retrieve-and-understand-the-change-data.md)」を参照してください。  
  
    2.  条件分割変換を使用して、適切な処理のために挿入、更新、および削除を異なる出力に送信します。  
  
         この変換を構成して出力先を分ける方法の例については、「 [挿入、更新、および削除を処理する](process-inserts-updates-and-deletes.md)」を参照してください。  
  
    3.  変換先コンポーネントを使用して、挿入を変換先に適用します。 OLE DB コマンド変換とパラメーター化された UPDATE および DELETE ステートメントを使用して、更新と削除を変換先に適用します。  
  
         この変換を使用して更新と削除を適用する方法の例については、「 [変換先に変更を適用する](apply-the-changes-to-the-destination.md)」を参照してください。  
  
## <a name="loading-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>1 つのパッケージ内の複数のデータ フロー タスクを使用した複数のテーブルの読み込み  
 読み込むソース テーブルごとに個別のデータ フロー タスクを用意している 1 つのパッケージを使用することもできます。  
  
#### <a name="to-load-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>1 つのパッケージ内の複数のデータ フロー タスクを使用して複数のテーブルを読み込むには  
  
1.  1 つのパッケージを作成します。  
  
2.  制御フローで、SQL 実行タスクまたは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 式を使用してエンドポイントを計算します。  
  
     エンドポイントの計算方法の例については、「 [変更データの間隔を指定する](specify-an-interval-of-change-data.md)」を参照してください。  
  
3.  必要に応じて、選択した間隔の変更データが準備できるまで実行を遅延させる For ループ コンテナーを使用します。  
  
     このような For ループ コンテナーの例については、「 [データの変更の準備ができているかどうかを判断する](determine-whether-the-change-data-is-ready.md)」を参照してください。  
  
4.  スクリプト タスクまたは SQL 実行タスクを使用して、変更をクエリで確認するために使用する SQL ステートメントを作成します。  
  
     クエリの作成方法の例については、「 [変更データのクエリを準備する](prepare-to-query-for-the-change-data.md)」を参照してください。  
  
5.  複数のデータ フロー タスクを使用して、各ソース テーブルから変更データを読み込んで変換先に適用します。 次の手順に従って、各データ フロー タスクを構成します。  
  
    1.  各データ フローで、変換元コンポーネントを使用して、選択したエンドポイント内にある変更をクエリで変更テーブルから取得します。  
  
         変更テーブルに対するクエリの実行方法の例については、「 [変更データを取得および理解する](retrieve-and-understand-the-change-data.md)」を参照してください。  
  
    2.  条件分割変換を使用して、適切な処理のために挿入、更新、および削除を異なる出力に送信します。  
  
         この変換を構成して出力先を分ける方法の例については、「 [挿入、更新、および削除を処理する](process-inserts-updates-and-deletes.md)」を参照してください。  
  
    3.  変換先コンポーネントを使用して、挿入を変換先に適用します。 OLE DB コマンド変換とパラメーター化された UPDATE および DELETE ステートメントを使用して、更新と削除を変換先に適用します。  
  
         この変換を使用して更新と削除を適用する方法の例については、「 [変換先に変更を適用する](apply-the-changes-to-the-destination.md)」を参照してください。  
  
  
