---
title: CLR 統合のパフォーマンス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: eced622903a0d68369f28d19ff521d99bcedbdc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874521"
---
# <a name="performance-of-clr-integration"></a>CLR 統合のパフォーマンス
  このトピックではいくつかのパフォーマンスを強化する設計上の選択肢の[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]との統合、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 共通言語ランタイム (CLR)。  
  
## <a name="the-compilation-process"></a>コンパイル処理  
 SQL 式のコンパイル時に、マネージド ルーチンへの参照が検出されると、MSIL ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] Intermediate Language) スタブが生成されます。 このスタブには、ルーチン パラメーターを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から CLR にマーシャリングして関数を呼び出し、結果を返すコードが含まれています。 この "グルー" (接着剤) コードは、パラメーターの型とパラメーターの方向 (入力、出力、または参照) に基づいています。  
  
 グルー コードを使用することで、型固有の最適化を行い、NULL 値の許容、制約ファセット、値渡し、標準の例外処理などの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セマンティクスを効率的に適用できます。 引数に真数型を使用するコードを生成することで、複数の呼び出しにまたがる型の強制またはラッパー オブジェクト作成によるコストを回避 ("ボックス化") できます。  
  
 生成されたスタブは、CLR の JIT (just-in-time) コンパイル サービスによって、ネイティブ コードへのコンパイル、および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行している特定のハードウェア アーキテクチャに合わせた最適化が行われます。 JIT サービスはメソッド レベルで呼び出され、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と CLR 両方を実行するための単一のコンパイル単位を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ホスティング環境で作成できます。 スタブをコンパイルすると、コンパイルされた関数のポインターが関数の実行時の実装になります。 このコード生成方式によって、実行時にリフレクションやメタデータのアクセスのために追加の呼び出しを行うコストを回避することができます。  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>SQL Server と CLR の高速切り替え  
 コンパイル処理の結果、実行時にネイティブ コードから呼び出すことのできる関数ポインターが生成されます。 ユーザー定義スカラー値関数の場合、関数が行ごとに呼び出されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と CLR の切り替えコストを最小限にするために、マネージド呼び出しを行うステートメントには対象になるアプリケーション ドメインを識別する起動処理があります。 この識別処理により、行ごとの切り替えコストを抑えます。  
  
## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項  
 次に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の CLR 統合固有のパフォーマンスに関する考慮事項を要約します。 詳細な情報が記載されて"[SQL Server 2005 の CLR 統合を使用して](https://go.microsoft.com/fwlink/?LinkId=50332)"MSDN Web サイト。 マネージ コードのパフォーマンスに関する一般的な情報が見つかりません"[.NET アプリケーションのパフォーマンスとスケーラビリティ](https://go.microsoft.com/fwlink/?LinkId=50333)"MSDN Web サイト。  
  
### <a name="user-defined-functions"></a>ユーザー定義関数  
 CLR 関数は、[!INCLUDE[tsql](../../../includes/tsql-md.md)] のユーザー定義関数に比べて呼び出し手順が速いという利点があります。 また、マネージド コードはプロシージャ コード、計算、および文字列操作のパフォーマンスが [!INCLUDE[tsql](../../../includes/tsql-md.md)] に比べて決定的に優れています。 計算中心の CLR 関数およびデータ アクセスを行わない CLR 関数は、マネージド コードで記述する方が適切です。 ただし、データ アクセスは [!INCLUDE[tsql](../../../includes/tsql-md.md)] 関数の方が CLR 統合に比べて効率的です。  
  
### <a name="user-defined-aggregates"></a>ユーザー定義集計  
 マネージド コードを使用すると、カーソル ベースの集計よりも大幅に優れたパフォーマンスを発揮できます。 一般的には、組み込みの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 集計関数に比べてマネージド コードはわずかに低速です。 ネイティブの組み込み集計関数が存在する場合は、その関数を使用することをお勧めします。 必要な集計がネイティブにサポートされていない場合、パフォーマンス上の理由からカーソル ベースの実装よりも CLR ユーザー定義集計の使用を検討してください。  
  
### <a name="streaming-table-valued-functions"></a>テーブル値関数のストリーミング  
 関数を呼び出した結果として、テーブルを返す必要性が生じる場合がよくあります。 たとえば、インポート操作の一環としてファイルから表形式のデータを読み取る場合や、コンマ区切りの値をリレーショナル表現に変換する場合などです。 一般的に、このような作業を実現するには、テーブルを呼び出し元で使用する前に、結果テーブルを具体化して値を格納する必要があります。 CLR を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に統合することで、STVF (ストリーミング テーブル値関数) という新しい拡張方式を使用できます。 マネージド STVF は、同様の拡張ストアド プロシージャを実装した場合に比べて、優れたパフォーマンスを発揮します。  
  
 STVF は、`IEnumerable` インターフェイスを返すマネージド関数です。 `IEnumerable` には STVF が返した結果セットの中を移動するメソッドがあります。 STVF を呼び出して返される `IEnumerable` は、クエリ プランに直接接続されます。 クエリ プランで行のフェッチが必要になると、`IEnumerable` のメソッドが呼び出されます。 このような反復的なモデルにより、テーブル全体に値が格納されるまで待たなくても、最初の行が生成された直後から結果を使用できます。 関数の呼び出しに伴うメモリの消費を大幅に抑えることもできます。  
  
