---
title: 'レッスン 5: クレンジングと照合 SSIS を使用して自動化する |Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ec6f347cdbc6d14e8f621466a1708b8ee9fe7d36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489752"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>レッスン 5: SSIS を使用してクレンジングと照合を自動化する
  レッスン 1 で Suppliers ナレッジ ベースを構築し、レッスン 2 でデータをクレンジングし、ツールを使用して、レッスン 3 でのデータと一致するために使用**DQS クライアント**します。 実際のシナリオを使用しなくても、DQS がサポートしていないか、自動化、クレンジングするソースと一致するプロセスからデータをプルする必要があります、 **DQS クライアント**ツール。 SQL Server Integration Services (SSIS) が使用できるさまざまな異種ソースからデータを統合するコンポーネントと **[DQS クレンジング変換](https://msdn.microsoft.com/library/ee677619.aspx)** を呼び出す、クレンジング コンポーネントDQS によって公開される機能です。 現時点では、DQS を使用するには、SSIS 用の照合機能を公開しませんが、使用することができます、 **[あいまいグループ化変換](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** データの重複を識別するためにします。  
  
 データを MDS にアップロードするにを使用して、**エンティティ ベースのステージング機能**します。 MDS でエンティティを作成する場合、対応するステージング テーブルとストアド プロシージャが自動的に作成されます。 たとえば、Supplier エンティティの作成時に、 **stg.supplier_Leaf**テーブルおよび**stg.udp_Supplier_Leaf**ストアド プロシージャが自動的に作成されました。 ステージング テーブルとプロシージャを使用して、エンティティ メンバーを作成、更新、および削除できます。 このレッスンでは、Supplier エンティティの新しいエンティティ メンバーを作成します。 MDS サーバーにデータを読み込むには、最初に SSIS パッケージでデータをステージング テーブル stg.supplier_Leaf に読み込み、関連するストアド プロシージャ stg.udp_Supplier_Leaf をトリガーします。 参照してください[データのインポート](../master-data-services/overview-importing-data-from-tables-master-data-services.md)の詳細。  
  
 このレッスンでは、次のタスクを行います。  
  
1.  MDS で仕入先データを削除します (前の 4 レッスンを終了している場合)。 このレッスンで作成する SSIS パッケージにより、MDS に自動的にデータがアップロードされます。 前の手順では、DQS クライアントを使用して MDS サーバーに手動でクレンジングした照合仕入先データをアップロードしました。  
  
2.  他のアプリケーションのエンティティでデータを公開するために、Supplier エンティティでサブスクリプション ビューを作成します。 この操作により、SQL ビューを作成します。このビューは SQL Server Management Studio を使用して検証します。 このバージョンのチュートリアルでは、このビューを使用しません。  
  
3.  作成しを使用して SSIS プロジェクトを実行**SQL Server Data Tools**します。 プロジェクトを使用して**データ クレンジング**DQS サーバーにクレンジング要求を送信する変換。 DQS は公開しません照合機能を使用するため**あいまいグループ化**重複を識別するために変換します。  
  
4.  マスター データ マネージャーを使用して、MDS にデータが作成されていることを確認します。  
  
5.  SSIS パッケージによって作成された DQS クレンジング プロジェクトの結果を確認し、必要に応じてインタラクティブなクレンジングを実行して、ナレッジ ベースを拡充します。  
  
## <a name="next-step"></a>次の手順  
 [タスク 1&#40;前提条件となる&#41;:MDS の仕入先データを削除します。](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
