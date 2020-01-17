---
title: インデックス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58d4d71189598a6fd101e6db0a40b8c8b0a3b903
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63161865"
---
# <a name="indexes"></a>インデックス
  次の表に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用できるインデックスの種類および追加情報へのリンクを示します。  
  
|インデックスの種類|説明|関連情報|  
|----------------|-----------------|----------------------------|  
|ハッシュ インデックス|ハッシュ インデックスの場合は、インメモリ ハッシュ テーブルを通じてデータにアクセスします。 ハッシュ インデックスは、バケット数の関数である固定量のメモリを消費します。|[メモリ最適化テーブルでのインデックス使用のガイドライン](../in-memory-oltp/memory-optimized-tables.md)|  
|メモリ最適化された非クラスター化インデックス|メモリ最適化された非クラスター化インデックスの場合、メモリ消費量はインデックス キー列の行数とサイズによって決まります。|[メモリ最適化テーブルでのインデックス使用のガイドライン](../in-memory-oltp/memory-optimized-tables.md)|  
|クラスター化インデックス|クラスター化インデックス キーを基準に、テーブルまたはビューのデータ行を並べ替えて格納します。 クラスター化インデックスは、クラスター化インデックス キーの値を基にして行を高速に取得できる B ツリー インデックス構造として実装されます。|[クラスター化インデックスと非クラスター化インデックスの概念](clustered-and-nonclustered-indexes-described.md)<br /><br /> [クラスター化インデックスの作成](create-clustered-indexes.md)|  
|非クラスター化インデックス|非クラスター化インデックスが設定されたテーブルやビュー、またはヒープ上に定義できます。 非クラスター化インデックスの各インデックス行には、非クラスター化キーの値および行ロケーターが含まれています。 このロケーターは、キー値があるクラスター化インデックスまたはヒープのデータ行を指します。 インデックスの行はインデックス キーの値順に格納されますが、データ行は、クラスター化インデックスをテーブルに作成している場合以外は特定の順序に並ぶ保証はありません。|[クラスター化インデックスと非クラスター化インデックスの概念](clustered-and-nonclustered-indexes-described.md)<br /><br /> [非クラスター化インデックスの作成](create-nonclustered-indexes.md)|  
|[一意]|インデックス キーの値が重複することがないので、テーブルまたはビューのすべての行をなんらかの方法で一意にすることができます。<br /><br /> クラスター化インデックスと非クラスター化インデックスは、どちらも一意にできます。|[一意のインデックスの作成](create-unique-indexes.md)|  
|列ストア|インメモリ columnstore インデックスは、列ベースのデータ ストレージと列ベースのクエリ処理を使用して、データを格納および管理します。<br /><br /> 列ストア インデックスは、主に一括読み込みと読み取り専用のクエリを実行するデータ ウェアハウスのワークロードで適切に動作します。 従来の行指向ストレージの最大 **10 倍のクエリ パフォーマンス** と、非圧縮データ サイズの最大 **7 倍のデータ圧縮** を達成するために列ストア インデックスを使用します。|[列ストア インデックスの説明](columnstore-indexes-described.md)<br /><br /> [非クラスター化列ストア インデックスの使用](../../database-engine/using-nonclustered-columnstore-indexes.md)<br /><br /> [クラスター化列ストア インデックスの使用](../../database-engine/using-clustered-columnstore-indexes.md)|  
|付加列インデックス|キー列に加えて非キー列を付加できるように拡張した非クラスター化インデックスです。|[付加列インデックスの作成](create-indexes-with-included-columns.md)|  
|計算列のインデックス|その他の列の値 (複数可) から、または特定の決定的入力から導かれる列のインデックスです。|[計算列のインデックス](indexes-on-computed-columns.md)|  
|フィルター選択されたインデックス|最適化された非クラスター化インデックスです。このインデックスは、適切に定義されたデータのサブセットから選択するクエリに対応する際に特に適しています。 フィルター選択されたインデックスは、フィルター述語を使用して、テーブル内の一部の行にインデックスを作成します。 フィルター選択されたインデックスを適切にデザインすると、クエリのパフォーマンスが向上し、インデックスのメンテナンス コストを削減して、テーブル全体のインデックスと比較してインデックスのストレージ コストを削減することができます。|[フィルター選択されたインデックスの作成](create-filtered-indexes.md)|  
|空間インデックス|空間インデックスを使用すると、*geometry*データ型の列に含まれる空間オブジェクト ( **空間データ** ) に対する一部の操作をより効率的に実行できます。 空間インデックスにより、比較的コストの高い空間操作を適用するオブジェクトの数を減らすことができます。|[空間インデックスの概要](../spatial/spatial-indexes-overview.md)|  
|XML|`xml` データ型列内の XML BLOB (binary large object) を細分化および永続化した表現です。|[XML インデックス &#40;SQL Server&#41;](../xml/xml-indexes-sql-server.md)|  
|フルテキスト|Microsoft Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]により構築および管理されるトークンベースの特殊な機能インデックスです。 文字列データに対する高度な単語検索を効率的にサポートします。|[フルテキスト インデックスの作成](../search/populate-full-text-indexes.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
## <a name="related-content"></a>関連コンテンツ  
 [インデックスの SORT_IN_TEMPDB オプション](sort-in-tempdb-option-for-indexes.md)  
  
 [インデックスと制約の無効化](disable-indexes-and-constraints.md)  
  
 [インデックスと制約の有効化](enable-indexes-and-constraints.md)  
  
 [インデックスの名前変更](rename-indexes.md)  
  
 [インデックス オプションの設定](set-index-options.md)  
  
 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)  
  
 [インデックスの再編成と再構築](reorganize-and-rebuild-indexes.md)  
  
 [インデックスの FILL FACTOR の指定](specify-fill-factor-for-an-index.md)  
  
## <a name="see-also"></a>参照  
 [クラスター化インデックスと非クラスター化インデックスの概念](clustered-and-nonclustered-indexes-described.md)  
  
  
