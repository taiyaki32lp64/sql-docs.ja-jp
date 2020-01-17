---
title: 実稼動サーバーのチューニング負荷の軽減 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: bb95ecaf-444a-4771-a625-e0a91c8f0709
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f05ede948892b7f9ae6a9f9ee24a3b6878586917
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113384"
---
# <a name="reduce-the-production-server-tuning-load"></a>実稼動サーバーのチューニング負荷の軽減
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーは、ワークロードの分析とチューニング推奨設定の生成をクエリ オプティマイザーに依存します。 実稼働サーバー上でこの分析を実行すると、サーバーの負荷が増し、チューニング セッション中のサーバーのパフォーマンスが低下することがあります。 実稼働サーバーに加えてテスト サーバーを使用することで、チューニング セッション中のサーバーの負荷への影響を小さくすることができます。  
  
## <a name="how-database-engine-tuning-advisor-uses-a-test-server"></a>データベース エンジン チューニング アドバイザーでテスト サーバーを使用する方法  
 これまでは、テスト サーバーを使用するために、実稼働サーバーからテスト サーバーにすべてのデータをコピーし、テスト サーバーをチューニングして、実稼働サーバーに推奨設定を実装する方法を使用してきました。 この処理により、実稼働サーバーのパフォーマンスに影響が及ぶことはありませんが、これは最善の解決策ではありません。 たとえば、大量のデータを実稼働サーバーからテスト サーバーにコピーする場合、非常に時間がかかり、多量のリソースが使用される可能性があります。 また、テスト サーバーのハードウェアが、実稼働サーバーに配置されているハードウェアほど優れていることはめったにありません。 チューニング処理は、クエリ オプティマイザーに依存し、生成される推奨設定は基になるハードウェアに部分的に基づきます。 テスト サーバーと実稼働サーバーのハードウェアが異なる場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの推奨設定の特性が低下します。  
  
 このような問題を防ぐために、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、大部分のチューニング負荷をテスト サーバーにオフロードして、実稼働サーバー上のデータベースをチューニングします。 このチューニングは、実際には実稼働サーバーからテスト サーバーにデータがコピーされずに、実稼働サーバーのハードウェア構成情報を使用して行われます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、実稼働サーバーからテスト サーバーに実際のデータがコピーされることはありません。 メタデータと必要な統計だけがコピーされます。  
  
 次の手順は、テスト サーバーでの実稼働データベースのチューニング処理の概要を示しています。  
  
1.  テスト サーバーを使用するユーザーが、両方のサーバーに存在することを確認します。  
  
     開始する前に、テスト サーバーを使用して実稼働サーバー上のデータベースをチューニングするユーザーが、両方のサーバーに存在することを確認します。 このためには、テスト サーバーにユーザーとそのユーザーのログインを作成する必要があります。 使用者が両方のコンピューターの **sysadmin** 固定サーバー ロールのメンバーであれば、この手順は不要です。  
  
2.  テスト サーバーでワークロードをチューニングします。  
  
     テスト サーバーでワークロードをチューニングするには、XML 入力ファイルと **dta** コマンド ライン ユーティリティを併用する必要があります。 XML 入力ファイルで、 **TestServer** サブ要素にテスト サーバーの名前を指定し、 **TuningOptions** 親要素の下の他のサブ要素の値も指定します。  
  
     チューニング処理中、データベース エンジン チューニング アドバイザーによって、テスト サーバーにシェル データベースが作成されます。 データベース エンジン チューニング アドバイザーでは、このシェル データベースを作成してチューニングするために、次の目的で実稼働サーバーに呼び出しが行われます。  
  
    1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーは、実稼働データベースからテスト サーバーのシェル データベースにメタデータをインポートします。 このメタデータには、空のテーブル、インデックス、ビュー、ストアド プロシージャ、トリガーなどが含まれます。 これにより、テスト サーバーのシェル データベースに対してワークロード クエリを実行できるようになります。  
  
    2.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーは、クエリ オプティマイザーでテスト サーバーのクエリを正確に最適化できるように、実稼働サーバーから統計をインポートします。  
  
    3.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーは、プロセッサ数と使用可能なメモリを指定するハードウェア パラメーターを実稼働サーバーからインポートし、クエリ プランの生成に必要な情報をクエリ オプティマイザーに提供します。  
  
3.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、テスト サーバーのシェル データベースのチューニング完了後、チューニングの推奨設定が生成されます。  
  
4.  テスト サーバーのチューニングによって作成された推奨設定を実稼働サーバーに適用します。  
  
 次の図は、テスト サーバーと実稼働サーバーのシナリオを示しています。  
  
 ![データベース エンジン チューニング アドバイザー テスト サーバーの使用状況](../../relational-databases/performance/media/testsvr.gif "データベース エンジン チューニング アドバイザー テスト サーバーの使用状況")  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーのグラフィカル ユーザー インターフェイス (GUI) では、テスト サーバーのチューニング機能はサポートされません。  
  
## <a name="example"></a>例  
 最初に、チューニングを実行するユーザーが、テスト サーバーと実稼働サーバーの両方に存在することを確認します。  
  
 ユーザー情報をテスト サーバーにコピーした後、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの XML 入力ファイルでテスト サーバーのチューニング セッションを定義できます。 次の XML 入力ファイルの例は、テスト サーバーを指定して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーを使用してデータベースをチューニングする方法を示しています。  
  
 この例では、 `MyDatabaseName` データベースが `MyServerName`でチューニングされています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトの `MyWorkloadScript.sql`をワークロードとして使用しています。 このワークロードには、 `MyDatabaseName`に対して実行するイベントが含まれています。 このデータベースに対し、クエリ オプティマイザーによって行われるほとんどの呼び出しは、チューニング処理の一部として行われ、 `MyTestServerName`に存在するシェル データベースによって処理されます。 シェル データベースは、メタデータと統計で構成されます。 この処理により、チューニングのオーバーヘッドがテスト サーバーにオフロードされます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでは、この XML 入力ファイルを使用してチューニングの推奨設定を生成するとき、インデックスのみ (`<FeatureSet>IDX</FeatureSet>`) を考慮し、パーティション分割を行わず、 `MyDatabaseName`に既存の物理デザイン構造を保持する必要がありません。  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<DTAXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="https://schemas.microsoft.com/sqlserver/2004/07/dta">  
  <DTAInput>  
    <Server>  
      <Name>MyServerName</Name>  
      <Database>  
        <Name>MyDatabaseName</Name>  
      </Database>  
    </Server>  
    <Workload>  
      <File>MyWorkloadScript.sql</File>  
    </Workload>  
    <TuningOptions>  
      <TestServer>MyTestServerName</TestServer>  
      <FeatureSet>IDX</FeatureSet>  
      <Partitioning>NONE</Partitioning>  
      <KeepExisting>NONE</KeepExisting>  
    </TuningOptions>  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>参照  
 [テスト サーバーの使用に関する注意点](../../relational-databases/performance/considerations-for-using-test-servers.md)   
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
