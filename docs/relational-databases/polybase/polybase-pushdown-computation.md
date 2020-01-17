---
title: PolyBase でのプッシュダウン計算 | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 94e360c19c4f734b891701a4ec40c82cdb57927d
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710483"
---
# <a name="pushdown-computations-in-polybase"></a>PolyBase でのプッシュダウン計算

## <a name="dmv"></a>DMV (DMV)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

プッシュダウン計算を使用すると、Hadoop クラスター上でのクエリ パフォーマンスを改善できます。

## <a name="enable-pushdown"></a>プッシュダウンを有効にする

次の記事では、プッシュダウンを有効にするための手順が説明されています。

[Enable pushdown computation in Hadoop (Hadoop でのプッシュダウン計算を有効にする)](polybase-configure-hadoop.md#pushdown)

## <a name="select-a-subset-of-rows"></a>行のサブセットを選択する

外部テーブルから行のサブセットを選択するクエリのパフォーマンスを改善するには、述語のプッシュダウンを使用します。

この例では、SQL Server 2016 は map-reduce ジョブを開始して、Hadoop で述語 `customer.account_balance < 200000` である行を取得します。 このクエリは、テーブルのすべての行をスキャンせずに完了できるため、述語の条件に合う行のみが SQL Server にコピーされます。 この方法で時間が大幅に短縮され、残高が 200000 未満の顧客数が、口座残高が 200000 以上の顧客数と比較して少ない場合に、一時的な記憶域が少なくなります。

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>列のサブセットを選択する

外部テーブルから列のサブセットを選択するクエリのパフォーマンスを改善するには、述語のプッシュダウンを使用します。

このクエリでは、SQL Server で map-reduce ジョブを開始し、Hadoop の区切られたテキスト ファイルを前処理して、customer.name と customer.zip_code という 2 列のデータのみが SQL Server PDW にコピーされるようにします。

```sql
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>基本的な式と演算子のプッシュダウン

SQL Server では、述語のプッシュダウンに次の基本的な式と演算子を使用できます。

+ 数値、日付値、時間値の 2 項比較演算子 (\<、>、=、!=、<>、>=、<=)。

+ 算術演算子 (+、-、*、/、%)。

+ 論理演算子 (AND、OR)。

+ 単項演算子 (NOT、IS NULL、IS NOT NULL)。

演算子 BETWEEN、NOT、IN、LIKE はプッシュダウンできる場合があります。 実際の動作は、クエリ オプティマイザーが演算子式をどのように基本的な関係演算子を使用する一連のステートメントとして書き換えるかに依存します。

この例のクエリには、Hadoop にプッシュダウンできる述語が複数あります。 SQL Server は、map-reduce ジョブを Hadoop にプッシュして、述語 `customer.account_balance <= 200000` を実行できます。 `BETWEEN 92656 and 92677` の式もまた、Hadoop にプッシュできる 2 項演算子と論理演算子とで構成されます。 `customer.account_balance and customer.zipcode` 内の論理**積**が最後の式です。

この述語の組み合わせで、map-reduce ジョブですべての WHERE 句を実行できます。 SELECT 条件を満たすデータのみが SQL Server PDW にコピーされます。

```sql
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="force-pushdown"></a>プッシュダウンを強制する

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

## <a name="disable-pushdown"></a>プッシュダウンを無効にする

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>次の手順

PolyBase について詳しくは、「[PolyBase とは](polybase-guide.md)」をご覧ください。
