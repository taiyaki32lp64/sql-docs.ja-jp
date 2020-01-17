---
title: インメモリ OLTP のサンプル データベース | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: df347f9b-b950-4e3a-85f4-b9f21735eae3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2806522e0dcc0c9aa7badd099be28e11072b396e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111805"
---
# <a name="sample-database-for-in-memory-oltp"></a>インメモリ OLTP のサンプル データベース
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
## <a name="overview"></a>概要  
 このサンプルでは、インメモリ OLTP 機能を紹介します。 このサンプルで取り上げるのは、メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャです。また、インメモリ OLTP のパフォーマンス上の利点も示します。  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]のこのトピックを表示するには、「 [メモリ内 OLTP を実証する AdventureWorks の拡張](https://msdn.microsoft.com/library/dn511655\(v=sql.120\).aspx)」をご覧ください。  
  
 このサンプルは、AdventureWorks データベースの 5 つのテーブルをメモリ最適化テーブルに移行します。販売注文処理のデモ ワークロードも含まれています。 このデモ ワークロードを使用して、サーバーでインメモリ OLTP を使用するパフォーマンス上の利点を確認できます。  
  
 サンプルの説明では、テーブルをインメモリ OLTP に移行することによって生じるトレードオフについて触れ、メモリ最適化テーブルでは (まだ) サポートされていない機能について記載しています。  
  
 このサンプルのドキュメントは、次の内容で構成されています。  
  
-   サンプルをインストールしてデモ ワークロードを実行するための[前提条件](#Prerequisites)  
  
-   [AdventureWorksに基づくインメモリOLTPサンプルのインストール](#InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks)する手順  
  
-   [サンプル テーブルおよびプロシージャの説明](#Descriptionofthesampletablesandprocedures) - インメモリ OLTP サンプルによって AdventureWorks に追加されるテーブルおよびプロシージャの説明、オリジナルの AdventureWorks テーブルをメモリ最適化テーブルに移行する際の考慮事項が記載されています  
  
-   [デモ ワークロードを使用したパフォーマンス測定](#PerformanceMeasurementsusingtheDemoWorkload)を実行する手順 - デモ ワークロード自体を実行する手順だけでなく、ワークロードを操作するツール、ostress をインストールして実行する手順も記載されています  
  
-   [サンプルにおけるメモリおよびディスク領域の使用率](#MemoryandDiskSpaceUtilizationintheSample)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   運用環境と仕様が似ているサーバー (パフォーマンス テスト用)。 このサンプルでは、SQL Server に使用できるメモリが 16 GB 以上必要です。 インメモリ OLTP でのハードウェアに関する一般的なガイドラインは、ブログの投稿「[SQL Server 2014 におけるインメモリ OLTP のハードウェアに関する考慮事項](blog-hardware-in-memory-oltp.md)」を参照してください。

##  <a name="InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks"></a> AdventureWorksに基づくインメモリOLTPサンプルのインストール  
 サンプルをインストールするには、次の手順を実行します。  
  
1.  [https://www.microsoft.com/download/details.aspx?id=49502](https://www.microsoft.com/download/details.aspx?id=49502) にある AdventureWorks2016CTP3.bak と SQLServer2016CTP3Samples.zip をローカル フォルダー ('c:\temp' など) にダウンロードします。  
  
2.  [!INCLUDE[tsql](../../includes/tsql-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、データベース バックアップを復元します  
  
    1.  データ ファイルの対象フォルダーおよびファイル名を特定します。次に例を示します  
  
         'h:\DATA\AdventureWorks2016CTP3_Data.mdf'  
  
    2.  ログ ファイルの対象フォルダーおよびファイル名を特定します。次に例を示します  
  
         'i:\DATA\AdventureWorks2016CTP3_log.ldf'  
  
        1.  ログ ファイルは、データ ファイルとは異なるドライブに配置します。最大限のパフォーマンスを実現するために、SSD、PCIe ストレージなど、待機時間の少ないドライブに配置することをお勧めします。  
  
     T-SQL スクリプトの例:  
  
    ```  
    RESTORE DATABASE [AdventureWorks2016CTP3]   
      FROM DISK = N'C:\temp\AdventureWorks2016CTP3.bak'   
        WITH FILE = 1,    
      MOVE N'AdventureWorks2016_Data' TO N'h:\DATA\AdventureWorks2016CTP3_Data.mdf',    
      MOVE N'AdventureWorks2016_Log' TO N'i:\DATA\AdventureWorks2016CTP3_log.ldf',  
      MOVE N'AdventureWorks2016CTP3_mod' TO N'h:\data\AdventureWorks2016CTP3_mod'  
     GO  
    ```  
  
3.  サンプル スクリプトとワークロードを表示するには、ファイル SQLServer2016CTP3Samples.zip をローカル フォルダーにアンパックします。 ワークロードを実行する手順については、インメモリ OLTP\readme.txt ファイルをご参照ください。  
  
##  <a name="Descriptionofthesampletablesandprocedures"></a> サンプル テーブルおよびプロシージャの説明  
 サンプルでは、AdventureWorks の既存のテーブルに基づいて、製品および販売注文ごとに新しいテーブルを作成します。 新しいテーブルのスキーマは既存のテーブルと似ていますが、以下に示すように、異なる点がいくつかあります。  
  
 新しいメモリ最適化テーブルには、"_inmem" というサフィックスが付いています。 また、サンプルにはこれに対応するテーブルも含まれており、このテーブルには "_ondisk" というサフィックスが付いています。これらのテーブルを使用することで、システム上のメモリ最適化テーブルのパフォーマンスと、ディスク ベース テーブルのパフォーマンスを一対一で比較できます。  
  
 パフォーマンスを比較するためにワークロードで使用されるメモリ最適化テーブルには完全持続性が適用され、その動作は完全にログに記録されます。 パフォーマンス向上を実現するために、持続性や信頼性が犠牲になることはありません。  
  
 このサンプルの対象ワークロードは販売注文処理のワークロードです。また、製品および割引に関する情報も考慮します。 このため、使用するのは、SalesOrderHeader、SalesOrderDetail、Product、SpecialOffer、SpecialOfferProduct の 5 つのテーブルです。  
  
 2 つの新しいストアド プロシージャ、Sales.usp_InsertSalesOrder_inmem と Sales.usp_UpdateSalesOrderShipInfo_inmem は、販売注文を挿入し、指定された販売注文の出荷情報を更新するときに使用されます。  
  
 新しいスキーマ "Demo" には、デモ ワークロードを実行するためのヘルパー テーブルとストアド プロシージャが含まれます。  
  
 具体的には、インメモリ OLTP サンプルでは、次のオブジェクトが AdventureWorks に追加されます。  
  
### <a name="tables-added-by-the-sample"></a>サンプルによって追加されるテーブル  
  
#### <a name="the-new-tables"></a>新しいテーブル  
 Sales.SalesOrderHeader_inmem  
  
-   販売注文に関するヘッダー情報。 このテーブルでは、各販売注文が 1 つの行に対応します。  
  
 Sales.SalesOrderDetail_inmem  
  
-   販売注文の詳細。 このテーブルでは、販売注文の各品目が 1 つの行に対応します。  
  
 Sales.SpecialOffer_inmem  
  
-   特価品情報。各特価品に関連付けられた値引き率が含まれます。  
  
 Sales.SpecialOfferProduct_inmem  
  
-   特価品と製品の間の参照テーブル。 各特価品が、0 個以上の製品を特徴付けることができます。また、0 個以上の特価品で、各製品を特徴付けることもできます。  
  
 Production.Product_inmem  
  
-   製品に関する情報 (表示価格を含む)。  
  
 Demo.DemoSalesOrderDetailSeed  
  
-   サンプル販売注文を作成するためにデモ ワークロードで使用されます。  
  
 ディスク ベース テーブルのバリエーション:  
  
-   Sales.SalesOrderHeader_ondisk  
  
-   Sales.SalesOrderDetail_ondisk  
  
-   Sales.SpecialOffer_ondisk  
  
-   Sales.SpecialOfferProduct_ondisk  
  
-   Production.Product_ondisk  
  
#### <a name="differences-between-original-disk-based-and-the-and-new-memory-optimized-tables"></a>元のディスク ベース テーブルと新しいメモリ最適化テーブルの違い  
 このサンプルで提供されている新しいテーブルでは、その大部分で、元のテーブルと同じ列および同じデータ型が使用されています。 しかし、違う点もいくつかあります。 ここでは、その違いと、こうした変更の妥当性について説明します。  
  
 Sales.SalesOrderHeader_inmem  
  
-   *既定の制約* はメモリ最適化テーブルでサポートされ、そのほとんどがそのまま移行されています。 ただし、元の Sales.SalesOrderHeader テーブルには、現在の日付を取得する既定の制約が 2 つあります。OrderDate 列の制約と ModifiedDate 列の制約です。 コンカレンシーが多くスループットが高い注文処理ワークロードでは、グローバル リソースが競合ポイントになる可能性があります。 たとえば、このようなグローバル リソースにはシステム時刻があります。販売注文を挿入するインメモリ OLTP ワークロードを実行しているとき、特に、販売注文ヘッダーおよび販売注文の詳細に含まれる複数の列に対して、システム時刻を取得する必要がある場合は、このシステム時刻がボトルネックになることがわかっています。 このサンプルでは、挿入された販売注文ごとに 1 度だけシステム時刻を取得することで問題に対処します。そして、ストアド プロシージャ Sales.usp_InsertSalesOrder_inmem で、SalesOrderHeader_inmem と SalesOrderDetail_inmem にある datetime 列に対して、その値を使用します。  
  
-   *エイリアス UDT* - 元のテーブルでは、2 つのエイリアス ユーザー定義データ型 (UDT) が使用されます。1 つは dbo.OrderNumber で、これは PurchaseOrderNumber 列に対して使用されます。もう 1 つは dbo.AccountNumber で、AccountNumber 列に対して使用されます。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] では、メモリ最適化テーブルに対してエイリアス UDT がサポートされていません。したがって、新しいテーブルでは、システム データ型 nvarchar(25) と nvarchar(15) が個別に使用されます。  
  
-   *インデックス キーの NULL 値を許容する列* - 元のテーブルでは、SalesPersonID 列は NULL 値を許容しますが、新しいテーブルのこの列では NULL 値が許容されず、既定の制約として値 -1 が設定されています。 これは、メモリ最適化テーブルのインデックスでは、インデックス キーに NULL 値を許容する列を使用できないためです。この場合は、-1 が NULL のサロゲートです。  
  
-   *計算列* - [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] のメモリ最適化テーブルでは計算列がサポートされていないため、計算列である SalesOrderNumber および TotalDue は省略されます。 新しい Sales.vSalesOrderHeader_extended_inmem ビューには、SalesOrderNumber 列と TotalDue 列が反映されています。 したがって、これらの列が必要な場合は、このビューを使用します。  

    - **適用対象:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 以降、メモリ最適化テーブルとインデックスで計算列がサポートされています。

  
-   *外部キー制約* は、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]のメモリ最適化テーブルでサポートされます。しかし参照テーブルもメモリ最適化テーブルである場合に限ります。 メモリ最適化テーブルにも移行されるテーブルを参照する外部キーは、移行したテーブルに保持されますが、他の外部キーは省略されます。  また、SalesOrderHeader_inmem はサンプル ワークロードのホット テーブルであり、外部キー制約には、すべての DML 操作に対して追加の処理が必要です。これは、このテーブルには、この制約で参照される他のすべてのテーブル内の参照が必要だからです。 したがって、アプリによって Sales.SalesOrderHeader_inmem table に対する参照整合性が確保されているものと見なされ、行の挿入時には参照整合性は検証されません。  
  
-   *Rowguid* - rowguid 列は省略されます。 uniqueidentifier はメモリ最適化テーブルでサポートされますが、ROWGUIDCOL オプションは [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]ではサポートされません。 この種類の列は、通常、マージ レプリケーション、または filestream 列を持つテーブルで使用されます。 このサンプルには、どちらも含まれていません。  
  
 Sales.SalesOrderDetail  
  
-   "*既定の制約*" - SalesOrderHeader と同様、システムの日付/時刻を必要とする既定の制約は移行されません。現在のシステムの日付/時刻の挿入は、販売注文を挿入するストアド プロシージャによる初回挿入時に行われます。  
  
-   "*計算列*" - [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] のメモリ最適化テーブルでは計算列がサポートされていないため、計算列である LineTotal は計算列としては移行されませんでした。 この列にアクセスするには、Sales.vSalesOrderDetail_extended_inmem ビューを使用します。  
  
-   *Rowguid* - rowguid 列は省略されます。 詳細については、SalesOrderHeader テーブルの説明を参照してください。  
  
 Production.Product  
  
-   "*エイリアス UDT*" - 元のテーブルでは、ユーザー定義データ型 dbo.Flag が使用されます。これは、システム データ型 bit と同じです。 移行したテーブルでは、代わりに bit データ型が使用されます。  
  
-   *Rowguid* - rowguid 列は省略されます。 詳細については、SalesOrderHeader テーブルの説明を参照してください。  
  
 Sales.SpecialOffer  
  
-   *Rowguid* - rowguid 列は省略されます。 詳細については、SalesOrderHeader テーブルの説明を参照してください。  
  
 Sales.SpecialOfferProduct  
  
-   *Rowguid* - rowguid 列は省略されます。 詳細については、SalesOrderHeader テーブルの説明を参照してください。  
  
#### <a name="considerations-for-indexes-on-memory-optimized-tables"></a>メモリ最適化テーブルのインデックスに関する注意点  
 メモリ最適化テーブルのベースライン インデックスは、非クラスター化インデックスです。このインデックスでは、ポイント参照 (等値述語に対するインデックスのシーク)、範囲スキャン (非等値述語に対するインデックスのシーク)、フル インデックス スキャン、および並べ替えられたスキャンがサポートされます。 また、インデックス キーの先頭列での検索もサポートされます。 実際、メモリ最適化された非クラスター化インデックスでは、ディスク ベースの非クラスター化インデックスでサポートされる操作が、後方スキャンを除き、すべてサポートされています。 したがって、非クラスター化インデックスは、インデックスとしては安全な選択肢です。  
  
 ハッシュ インデックスを使用すると、ワークロードをさらに最適化できます。 これは、特にポイント参照と行挿入に合わせて最適化されています。 ただし、範囲スキャン、並べ替えられたスキャン、または先頭のインデックス キー列での検索がサポートされていないことを考慮する必要があります。 したがって、このインデックスを使用するときは注意が必要です。 また、作成時に bucket_count を指定する必要もあります。 一般的にはインデックス キー値の数の 1 ～ 2 倍に設定しますが、多めに設定しても通常は問題ありません。  
  
 詳細については、オンライン ブックの [インデックスのガイドライン](https://technet.microsoft.com/library/dn133166\(v=sql.120\).aspx) 、および [適切な bucket_count の選択](https://technet.microsoft.com/library/dn494956\(v=sql.120\).aspx)に関するガイドラインをご覧ください。  
  
 移行したテーブルのインデックスは、販売注文処理のデモ ワークロードに合わせて調整されています。 ワークロードは、Sales.SalesOrderHeader_inmem テーブルおよび Sales.SalesOrderDetail_inmem テーブルの挿入とポイント参照のほか、Production.Product_inmem テーブルおよび Sales.SpecialOffer_inmem テーブルの主キー列のポイント参照にも依存します。  
  
 Sales.SalesOrderHeader_inmem には 3 つのインデックスがあります。このインデックスは、パフォーマンス上の理由から、また、並べ替えられたスキャンと範囲スキャンがワークロードに不要であることから、すべてハッシュ インデックスです。  
  
-   (SalesOrderID) のハッシュ インデックス: 予測される販売注文数は 1,000 万であるため、bucket_count は 1,000 万です (1,600 万まで切り上げ)  
  
-   (SalesPersonID) のハッシュ インデックス: bucket_count は 100 万です。 提供されたデータ セットに含まれる販売員は多くありませんが、これにより将来の成長に対応できます。さらに、bucket_count のサイズが超過しても、ポイント参照のパフォーマンスが低下することはありません。  
  
-   (CustomerID) のハッシュ インデックス: bucket_count は 100 万です。 提供されたデータ セットに含まれる顧客は多くありませんが、これにより将来の成長に対応できます。  
  
 Sales.SalesOrderDetail_inmem には 3 つのインデックスがあります。このインデックスは、パフォーマンス上の理由から、また、並べ替えられたスキャンと範囲スキャンがワークロードに不要であることから、すべてハッシュ インデックスです。  
  
-   (SalesOrderID、SalesOrderDetailID) のハッシュ インデックス: これは主キー インデックスです。(SalesOrderID、SalesOrderDetailID) での参照頻度が低くなりますが、このキーのハッシュ インデックスを使用すると行挿入の速度が上がります。 bucket_count は 5,000 万です (6,700 万まで切り上げ)。つまり、予測される販売注文数は 1,000 万で、各注文の平均品目数が 5 品目になるように調整されます  
  
-   (SalesOrderID) のハッシュ インデックス: 販売注文による参照が頻繁に行われます。1 つの注文に対応するすべての品目を検索する必要があります。  予測される販売注文数は 1,000 万であるため、bucket_count は 1,000 万です (1,600 万まで切り上げ)  
  
-   (ProductID) のハッシュ インデックス: bucket_count は 100 万です。 提供されたデータ セットに含まれる製品は多くありませんが、これにより将来の成長に対応できます。  
  
 Production.Product_inmem には 3 つのインデックスがあります  
  
-   (ProductID) のハッシュ インデックス: ProductID での参照はデモ ワークロードのクリティカル パスに含まれるため、これはハッシュ インデックスです  
  
-   (Name) の非クラスター化インデックス: これにより、製品名に対して、並べ替えられたスキャンを実行できます  
  
-   (ProductNumber) の非クラスター化インデックス: これにより、製品番号に対して、並べ替えられたスキャンを実行できます  
  
 Sales.SpecialOffer_inmem の (SpecialOfferID) には、ハッシュ インデックスが 1 つあります。特価品のポイント参照は、デモ ワークロードでは重要です。 bucket_count は 100 万です。これにより、将来の成長に対応できます。  
  
 Sales.SpecialOfferProduct_inmem は、デモ ワークロードでは参照されません。したがって、このテーブルでは、ハッシュ インデックスを使用してワークロードを最適化する必要はありません。(SpecialOfferID、ProductID) および (ProductID) のインデックスは非クラスター化インデックスです。  
  
 上記で挙げた bucket_count の中にはサイズ超過しているものがありますが、SalesOrderHeader_inmem と SalesOrderDetail_inmem のインデックスの bucket_count は違います。つまり、これらの bucket_count のサイズは、1,000 万個の販売注文を対象にしています。 その目的は、使用できるメモリ容量が少ないシステムにサンプルをインストールできるようにすることですが、この場合、メモリ不足になるとデモ ワークロードは失敗します。 1,000 万を超える販売注文を適切に処理する必要がある場合は、必要に応じてバケット数を増やすことができます。  
  
#### <a name="considerations-for-memory-utilization"></a>メモリ使用率に関する注意点  
 デモ ワークロードの実行前および実行後のサンプル データベースのメモリ使用について、セクション「 [メモリ最適化テーブルのメモリ使用率](#Memoryutilizationforthememory-optimizedtables)」で説明しています。  
  
### <a name="stored-procedures-added-by-the-sample"></a>サンプルによって追加されたストアド プロシージャ  
 販売注文を挿入するストアド プロシージャと、出荷情報の詳細を更新するストアド プロシージャの 2 つの主要ストアド プロシージャを次に示します。  
  
-   Sales.usp_InsertSalesOrder_inmem  
  
    -   新しい販売注文をデータベースに挿入し、その販売注文の SalesOrderID を出力します。 入力パラメーターとして、販売注文ヘッダーの詳細と注文の品目を取得します。  
  
    -   出力パラメーター:  
  
        -   @SalesOrderID int - 挿入された販売注文の SalesOrderID  
  
    -   入力パラメーター (必須):  
  
        -   @DueDate datetime2  
  
        -   @CustomerID int  
  
        -   @BillToAddressID [int]  
  
        -   @ShipToAddressID [int]  
  
        -   @ShipMethodID [int]  
  
        -   @SalesOrderDetails Sales.SalesOrderDetailType_inmem - 注文の品目が含まれる TVP  
  
    -   入力パラメーター (省略可能):  
  
        -   @Status [tinyint]  
  
        -   @OnlineOrderFlag [bit]  
  
        -   @PurchaseOrderNumber [nvarchar](25\)  
  
        -   @AccountNumber [nvarchar](15\)  
  
        -   @SalesPersonID [int]  
  
        -   @TerritoryID [int]  
  
        -   @CreditCardID [int]  
  
        -   @CreditCardApprovalCode [varchar](15\)  
  
        -   @CurrencyRateID [int]  
  
        -   @Comment nvarchar(128)  
  
-   Sales.usp_UpdateSalesOrderShipInfo_inmem  
  
    -   指定された販売注文の出荷情報を更新します。 これにより、販売注文のすべての品目の出荷情報も更新されます。  
  
    -   これはネイティブ コンパイル ストアド プロシージャ Sales.usp_UpdateSalesOrderShipInfo_native のラッパー プロシージャで、再試行ロジックを備えており、同じ注文を更新する同時実行トランザクションとの間で発生する可能性のある (予期しない) 競合を処理します。 再試行ロジックの詳細については、オンライン ブックの [こちら](https://technet.microsoft.com/library/dn169141\(v=sql.120\).aspx)のトピックを参照してください。  
  
-   Sales.usp_UpdateSalesOrderShipInfo_native  
  
    -   これは、出荷情報に対する更新を実際に処理するネイティブ コンパイル ストアド プロシージャで、 ラッパー ストアド プロシージャ Sales.usp_UpdateSalesOrderShipInfo_inmem から呼び出される手段です。 クライアントがエラーに対処できる場合、再試行ロジックを実装すると、ラッパー ストアド プロシージャを使用せずに、このプロシージャを直接呼び出すことができます。  
  
 次のストアド プロシージャは、デモ ワークロードに対して使用します。  
  
-   Demo.usp_DemoReset  
  
    -   SalesOrderHeader テーブルおよび SalesOrderDetail テーブルを空にして、再作成することで、デモをリセットします。  
  
 次のストアド プロシージャは、ドメインと参照整合性を確保しながら、メモリ最適化テーブルへの挿入や、テーブルからの削除を行うときに使用します。  
  
-   Production.usp_InsertProduct_inmem  
  
-   Production.usp_DeleteProduct_inmem  
  
-   Sales.usp_InsertSpecialOffer_inmem  
  
-   Sales.usp_DeleteSpecialOffer_inmem  
  
-   Sales.usp_InsertSpecialOfferProduct_inmem  
  
 最後に、ドメインと参照整合性を確認するときに使用するストアド プロシージャを次に示します。  
  
1.  dbo.usp_ValidateIntegrity  
  
    -   省略可能なパラメーター: @object_id - 整合性を検証するオブジェクトの ID  
  
    -   このプロシージャは、検証する必要がある整合性規則に関して、dbo.DomainIntegrity テーブル、dbo.ReferentialIntegrity テーブル、および dbo.UniqueIntegrity テーブルに依存しています。サンプルでは、AdventureWorks データベースの元のテーブルに対して存在する CHECK 制約、外部キー制約、および UNIQUE 制約に基づいて、これらのテーブルにデータが入力されます。  
  
    -   これはヘルパー プロシージャ dbo.usp_GenerateCKCheck、dbo.usp_GenerateFKCheck、および dbo.GenerateUQCheck を使用して、整合性チェックの実行に必要な T-SQL を生成します。  
  
##  <a name="PerformanceMeasurementsusingtheDemoWorkload"></a> デモ ワークロードを使用したパフォーマンス測定  
 ostress は、Microsoft CSS SQL Server サポート チームによって開発されたコマンド ライン ツールです。 このツールを使用すると、クエリやストアド プロシージャを並列実行できます。 指定された T-SQL ステートメントが並列実行されるようにスレッドの数を構成できるほか、そのスレッドでステートメントを実行する回数を指定できます。ostress はスレッドをスピン アップし、すべてのスレッド内のステートメントを並列実行します。 すべてのスレッドに対する実行が完了したら、その実行が完了するまでの所要時間を報告します。  
  
### <a name="installing-ostress"></a>ostress のインストール  
 ostress は、RML ユーティリティの一部としてインストールされます。ostress のスタンドアロン インストールはありません。  
  
 インストール手順:  
  
1.  以下のページから RML ユーティリティの x64 インストール パッケージをダウンロードして実行します。[SQL Server 用の Report Markup Language (RML) をダウンロードする](https://www.microsoft.com/en-us/download/details.aspx?id=4511)

2.  特定のファイルが使用中であることを通知するダイアログ ボックスが表示された場合は、[続行] をクリックします  
  
### <a name="running-ostress"></a>ostress の実行  
 ostress は、コマンド ライン プロンプトから実行されます。 最も便利なのは、RML ユーティリティの一部としてインストールされている "RML Cmd Prompt" から実行する方法です。  
  
 RML Cmd Prompt を開くには、次の手順に従います。  
  
 Windows Server 2012 [R2] および Windows 8/8.1 で、Windows キーをクリックして [スタート] メニューを開き、「rml」と入力します。 検索結果の一覧に表示される [RML Cmd Prompt] をクリックします。  
  
 コマンド プロンプトが、RML ユーティリティのインストール フォルダーにあることを確認します。  
  
 コマンド ライン オプションを指定せずに ostress.exe を実行すると、ostress のコマンド ライン オプションを確認できます。 このサンプルで ostress を実行するときに使用できる主なオプションを次に示します。  
  
-   -S 接続する Microsoft SQL Server インスタンスの名前  
  
-   -E Windows 認証を使用して接続 (既定)。SQL Server 認証を使用する場合は、オプションとして -U および -P を使用して、ユーザー名とパスワードをそれぞれ指定  
  
-   -d データベースの名前。この例では AdventureWorks2014  
  
-   -Q 実行される T-SQL ステートメント  
  
-   -n 各入力ファイル/クエリを処理する接続の数  
  
-   -r 各入力ファイル/クエリを実行するために接続ごとに繰り返される数  
  
### <a name="demo-workload"></a>デモ ワークロード  
 デモ ワークロードで使用する主なストアド プロシージャは Sales.usp_InsertSalesOrder_inmem/ondisk です。 以下のスクリプトでは、サンプル データを使用してテーブル値パラメーター (TVP) を生成し、5 つの品目が含まれる販売注文を挿入するプロシージャを呼び出します。  
  
 ostress ツールは、ストアド プロシージャ呼び出しを並列実行し、販売注文を同時に挿入するクライアントをシミュレートする際に使用します。  
  
 負荷をかけた Demo.usp_DemoReset の実行が完了するたびに、デモをリセットしてください。 このプロシージャにより、メモリ最適化テーブルの行とディスク ベース テーブルが削除され、データベース チェックポイントが実行されます。  
  
 次のスクリプトは同時に実行され、販売注文処理のワークロードをシミュレートします。  
  
```  
DECLARE   
      @i int = 0,   
      @od Sales.SalesOrderDetailType_inmem,   
      @SalesOrderID int,   
      @DueDate datetime2 = sysdatetime(),   
      @CustomerID int = rand() * 8000,   
      @BillToAddressID int = rand() * 10000,   
      @ShipToAddressID int = rand() * 10000,   
      @ShipMethodID int = (rand() * 5) + 1;   
  
INSERT INTO @od   
SELECT OrderQty, ProductID, SpecialOfferID   
FROM Demo.DemoSalesOrderDetailSeed   
WHERE OrderID= cast((rand()*106) + 1 as int);   
  
WHILE (@i < 20)   
BEGIN;   
      EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od;   
      SET @i += 1   
END  
  
```  
  
 このスクリプトでは、作成された各サンプル注文が、WHILE ループで実行された 20 個のストアド プロシージャによって 20 回挿入されます。 ループを使うことで、サンプル注文がデータベースを使用して作成されるという事実を説明します。 一般的な運用環境では、中間層アプリケーションが、挿入する販売注文を作成します。  
  
 前のスクリプトでは、メモリ最適化テーブルに販売注文が挿入されます。 ディスク ベース テーブルに販売注文を挿入するスクリプトを取得するには、2 つある "_inmem" を "_ondisk" に置き換えます。  
  
 ostress ツールを使って、複数のコンカレント接続を使用してスクリプトを実行します。 "-n" パラメーターで接続数を制御し、"r" パラメーターで各接続のスクリプト実行回数を制御します。  
  
#### <a name="running-the-workload"></a>ワークロードの実行  
 拡張性をテストするために、100 個の接続を使用して、1,000 万個の販売注文を挿入します。 このテストは、適度なサーバー (たとえば、8 個の物理コアと 16 個の論理コア) と、ログ用の基本 SSD ストレージで問題なく実行されます。 ご利用のハードウェアでテストを正常に実行できない場合は、「[実行速度の遅いテストのトラブルシューティング](#Troubleshootingslow-runningtests)」セクションをご覧ください。このテストのストレス レベルを下げるには、"-n" パラメーターを変更して接続数を減らします。 たとえば、接続数を 40 に下げるには、"-n100" パラメーターを "-n40" に変更します。  
  
 ワークロードのパフォーマンス評価基準として、ワークロードの実行後に ostress.exe によって報告された経過時間を使用します。  
  
 以下の手順と測定では、1,000 万個の販売注文を挿入するワークロードを使用します。 販売注文を 100 万個に縮小して挿入するワークロードを実行する手順については、SQLServer2016CTP3Samples.zip アーカイブに含まれる 'In-Memory OLTP\readme.txt' 内の手順をご覧ください。  
  
##### <a name="memory-optimized-tables"></a>メモリ最適化テーブル  
 まず、メモリ最適化テーブルでワークロードを実行します。 次のコマンドは、100 個のスレッドを開きます。このスレッドそれぞれが、5,000 個の繰り返しに対して実行されており、  各繰り返しによって、20 個の販売注文が個別のトランザクションに挿入されます。 1 つの繰り返しにつき 20 個の挿入があり、挿入するデータがデータベースを使用して生成されるという事実を補います。 この結果、販売注文の挿入の合計は 20 \* 5,000 \* 100 = 10,000,000" 個になります。  
  
 RML Cmd Prompt を開いて、次のコマンドを実行します。  
  
 [コピー] をクリックしてコマンドをコピーし、RML ユーティリティのコマンド プロンプトに貼り付けてください。  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2016CTP3 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 合計 8 個の物理 (16 個の論理) コアを備えたテスト サーバーでの所要時間は 2 分 5 秒でした。 合計 24 個の物理 (48 個の論理) コアを備えた 2 台目のテスト サーバーでの所要時間は 1 分 0 秒でした。  
  
 ワークロードの実行中、タスク マネージャーなどを使用して、CPU の使用率を確認します。 CPU 使用率が 100% に近いことがわかります。 そうでない場合は、ログ IO がボトルネックになっています。「 [実行速度の遅いテストのトラブルシューティング](#Troubleshootingslow-runningtests)」も参照してください。  
  
##### <a name="disk-based-tables"></a>ディスク ベース テーブル  
 次のコマンドは、ディスク ベース テーブルでワークロードを実行します。 このワークロードの実行には時間がかかる場合があり、その主な原因はシステム内のラッチ競合です。 メモリ最適化テーブルはラッチ フリーであるため、この問題は発生しません。  
  
 RML Cmd Prompt を開いて、次のコマンドを実行します。  
  
 [コピー] をクリックしてコマンドをコピーし、RML ユーティリティのコマンド プロンプトに貼り付けてください。  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2016CTP3 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 合計 8 個の物理 (16 個の論理) コアを備えたテスト サーバーでの所要時間は 41 分 25 秒でした。 合計 24 個の物理 (48 個の論理) コアを備えた 2 台目のテスト サーバーでの所要時間は 52 分 16 秒でした。  
  
 ディスク ベース テーブルを使用していると、SQL Server では CPU をフルに活用できません。これが主な要因となり、このテストでは、メモリ最適化テーブルとディスク ベース テーブルのパフォーマンスに差が生じました。 CPU をフル活用できない原因はラッチ競合です。同時実行トランザクションは同じデータ ページに書き込もうとしますが、ラッチにより、一度に 1 つのトランザクションしかページに書き込むことができなくなります。 インメモリ OLTP エンジンはラッチ フリーで、データ行はページ単位で整理されていません。 このため、同時実行トランザクションが挿入をブロックし合うことはなく、SQL Server は CPU をフル活用できます。  
  
 ワークロードの実行中、タスク マネージャーなどを使用して、CPU の使用率を確認できます。 ディスク ベース テーブルの CPU 使用率が、100% からはかけ離れていることがわかります。 16 個の論理プロセッサを備えたテスト構成では、使用率は 24% 前後で推移します。  
  
 必要に応じて、パフォーマンス モニターを使用して、パフォーマンス カウンター "\SQL Server:Latches\Latch Waits/sec" で 1 秒あたりのラッチ待機数を表示できます。  
  
#### <a name="resetting-the-demo"></a>デモのリセット  
 デモをリセットするには、RML Cmd Prompt を開いて、次のコマンドを実行します。  
  
```  
ostress.exe -S. -E -dAdventureWorks2016CTP3 -Q"EXEC Demo.usp_DemoReset"  
```  
  
 ハードウェアによっては、この実行に数分かかることがあります。  
  
 デモの実行が完了するたびに、リセットすることをお勧めします。 このワークロードは挿入のみであるため、実行のたびに多くのメモリを消費します。このため、メモリ不足が発生しないようにリセットが必要です。 実行後に消費されるメモリ量について、セクション「 [ワークロード実行後のメモリ使用率](#Memoryutilizationafterrunningtheworkload)」で説明しています。  
  
###  <a name="Troubleshootingslow-runningtests"></a> 実行速度の遅いテストのトラブルシューティング  
 テスト結果は、通常、ハードウェアと、テスト実行で使用されたコンカレンシーのレベルによって変わります。 期待した結果を得られない場合に確認することをいくつか次に示します。  
  
-   同時実行トランザクション数:1 つのスレッドでワークロードを実行すると、インメモリ OLTP によるパフォーマンス向上が 2 倍に満たない場合があります。 高レベルのコンカレンシーがある場合、唯一大きな問題になるのがラッチ競合です。  
  
-   SQL Server で使用できるコアが少ない: つまり、低レベルの同時実行がシステムに存在することになります。これは、SQL で使用できるコアの数しか、トランザクションを同時実行できないからです。  
  
    -   現象: ディスク ベース テーブルでワークロードを実行しているときに CPU 使用率が高い場合、競合の数はそれほど多くありません。これは、コンカレンシーが不足していることを示します。  
  
-   ログ ドライブの速度:ログ ドライブが、システム内のトランザクション スループット レベルに対応できない場合、ワークロードはログ IO でボトルネックになります。 インメモリ OLTP でのログ記録は効率的ですが、ログ IO がボトルネックになっていると、パフォーマンス向上の可能性は限られます。  
  
    -   現象: メモリ最適化テーブルでワークロードを実行しているとき、CPU 使用率が 100% からかけ離れている場合、または、その変動が激しい場合は、ログ IO ボトルネックが存在する可能性があります。 これを確認するには、リソース モニターを開き、ログ ドライブのキュー長を確認します。  
  
##  <a name="MemoryandDiskSpaceUtilizationintheSample"></a> サンプルにおけるメモリおよびディスク領域の使用率  
 ここでは、サンプル データベースのメモリおよびディスク領域の使用率に関して期待すべき事項について説明します。 また、16 個の論理コアを備えたテスト サーバーでの結果も示します。  
  
###  <a name="Memoryutilizationforthememory-optimizedtables"></a> メモリ最適化テーブルのメモリ使用率  
  
#### <a name="overall-utilization-of-the-database"></a>データベースの全体的な使用率  
 次のクエリを使用すると、システムのインメモリ OLTP の合計メモリ使用率を取得できます。  
  
```  
SELECT type  
   , name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
 データベースが作成された後のスナップショット:  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|既定|94|  
|MEMORYCLERK_XTP|DB_ID_5|877|  
|MEMORYCLERK_XTP|既定|0|  
|MEMORYCLERK_XTP|既定|0|  
  
 既定のメモリ クラークは比較的小さく、システム全体のメモリ構造が含まれています。 ユーザー データベースのメモリ クラーク (この場合は ID 5 のデータベース) は約 900 MB です。  
  
#### <a name="memory-utilization-per-table"></a>テーブルごとのメモリ使用率  
 次のクエリを使用すると、個別のテーブルとそのインデックスのメモリ使用率にドリル ダウンできます。  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
 サンプルの新しいインストールに対するこのクエリの結果を次に示します。  
  
||||  
|-|-|-|  
|**テーブル名**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SpecialOfferProduct_inmem|64|3840|  
|DemoSalesOrderHeaderSeed|1984|5504|  
|SalesOrderDetail_inmem|15316|663552|  
|DemoSalesOrderDetailSeed|64|10432|  
|SpecialOffer_inmem|3|8192|  
|SalesOrderHeader_inmem|7168|147456|  
|Product_inmem|124|12352|  
  
 テーブルがかなり小さいことがわかります。SalesOrderHeader_inmem は約 7 MB、SalesOrderDetail_inmem は約 15 MB です。  
  
 ここで印象的なのは、インデックスに割り当てられているメモリのサイズです (テーブル データのサイズと比較)。 このサイズになるのは、サンプルのハッシュ インデックスが、大きなデータ サイズに合わせて事前にサイズ調整されているためです。 ハッシュ インデックスのサイズは固定されているため、テーブルのデータのサイズに合わせて大きくなることはありません。  
  
####  <a name="Memoryutilizationafterrunningtheworkload"></a> ワークロード実行後のメモリ使用率  
 1,000 万個の販売注文を挿入した後の全体的なメモリ使用率は次のようになります。  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|既定|146|  
|MEMORYCLERK_XTP|DB_ID_5|7374|  
|MEMORYCLERK_XTP|既定|0|  
|MEMORYCLERK_XTP|既定|0|  
  
 このように、SQL Server がサンプル データベースのメモリ最適化テーブルおよびインデックスに対して使用しているビットは 8 GB を下回ります。  
  
 サンプルを 1 回実行した後のテーブルごとの詳細なメモリ使用量を確認します。  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
||||  
|-|-|-|  
|**テーブル名**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SalesOrderDetail_inmem|5113761|663552|  
|DemoSalesOrderDetailSeed|64|10368|  
|SpecialOffer_inmem|2|8192|  
|SalesOrderHeader_inmem|1575679|147456|  
|Product_inmem|111|12032|  
|SpecialOfferProduct_inmem|64|3712|  
|DemoSalesOrderHeaderSeed|1984|5504|  
  
 データの合計サイズが約 6.5 GB であることがわかります。 SalesOrderHeader_inmem テーブルと SalesOrderDetail_inmem テーブルのインデックスのサイズが、販売注文を挿入する前のインデックスのサイズと同じであることに注意してください。 インデックスのサイズが変わらなかったのは、この両方のテーブルがハッシュ インデックスを使用しているからです。ハッシュ インデックスは静的です。  
  
#### <a name="after-demo-reset"></a>デモのリセット後  
 ストアド プロシージャ Demo.usp_DemoReset を使用すると、デモをリセットできます。 これにより SalesOrderHeader_inmem テーブルと SalesOrderDetail_inmem テーブルのデータが削除され、元の SalesOrderHeader テーブルと SalesOrderDetail テーブルからデータが再送信されます。  
  
 この時点でテーブルの行は削除されていますが、メモリはすぐに再利用されるわけではありません。 SQL Server では、メモリはメモリ最適化テーブルの削除された行から、必要に応じてバックグラウンドで再利用されます。 デモのリセット後すぐにこれがわかります。システムにトランザクション ワークロードがない場合、削除された行のメモリはまだ再利用されていません。  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|既定|2261|  
|MEMORYCLERK_XTP|DB_ID_5|7396|  
|MEMORYCLERK_XTP|既定|0|  
|MEMORYCLERK_XTP|既定|0|  
  
 これは想定されている動作です。メモリはトランザクション ワークロードの実行中に再利用されます。  
  
 2 回目のデモ ワークロードの実行を開始すると、前に削除された行がクリーンアップされるため、メモリ使用率は最初は減少します。 ある時点で、メモリ サイズは再び増加し、ワークロードが終了するまで増加し続けます。 デモをリセットしてから 1,000 万行を挿入した後のメモリ使用率は、最初の実行後の使用率とよく似ています。 例 :  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|既定|1863|  
|MEMORYCLERK_XTP|DB_ID_5|7390|  
|MEMORYCLERK_XTP|既定|0|  
|MEMORYCLERK_XTP|既定|0|  
  
### <a name="disk-utilization-for-memory-optimized-tables"></a>メモリ最適化テーブルのディスク使用率  
 特定の時点におけるデータベースのチェックポイント ファイルに対する、全体的なディスク上のサイズを確認するには、次のクエリを使用します。  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
  
```  
  
#### <a name="initial-state"></a>初期状態  
 サンプル ファイル グループとサンプル メモリ最適化テーブルの初回作成時に、チェックポイント ファイルがいくつか事前作成され、システムによってデータが入力されます。事前作成されるチェックポイント ファイルの数は、システム内の論理プロセッサの数によって異なります。 最初はサンプルがかなり小さいため、初回作成後の事前作成されたファイルはほとんど空です。  
  
 16 個の論理プロセッサを持つコンピューター上のサンプルに対する、最初のディスク上のサイズを次に示します。  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**On-disk size in MB**|  
|2312|  
  
 チェックポイント ファイルのディスク上のサイズ (2.3 GB) と実際のデータ サイズ (約 30 MB) に大きな違いがあることがわかります。  
  
 ディスク領域の使用率の詳細を確認するには、次のクエリを使用します。 このクエリから返されるディスクのサイズは、5 (REQUIRED FOR BACKUP/HA)、6 (IN TRANSITION TO TOMBSTONE)、または 7 (TOMBSTONE) の状態のファイルに関するおおよそのサイズです。  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
 サンプルの初期状態については、このクエリ結果は、16 個の論理プロセッサを持つサーバーに対する結果と似ています。  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|@shouldalert|128|  
|UNDER CONSTRUCTION|DELTA|@shouldalert|8|  
  
 領域のほとんどが、事前作成されたデータとデルタ ファイルによって使用されていることがわかります。 SQL Server では、1 組のファイル ペア (データとデルタ) が論理プロセッサごとに事前作成されます。 また、さらに効率よくデータを挿入できるように、データ ファイルは 128 MB に、デルタ ファイルは 8 MB に事前にサイズ調整されています。  
  
 メモリ最適化テーブルの実際のデータは、1 つのデータ ファイルにあります。  
  
#### <a name="after-running-the-workload"></a>ワークロードの実行後  
 1,000 万個の販売注文を挿入するテストを 1 回実行すると、全体的なディスク上のサイズは次のようになります (16 コア テスト サーバーの場合)。  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**On-disk size in MB**|  
|8828|  
  
 ディスク上のサイズは 9 GB に迫っています。これは、データのインメモリ サイズに近い数値です。  
  
 さまざまな状態のチェックポイント ファイルのサイズを詳しく確認します。  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|@shouldalert|128|  
|UNDER CONSTRUCTION|DELTA|@shouldalert|8|  
  
 事前作成された 16 組のファイル ペアはまだあり、チェックポイントが閉じているので、準備状態です。  
  
 1 組の作成中のファイル ペアは、現在のチェックポイントが閉じるまで使用されます。 これにより、アクティブなチェックポイント ファイルと共に、約 6.5 GB のディスク使用率が 6.5 GB のメモリ内のデータに対して提供されます。 インデックスはディスクに保存されないため、この場合、全体的なディスクのサイズはメモリのサイズよりも小さくなることに注意してください。  
  
#### <a name="after-demo-reset"></a>デモのリセット後  
 システムにトランザクション ワークロードがなく、また、データベース チェックポイントもない場合は、デモをリセットしても、ディスク領域はすぐには再利用されません。 チェックポイント ファイルがさまざまな段階を経て最終的に破棄されるようにするには、複数のチェックポイントとログの切り捨てイベントが発生する必要があり、これによりチェックポイント ファイルのマージとガベージ コレクションが開始されます。 システムにトランザクション ワークロードがある場合 (また、完全復旧モデルの使用時に、定期的なログ バックアップを取得する場合)、システムがアイドル状態でなければ、デモ シナリオで示すように、これらは自動的に発生します。  
  
 この例では、デモのリセット後、次のように表示される場合があります  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**On-disk size in MB**|  
|11839|  
  
 ディスク サイズは 12 GB 近くあり、デモをリセットする前の 9 GB を大幅に上回っています。 これは、一部のチェックポイント ファイルのマージが開始されたにもかかわらず、まだインストールされていないマージ ターゲットがあるためです。また、クリーン アップされていないマージ ソース ファイルの存在も原因となっています。これを次に示します。  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|ACTIVE|DATA|38|5152|  
|ACTIVE|DELTA|38|1331|  
|MERGE TARGET|DATA|7|896|  
|MERGE TARGET|DELTA|7|56|  
|MERGED SOURCE|DATA|13|1772|  
|MERGED SOURCE|DELTA|13|455|  
  
 トランザクション アクティビティがシステムで発生すると、マージ ターゲットがインストールされ、マージされたソースがクリーン アップされます。  
  
 2 回目のデモ ワークロードを実行してからデモをリセットし、1,000 万個の販売注文を挿入すると、最初のワークロードの実行中に作成されたファイルはクリーンアップされています。 ワークロードの実行中に前のクエリを複数回実行した場合、チェックポイント ファイルはさまざまな段階を経て進行します。  
  
 2 回目のワークロードを実行してから 1,000 万個の販売注文を挿入した場合、そのディスク使用率は最初の実行後の使用率とよく似ています。ただし、システムはもともと動的であるため、必ずしも同じであるとは限りません。 例 :  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|2|268|  
|UNDER CONSTRUCTION|DELTA|2|16|  
|ACTIVE|DATA|41|5608|  
|ACTIVE|DELTA|41|328|  
  
 この場合、"under construction" 状態のチェックポイント ファイルのペアが 2 組あります。これは、複数のファイル ペアが、おそらくワークロードにおける高レベルのコンカレンシーが原因で、"under construction" 状態に移行されたことを意味します。 一方、複数の同時実行スレッドには新しいファイル ペアが必要だったため、ペアの状態が "precreated" から "under construction" に移行されました。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

