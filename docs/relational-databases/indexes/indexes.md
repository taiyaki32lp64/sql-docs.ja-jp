---
title: インデックス | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 899bd7aada6364449fa71e9f87839447de73dedd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909666"
---
# <a name="indexes"></a>インデックス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="available-index-types"></a>使用可能なインデックスの種類
次の表に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用できるインデックスの種類および追加情報へのリンクを示します。  
  
|インデックスの種類|[説明]|関連情報|  
|----------------|-----------------|----------------------------|  
|ハッシュ インデックス|ハッシュ インデックスの場合は、インメモリ ハッシュ テーブルを通じてデータにアクセスします。 ハッシュ インデックスは、バケット数の関数である固定量のメモリを消費します。|[メモリ最適化テーブルでのインデックス使用のガイドライン](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [ハッシュ インデックスのデザイン ガイドライン](../../relational-databases/sql-server-index-design-guide.md#hash_index)|  
|メモリ最適化された非クラスター化インデックス|メモリ最適化された非クラスター化インデックスの場合、メモリ消費量はインデックス キー列の行数とサイズによって決まります。|[メモリ最適化テーブルでのインデックス使用のガイドライン](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [メモリ最適化された非クラスター化インデックスのデザイン ガイドライン](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)|  
|クラスター化インデックス|クラスター化インデックス キーを基準に、テーブルまたはビューのデータ行を並べ替えて格納します。 クラスター化インデックスは、クラスター化インデックス キーの値を基にして行を高速に取得できる B ツリー インデックス構造として実装されます。|[クラスター化インデックスと非クラスター化インデックスの概念](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [クラスター化インデックスの作成](../../relational-databases/indexes/create-clustered-indexes.md)<br /><br /> [クラスター化インデックスのデザイン ガイドライン](../../relational-databases/sql-server-index-design-guide.md#Clustered)|  
|非クラスター化インデックス|非クラスター化インデックスが設定されたテーブルやビュー、またはヒープ上に定義できます。 非クラスター化インデックスの各インデックス行には、非クラスター化キーの値および行ロケーターが含まれています。 このロケーターは、キー値があるクラスター化インデックスまたはヒープのデータ行を指します。 インデックスの行はインデックス キーの値順に格納されますが、データ行は、クラスター化インデックスをテーブルに作成している場合以外は特定の順序に並ぶ保証はありません。|[クラスター化インデックスと非クラスター化インデックスの概念](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [非クラスター化インデックスの作成](../../relational-databases/indexes/create-nonclustered-indexes.md)<br /><br /> [非クラスター化インデックスのデザイン ガイドライン](../../relational-databases/sql-server-index-design-guide.md#Nonclustered)|  
|[一意]|インデックス キーの値が重複することがないので、テーブルまたはビューのすべての行をなんらかの方法で一意にすることができます。<br /><br /> クラスター化インデックスと非クラスター化インデックスは、どちらも一意にできます。|[一意のインデックスの作成](../../relational-databases/indexes/create-unique-indexes.md)<br /><br /> [一意インデックスのデザイン ガイドライン](../../relational-databases/sql-server-index-design-guide.md#Unique)|  
|列ストア|インメモリ columnstore インデックスは、列ベースのデータ ストレージと列ベースのクエリ処理を使用して、データを格納および管理します。<br /><br /> 列ストア インデックスは、主に一括読み込みと読み取り専用のクエリを実行するデータ ウェアハウスのワークロードで適切に動作します。 従来の行指向ストレージの最大 **10 倍のクエリ パフォーマンス** と、非圧縮データ サイズの最大 **7 倍のデータ圧縮** を達成するために列ストア インデックスを使用します。|[列ストア インデックス ガイド](../../relational-databases/indexes/columnstore-indexes-overview.md)<br /><br /> [列ストア インデックスのデザイン ガイドライン](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)|  
|付加列インデックス|キー列に加えて非キー列を付加できるように拡張した非クラスター化インデックスです。|[付加列インデックスの作成](../../relational-databases/indexes/create-indexes-with-included-columns.md)|  
|計算列のインデックス|その他の列の値 (複数可) から、または特定の決定的入力から導かれる列のインデックスです。|[計算列のインデックス](../../relational-databases/indexes/indexes-on-computed-columns.md)|  
|フィルター選択されたインデックス|最適化された非クラスター化インデックスです。このインデックスは、適切に定義されたデータのサブセットから選択するクエリに対応する際に特に適しています。 フィルター選択されたインデックスは、フィルター述語を使用して、テーブル内の一部の行にインデックスを作成します。 フィルター選択されたインデックスを適切にデザインすると、クエリのパフォーマンスが向上し、インデックスのメンテナンス コストを削減して、テーブル全体のインデックスと比較してインデックスのストレージ コストを削減することができます。|[フィルター選択されたインデックスの作成](../../relational-databases/indexes/create-filtered-indexes.md)<br /><br /> [フィルター選択されたインデックスのデザイン ガイドライン](../../relational-databases/sql-server-index-design-guide.md#Filtered)|  
|空間インデックス|空間インデックスを使用すると、*geometry*データ型の列に含まれる空間オブジェクト ( **空間データ** ) に対する一部の操作をより効率的に実行できます。 空間インデックスにより、比較的コストの高い空間操作を適用するオブジェクトの数を減らすことができます。|[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)|  
|XML|**xml** データ型列内の XML BLOB (binary large object) を細分化および永続化した表現です。|[XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)|  
|フルテキスト|Microsoft Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]により構築および管理されるトークンベースの特殊な機能インデックスです。 文字列データに対する高度な単語検索を効率的にサポートします。|[フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
 [SQL Server インデックス デザイン ガイド](../../relational-databases/sql-server-index-design-guide.md)      
 [インデックスの SORT_IN_TEMPDB オプション](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)     
 [インデックスと制約の無効化](../../relational-databases/indexes/disable-indexes-and-constraints.md)     
 [インデックスと制約の有効化](../../relational-databases/indexes/enable-indexes-and-constraints.md)    
 [インデックスの名前変更](../../relational-databases/indexes/rename-indexes.md)     
 [インデックス オプションの設定](../../relational-databases/indexes/set-index-options.md)     
 [インデックス DDL 操作に必要なディスク領域](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)     
 [インデックスの再構成と再構築](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)     
 [インデックスの FILL FACTOR の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)     
 [ページとエクステントのアーキテクチャ ガイド](../../relational-databases/pages-and-extents-architecture-guide.md)     
 [クラスター化インデックスと非クラスター化インデックスの概念](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
