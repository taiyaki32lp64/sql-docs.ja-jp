---
title: PolyBase の機能と制限事項 | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd4c7e7bb150a0eafbd855e1703713f3781bdc49
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710452"
---
# <a name="polybase-features-and-limitations"></a>PolyBase の機能と制限事項

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

この記事は、SQL Server の製品やサービスで利用可能な PolyBase 機能の概要です。  
  
## <a name="feature-summary-for-product-releases"></a>製品リリースの機能の概要

PolyBase の主な機能と、これらの機能を利用できる製品を一覧表示した表を次に示します。  
  
||||||
|-|-|-|-|-|   
|**機能**|**SQL Server 2016**|**Azure SQL Database**|**Azure SQL Data Warehouse**|**Parallel Data Warehouse**| 
|で Hadoop データのクエリを実行する [!INCLUDE[tsql](../../includes/tsql-md.md)]|はい|いいえ|いいえ|はい|
|Hadoop からデータをインポートする|はい|いいえ|いいえ|はい|
|データを Hadoop にエクスポートする  |はい|いいえ|いいえ| はい|
|Azure HDInsight のクエリ、インポート、エクスポート |いいえ|いいえ|いいえ|いいえ
|クエリの計算を Hadoop にプッシュダウンする|はい|いいえ|いいえ|はい|  
|Azure Blob Storage からデータをインポートする|はい|いいえ|はい|はい| 
|Azure Blob Storage にデータをエクスポートする|はい|いいえ|はい|はい|  
|Azure Data Lake Store からデータをインポートする|いいえ|いいえ|はい|いいえ|    
|Azure Data Lake Store からデータをエクスポートする|いいえ|いいえ|はい|いいえ|
|Microsoft BI ツールから PolyBase クエリを実行する|はい|いいえ|はい|はい|   

## <a name="pushdown-computation-supported-by-t-sql-operators"></a>T-SQL 演算子でサポートされるプッシュダウン計算

SQL Server および APS では、すべての T-SQL 演算子を Hadoop クラスターにプッシュダウンできるわけではありません。 この表は、サポートされているすべての演算子と、サポートされていない演算子のサブセットを一覧表示しています。 

||||
|-|-|-| 
|**演算子の種類**|**Hadoop にプッシュ可能**|**Blob Storage にプッシュ可能**|
|列のプロジェクション|はい|いいえ|
|述語|はい|いいえ|
|集計|部分的|いいえ|
|外部テーブル間の結合|いいえ|いいえ|
|外部テーブルとローカル テーブル間の結合|いいえ|いいえ|
|並べ替え|いいえ|いいえ|

部分的な集計は、データが SQL Server に到達した後に、最終的な集計を行う必要があることを意味します。 ただし、集計の一部は、Hadoop で発生します。 これは、超並列処理システムで一般的な集計の計算方法です。  

## <a name="known-limitations"></a>既知の制限事項

PolyBase には次の制限事項があります。

- PolyBase を使用するには、データベースでの sysadmin または CONTROL SERVER レベルのアクセス許可が必要です。

- 可変長列の全長を含む最大行サイズは、SQL Server で 32 KB 以下、または Azure SQL Data Warehouse で 1 MB 以下にする必要があります。

- SQL Server または SQL Data Warehouse からデータが ORC ファイル形式にエクスポートされるときに、テキストの量が多い列が制限される可能性があります。 Java のメモリ不足エラー メッセージにより、わずか 50 列に制限される場合があります。 この問題を回避するには、列のサブセットだけをエクスポートします。

- KNOX が有効になっている場合、PolyBase は、Hortonworks インスタンスに接続できません。

- transactional = true の Hive テーブルを使用している場合、PolyBase は Hive テーブルのディレクトリにあるデータにアクセスできません。

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [SQL Server 2016 のフェールオーバー クラスターにノードを追加すると、PolyBase の機能をインストールできません](https://support.microsoft.com/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)。

::: moniker-end

## <a name="next-steps"></a>次の手順

PolyBase について詳しくは、「[PolyBase とは](polybase-guide.md)」をご覧ください。