### <a name="arrays-vs-cursors"></a>配列とします。カーソル  
 配列として簡単に表現できるデータを [!INCLUDE[tsql](../../../includes/tsql-md.md)] カーソルでスキャンする必要がある場合、マネージド コードを使用するとパフォーマンスが大幅に向上します。  
  
### <a name="string-data"></a>文字列データ  
 `varchar` などの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 文字データは、マネージド関数では SqlString 型または SqlChars 型にすることができます。 SqlString 変数は値全体のインスタンスをメモリに作成します。 SqlChars 変数には、ストリーミング インターフェイスが用意されており、これを使用すると、値全体のインスタンスをメモリに作成しないことでパフォーマンスおよびスケーラビリティを高めることができます。 このことは、特に LOB (ラージ オブジェクト) データにとって重要です。 また、`SqlXml.CreateReader()` が返すストリーミング インターフェイスを経由すると、サーバーの XML データにアクセスできます。  
  
### <a name="clr-vs-extended-stored-procedures"></a>CLR とします。拡張ストアド プロシージャ  
 マネージド プロシージャから結果セットをクライアントに返す Microsoft.SqlServer.Server API (アプリケーション プログラミング インターフェイス) は、拡張ストアド プロシージャにより使用される ODS (オープン データ サービス) API に比べパフォーマンスに優れています。 また、System.Data.SqlServer API は [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入された `xml`、`varchar(max)`、`nvarchar(max)`、`varbinary(max)` などのデータ型をサポートしていますが、ODS API ではこれらの新しいデータ型をサポートするための拡張が行われていません。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではマネージド コードによってメモリ、スレッド、同期などのリソースの使用状況が管理されます。 これらのリソースを公開するマネージド API が、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソース マネージャーの上位に実装されるためです。 逆に、拡張ストアド プロシージャは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によってリソースの使用状況が監視または制御されることがありません。 たとえば、拡張ストアド プロシージャで大量の CPU リソースまたはメモリ リソースが消費されていても、それを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で検出したり制御することはできません。 一方、マネージド コードでは、特定のスレッドが長期間リソースを占有していることを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で検出して、タスクからリソースを解放し、他の作業のスケジュールを設定できるようになります。 つまり、マネージド コードを使用すると、スケーラビリティやシステム リソースの使用状況が改善されます。  
  
 マネージド コードを使用すると、実行環境の保持およびセキュリティ チェックの実施に必要なオーバーヘッドが発生することがあります。 たとえば、([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はネイティブ コードと行き来する際にスレッド固有の設定を保つ必要があるので、) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内でコードを実行し、マネージド コードとネイティブ コードの切り替えを何度も行う必要がある場合などにオーバーヘッドが生じます。 つまり、マネージド コードとネイティブ コードの切り替えが頻発する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内で実行されるマネージド コードに比べて、拡張ストアド プロシージャの方が高いパフォーマンスを発揮できます。  
  
> [!NOTE]  
>  この機能の使用は非推奨とされるため、拡張ストアド プロシージャを新規作成しないことをお勧めします。  
  
### <a name="native-serialization-for-user-defined-types"></a>ユーザー定義型のネイティブ シリアル化  
 UDT (ユーザー定義型) は、スカラー型システムの拡張方式として設計されています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には `Format.Native` という UDT のシリアル化形式が実装されています。 コンパイルのとき、型の定義に合わせてカスタマイズされた MSIL を生成するために型の構造を検査します。  
  
 ネイティブ シリアル化は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既定の実装です。 ユーザー定義のシリアル化を行うと、型の作成者がシリアル化のために定義したメソッドが呼び出されます。 最高のパフォーマンスを得るには、`Format.Native` シリアル化をできる限り使用してください。  
  
### <a name="normalization-of-comparable-udts"></a>同等の UDT の正規化  
 UDT の並べ替え、比較などのリレーショナル操作で、値のバイナリ表現を直接操作します。 これを行うには、ディスクに UDT の状態を正規化した (バイナリ順にした) 表現を格納します。  
  
 正規化には 2 つの利点があります。1 つは、型のインスタンスの作成やメソッド呼び出しのオーバヘッドが発生しないようにすることで比較操作のコストが大幅に抑えられることです。もう 1 つは、UDT のバイナリ領域が作成され、ヒストグラム、インデックス、およびその型の値のヒストグラムが作成できるようになることです。 つまり、メソッド呼び出しを伴わない操作では、正規化した UDT はネイティブの組み込み型と変わらないパフォーマンスを発揮します。  
  
### <a name="scalable-memory-usage"></a>スケーラビリティを確保するメモリの使用方法  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のマネージド ガベージ コレクションのパフォーマンスやスケーラビリティを高めるには、大量のメモリを 1 単位として割り当てないようにしてください。 88 KB を超える割り当てはラージ オブジェクト ヒープに配置されます。その結果、小規模の割り当てをいくつも行った場合に比べて、ガベージ コレクションのパフォーマンスやスケーラビリティが低下します。 たとえば、大きな多次元配列を割り当てる場合、ジャグ (散在した) 配列を割り当てることをお勧めします。  
  
## <a name="see-also"></a>関連項目  
 [CLR ユーザー定義型](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
