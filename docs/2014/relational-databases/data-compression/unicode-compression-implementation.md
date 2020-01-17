---
title: Unicode 圧縮の実装 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a43a437b277c0fcc090a4ebd52d9deb14bec9fd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872980"
---
# <a name="unicode-compression-implementation"></a>Unicode 圧縮の実装
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Standard Compression Scheme for Unicode (SCSU) アルゴリズムの実装を使用して、行またはページの圧縮オブジェクトに格納する Unicode 値を圧縮します。 これらの圧縮オブジェクトでは、`nchar(n)` 列および `nvarchar(n)` 列の Unicode 圧縮が自動的に行われます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、ロケールに関係なく、Unicode データが 2 バイトで格納されます。 これは UCS-2 エンコードと呼ばれています。 ロケールによっては、SQL Server の SCSU 圧縮実装で保存できる最大領域がストレージ領域の 50% になる場合があります。  
  
## <a name="supported-data-types"></a>サポートされるデータ型  
 Unicode 圧縮では、固定長の `nchar(n)` データ型および `nvarchar(n)` データ型がサポートされます。 行外または `nvarchar(max)` 列に格納されるデータ値は圧縮されません。  
  
> [!NOTE]  
>  行内に格納される場合であっても、`nvarchar(max)` データでは Unicode 圧縮がサポートされません。 ただし、このデータ型ではページ圧縮の利点を得ることができます。  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>以前のバージョンの SQL Server からのアップグレード  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードした場合、圧縮されているか圧縮されていないかにかかわらず、データベース オブジェクトに対して Unicode 圧縮に関連する変更は加えられません。 データベースのアップグレード後、オブジェクトには次のような影響があります。  
  
-   オブジェクトが圧縮されていない場合、何も変更は加えられず、オブジェクトは以前と同様に機能します。  
  
-   行またはページ圧縮されたオブジェクトは、以前と同様に機能します。 圧縮されていないデータは、値が更新されない限り、圧縮されていない形式のままになります。  
  
-   行またはページ圧縮されたテーブルに新しい行を挿入すると、Unicode 圧縮を使用して圧縮されます。  
  
    > [!NOTE]  
    >  Unicode 圧縮を十分に活用するには、ページまたは行の圧縮を使用してオブジェクトを再構築する必要があります。  
  
## <a name="how-unicode-compression-affects-data-storage"></a>Unicode 圧縮によるデータ ストレージへの影響  
 行またはページの圧縮で圧縮されているテーブル内で、インデックスが作成または再構築されたときや値が変更されたとき、その影響を受けたインデックスまたは値は、圧縮後のサイズが現在のサイズより小さくなる場合に限り、圧縮して格納されます。 これにより、Unicode 圧縮によってテーブルの行またはインデックスのサイズが大きくなる状況が回避されます。  
  
 圧縮により節約されるストレージ領域は、圧縮されるデータの特性とデータのロケールによって異なります。 次の表に、いくつかのロケールで節約できる領域の一覧を示します。  
  
|ロケール|圧縮率|  
|------------|-------------------------|  
|英語|50%|  
|ドイツ語|50%|  
|ヒンディー語|50%|  
|トルコ語|48%|  
|ベトナム語|39%|  
|日本語|15%|  
  
## <a name="see-also"></a>参照  
 [データの圧縮](data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql)   
 [ページの圧縮の実装](page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql)  
  
  
