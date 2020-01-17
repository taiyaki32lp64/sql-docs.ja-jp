---
title: クラスター化インデックスと非クラスター化インデックスの概念 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- query optimizer [SQL Server], index usage
- index concepts [SQL Server]
ms.assetid: b7d6b323-728d-4763-a987-92e6292f6f7a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3b0fdb182b3623f4461544d94347544d7d19bf6
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811129"
---
# <a name="clustered-and-nonclustered-indexes-described"></a>クラスター化インデックスと非クラスター化インデックスの概念

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

インデックスとは、テーブルまたはビューに関連付けられたディスク上の構造で、テーブルやビューからの行の取得を高速化します。 インデックスには、テーブル内またはビュー内の 1 つ以上の列から構築されたキーが含まれています。 これらのキーは 1 つの構造 (B-Tree) 内に格納され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はその構造を使用して、キー値に関連した 1 つ以上の行を効率よく迅速に検出できます。

テーブルまたはビューには、次の種類のインデックスを含めることができます。

- クラスター化インデックス

  - クラスター化インデックスは、テーブルまたはビュー内のデータ行をそのキー値に基づいて並べ替え、格納します。 クラスター化インデックスは、インデックス定義に含まれる列です。 データ行自体は 1 つの順序でしか並べ替えられないので、1 つのテーブルに設定できるクラスター化インデックスは 1 つだけです。  
  - テーブル内のデータ行が並べ替えられた順に格納されるのは、テーブルにクラスター化インデックスが含まれているときだけです。 テーブルにクラスター化インデックスが含まれている場合、そのテーブルをクラスター化テーブルと呼びます。 クラスター化インデックスが含まれないテーブルのデータ行は、ヒープと呼ばれる順序付けられていない構造に格納されます。

- 非クラスター化インデックス

  - 非クラスター化インデックスは、データ行とは独立した構造になっています。 非クラスター化インデックスには、非クラスター化インデックスのキー値が含まれており、各キー値のエントリにはキー値が含まれているデータ行へのポインターが含まれています。
  - 非クラスター化インデックス内のインデックス行からデータ行を指すポインターを、行ロケーターと呼びます。 行ロケーターの構造は、データ ページがヒープまたはクラスター化テーブルのどちらに格納されているかによって異なります。 ヒープに格納されている場合、行ロケーターは行を指すポインターです。 クラスター化テーブルに格納されている場合、行ロケーターはクラスター化インデックス キーです。

  - 非キー列をリーフ レベルの非クラスター化インデックスに追加することで、既存のインデックス キーの制限を回避して、すべてを対象とするインデックスが設定されたクエリを実行できます。 詳細については、「 [付加列インデックスの作成](../../relational-databases/indexes/create-indexes-with-included-columns.md)」を参照してください。 インデックス キーの制限の詳細については、「[SQL Server の最大容量仕様](../../sql-server/maximum-capacity-specifications-for-sql-server.md)」を参照してください。

クラスター化インデックスと非クラスター化インデックスは共に一意インデックスにできます。 つまり、2 つの行がインデックス キーに同じ値を持つことができなくなります。 一意インデックスにしない場合、インデックスは一意でなくなり、複数の行が同じキー値を共有できます。 詳細については、「 [一意のインデックスの作成](../../relational-databases/indexes/create-unique-indexes.md)」を参照してください。

テーブル データが変更されるたびに、テーブルまたはビューのインデックスが自動的にメンテナンスされます。

特別な用途のインデックスのその他の種類については、「 [インデックス](../../relational-databases/indexes/indexes.md) 」を参照してください。

## <a name="indexes-and-constraints"></a>インデックスと制約

PRIMARY KEY 制約と UNIQUE 制約がテーブル列に定義されると、インデックスが自動的に作成されます。 たとえば、UNIQUE 制約があるテーブルを作成すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって非クラスター化インデックスが自動的に作成されます。 PRIMARY KEY を構成した場合、クラスター化インデックスが既に存在しない限り、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって自動的に作成されます。 既存のテーブルに PRIMARY KEY 制約を適用しようとしたときに、そのテーブルにクラスター化インデックスが既に存在する場合、SQL Server によって、非クラスター化インデックスを使用するプライマリ キーが適用されます。

詳細については、「 [主キーの作成](../../relational-databases/tables/create-primary-keys.md) 」および「 [UNIQUE 制約の作成](../../relational-databases/tables/create-unique-constraints.md)」を参照してください。

## <a name="how-indexes-are-used-by-the-query-optimizer"></a>クエリ オプティマイザーでのインデックスの使用方法

インデックスを適切に設計すると、ディスク I/O 操作が減少し、使用するシステム リソースが少なくなります。その結果、クエリのパフォーマンスが向上します。 インデックスは、SELECT、UPDATE、DELETE、または MERGE の各ステートメントを含むさまざまなクエリで役立ちます。 `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` データベースのクエリ [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] について考えてみましょう。 このクエリが実行されるときに、クエリ オプティマイザーでは、データの取得に使用できる方法がそれぞれ評価され、最も効率的な方法が選択されます。 選択される方法には、テーブルのスキャン、1 つ以上のインデックスのスキャン (存在する場合) などがあります。

テーブル スキャンを実行すると、クエリ オプティマイザーでテーブルのすべての行が読み取られ、クエリの条件を満たす行が抽出されます。 テーブル スキャンでは、ディスク I/O 操作が数多く行われ、リソースが集中的に使用される可能性があります。 ただし、クエリの結果セットに大部分のテーブル行が含まれる場合などは、テーブル スキャンが最も効率的な方法になることがあります。

クエリ オプティマイザーでインデックスが使用されるときは、インデックス キー列が検索され、クエリで必要とされる行のストレージの場所が検索されて、一致する行がその場所から抽出されます。 一般に、インデックスの検索はテーブルの検索よりも高速です。これは、テーブルとは異なり、多くの場合、インデックスでは各行にごく少数の列しか含まれず、行が既に並べ替え済みであるためです。

 クエリ オプティマイザーでは、通常、クエリを実行するときに最も効率的な方法が選択されます。 ただし、インデックスが使用できなければ、クエリ オプティマイザーではテーブル スキャンを使用する必要があります。 クエリ オプティマイザーが効率的なインデックスを選択できるように、環境に最も適したインデックスを設計および作成する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][データベース エンジン チューニング アドバイザー](../../relational-databases/performance/database-engine-tuning-advisor.md) が用意されており、データベース環境の分析や適切なインデックスの選択に役立てることができます。

> [!IMPORTANT]
> インデックスの設計のガイドラインおよび内部構造の詳細については、「[SQL Server インデックス デザイン ガイド](../../relational-databases/sql-server-index-design-guide.md)」を参照してください。

## <a name="related-content"></a>関連コンテンツ

- [SQL Server インデックス デザイン ガイド](../../relational-databases/sql-server-index-design-guide.md)
- [クラスター化インデックスの作成](../../relational-databases/indexes/create-clustered-indexes.md)
- [非クラスター化インデックスの作成](../../relational-databases/indexes/create-nonclustered-indexes.md)
