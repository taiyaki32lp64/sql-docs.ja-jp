---
title: SQL Server 2014 ハイブリッドクラウドの概要 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 711d9d5bf7a3268b400eae4b1b117b4034133f5c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228069"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>SQL Server 2014 ハイブリッド クラウドの概要
 ほとんどのアプリケーションは、高い効率、ビジネス価値、複雑なハードウェア構成、非常に高いピーク性能の要求などの重要な課題に直面しており、業界と企業の規制に準拠する必要があります。 これらすべての要因を考慮に入れ、エンタープライズ グレードのテクノロジを構築する作業は、非常に困難になる可能性があります。 Microsoft ハイブリッド クラウド戦略は、従来型のプライベート クラウド、パブリック クラウド、およびハイブリッド クラウド環境に対して、これらの主要な課題を克服するためのサポートを提供します。 
 
 ニーズに応じて拡張できる柔軟な IT インフラストラクチャがビジネスで必要な場合は、データセンターまたは Azure グローバルデータセンターのパブリッククラウドでプライベートクラウドを構築できます。 パブリック クラウドの要件を満たすようにデータ センターを拡張する場合は、ハイブリッド クラウド モデルを構築することになります。 
 
 このトピックでは、ハイブリッドクラウドのシナリオをサポートする SQL Server 2014 の機能について説明します。 Microsoft ハイブリッド クラウド戦略と SQL Server の詳細については、「 [SQL Server ハイブリッド IT](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) 」Web サイトを参照してください。 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server、Azure、ハイブリッドクラウド 
 Microsoft のテクノロジを使用すると、内部設置型とクラウドの両方でコードを実行するか、内部設置型のデータを使用してクラウドで実行するか、または複数のデータ センターを活用してクラウドで全体を実行することができます。 したがって、既存の IT 投資の価値を保ったまま、独自のペースでアプリケーションをクラウドに移行することができます。 
 
 この記事では、オンプレミスの SQL Server から Azure パブリッククラウドサービス[(azure Virtual Machines および Azure Storage で SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)にまたがるハイブリッドクラウドのシナリオに焦点[](https://www.azure.com/documentation/services/storage/)を当てます。 具体的には、次のシナリオについて説明します。 
 
-  [Azure Storage との間でのデータベースのバックアップと復元](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Azure Virtual Machines でのデータベースレプリカの管理](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Azure Storage に SQL Server データファイルを格納する](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [既存の SQL Server データベースを Azure Virtual Machines に移行する](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>SQL Server および Microsoft Azure 向けのハイブリッドクラウドシナリオ 
 
#### <a name="backup"></a>Azure Storage との間でのデータベースのバックアップと復元 
 管理者の業務のうち最も基本的なものは、データベースのバックアップと復元です。 SQL Server と Azure では、クラウド内のデータベースを安全にバックアップできます。 
 
 Azure Storage をバックアップ先として SQL Server のバックアップと復元の機能を使用する主な利点は次のとおりです。 
 
-  容量無制限の低コスト ストレージ 
 
-  可用性の高いストレージ (地理的に分散したレプリケートによるデータ損失防止の保証) 
 
-  ディザスター リカバリーとコンプライアンスの要件をサポートできるオフサイト ストレージ 
 
-  リモート バックアップおよび復元の簡略化されたプロセス 
 
 次に、クラウドと内部設置型のシナリオで使用できる SQL Server のバックアップと復元の機能の一覧を示します。 
 
-  [SQL Server backup TO URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)機能を使用すると、バックアップ先として url を指定することで Azure Storage にバックアップできます。 この機能を使用すると、手動のバックアップを実行することも、ローカル ストレージまたはその他のオフサイト オプションを活用する場合と同じように独自のバックアップ方法を構成することもできます。 
 
-  [バックアップ暗号化](../relational-databases/backup-restore/backup-encryption.md)機能を使用すると、ストレージの保存先 (オンプレミスと Azure Storage) のバックアップを作成するときに、データを暗号化することができます。 
 
-  [バックアップ圧縮 (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md)機能を使用すると、同じデータの圧縮されていないバックアップよりも小さいバックアップを作成できます。 バックアップを圧縮すると、必要とされるデバイス I/O が少なくなるため、通常はバックアップ速度が大幅に向上します。 これにより、バックアップファイルを Azure Storage に格納する際に大きなメリットが得られます。 
 
-  [SQL Server Managed backup To Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx)機能を使用すると、SQL Server データベースを[Azure Storage](https://www.azure.com/documentation/services/storage/)に自動的にバックアップできます。 この機能を使用すると、SQL Server を構成して、単一データベースまたは複数データベースのバックアップ方法やスケジュールを管理することも、インスタンス レベルでの既定値を設定することもできます。 
 
-  [SQL Server backup To Azure Tool](https://www.microsoft.com/download/details.aspx?id=40740)を使用すると、ローカルまたはクラウドに格納されている SQL Server バックアップを Azure Blob Storage して暗号化し、圧縮することができます。 このツールにより、SQL Server 2005、2008、2008 R2、2014 などの SQL Server の複数のバージョンにまたがって、単一のクラウド バックアップ戦略を使用することができます。 
 
#### <a name="replica"></a>Azure Virtual Machines でのデータベースレプリカの管理 
 データベースに対して安定したディザスターリカバリーソリューションを用意することは、ビジネスの成功に不可欠です。 ほとんどの顧客は、データベース レプリカを格納するためにディザスター リカバリー サイトを構成し、追加のハードウェアを購入する必要があります。 SQL Server と Azure を使用すると、データベースの1つ以上のレプリカをクラウドで管理できます。 
 
 Azure でセカンダリレプリカを維持する主な利点は次のとおりです。 
 
-  低コストのディザスター リカバリー ソリューション 
 
-  アプリケーションの透過的なフェールオーバー 
 
-  複数のレプリカを活用した、読み取りワークロードとバックアップ作業のオフロード 
 
 次のいずれかの方法を使用して、Azure でセカンダリレプリカを維持することができます。 
 
-  [Azure のレプリカ追加ウィザード](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx)を使用すると、ディザスターリカバリーのために azure の仮想マシンにデータベースの1つまたは複数のレプリカをデプロイできます。 
 
-  AlwaysOn 可用性グループ、データベースミラーリング、およびログ配布は、アプリケーションの高可用性とディザスターリカバリーのニーズに対応するために使用できる最も一般的なテクノロジです。 詳細については、「 [Azure Virtual Machines での SQL Server の高可用性とディザスターリカバリー](https://msdn.microsoft.com/library/azure/jj870962.aspx)」を参照してください。 
 
#### <a name="store"></a>Azure Storage に SQL Server データファイルを格納する 
 オンプレミスの SQL Server データファイルを Azure Storage に格納すると、データベースに対して柔軟で信頼性が高く、無制限のオフサイトストレージが提供されます。 SQL Server 2014 以降では、 [Miceosoft Azure の SQL Server データファイル](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure)を使用して、SQL Server データベースファイルを Azure Storage に格納できます。 この機能を使用すると、オンプレミスのデータベースのデータファイルとログファイルを Azure Storage に移動し、SQL Server のコンピューティングノードをオンプレミスで実行し続けることができます。 この機能により、Azure Storage に無制限のストレージ容量を使用できます。 
 
 SQL Server データ Azure Storage ファイルを格納する主な利点は次のとおりです。 
 
-  Azure Storage の低コストの無制限ストレージ 
 
-  履歴の読み取りワークロードをクラウドにオフロードし、内部設置型アプリケーションをサポートする用途に最適 
 
-  計算インスタンス (SQL Server のインスタンス) とデータ (SQL Server データ ファイル) を分離することにより、ディザスター リカバリーを推進 これにより、障害が発生した場合に、オンプレミス環境または Azure 仮想マシン内の SQL Server の別のインスタンスにデータベースを簡単にアタッチできるようになります。 
 
#### <a name="migrate"></a>既存の SQL Server データベースを Azure Virtual Machines に移行する 
 クラウド コンピューティングによって、容量無制限の仮想化リソースを従量制で使用できるなど、企業にとっていくつかの主要な利点がもたらされ、自社独自のデータセンターを構築して管理する代わりに、一般に公開されているクラウド データ センターを活用して IT コストとハードウェア コストを削減することができます。 
 
 [Azure Virtual Machines の SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)を使用すると、コードを変更することなく、既存のオンプレミスアプリケーションを azure に移行することができます。 管理者と開発者は、内部設置型で使用できるのと同じ開発ツールと管理ツールを引き続き使用できます。 
 
 オンプレミスの SQL Server から Azure 仮想マシンで実行されている SQL Server にデータベースを移動するには、通常、次のいずれかのパスを取得します。 
 
-  **データベースのみの移動:** 既存のオンプレミスデータベースを Azure Virtual Machines の SQL Server に移行するために使用できるツールと手法がいくつかあります。 Azure Virtual Machines の SQL Server への移行に関するガイドラインと推奨事項については、「 [azure Virtual Machines で SQL Server に移行する](https://msdn.microsoft.com/library/dn133142.aspx)ための準備」および「 [Azure の仮想マシンの SQL Server へ](https://msdn.microsoft.com/library/jj156165.aspx)の移行」を参照してください。 
 
   さらに、SQL Server 2014 以降では、新しいウィザード[SQL Server データベースを Microsoft Azure 仮想マシンにデプロイ](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)して、Azure 仮想マシンで実行されている別の SQL Server インスタンスにデータベースをデプロイすることができます。 
 
-  **仮想マシン全体の移動:** 独自の SQL Server 仮想マシンを Azure に持ち込むことも、プラットフォームイメージを使用して仮想マシンを作成することもできます。 次に、既にデータを格納しているデータ ディスクをアップロードして仮想マシンにアタッチすること、または空のディスクを仮想マシンにアタッチすることができます。 データディスクが接続された Azure Virtual Machines に SQL Server データインスタンスを用意すると、データファイルとアプリケーションデータに対して別の永続的なストレージが提供されます。 包括的な情報と操作方法については、「 [Azure Virtual Machines での SQL Server デプロイ](https://msdn.microsoft.com/library/dn133141.aspx)」を参照してください。 
 
 アプリケーション層 (プレゼンテーション層、ビジネス層、データベース層など) を Azure Virtual Machines に移行する予定がある場合は、「 [azure Virtual Machines SQL Server のアプリケーションパターンと開発戦略](https://msdn.microsoft.com/library/dn574746.aspx)」に記載されている推奨事項を確認することをお勧めします。 この記事の目的は、ソリューション設計者および開発者に、既存のアプリケーションを Azure に移行する際や Azure で新しいアプリケーションを開発する際に利用できる優れたアプリケーション アーキテクチャと設計の基礎を理解してもらうことです。 アプリケーション パターンごとに、この記事では内部設置型のシナリオ、それに相当するクラウド対応ソリューション、および関連する技術的な推奨事項について説明します。 また、アプリケーションを正しく設計できるように、Azure 固有の開発計画についても説明します。 
 
## <a name="see-also"></a>参照 
 [SQL Server 2014 CTP2 製品ガイド](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Microsoft SQL Server ハイブリッド クラウドのブログ シリーズ](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [データ処理を中心とするアプリケーションの Azure への移行](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
