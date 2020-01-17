---
title: SQL Server 2005 からアップグレードしますか? | Microsoft Docs
ms.custom: ''
ms.date: 12/15/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d50a66a-1845-4116-8b3a-7b5a2eeb78e6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d5e44dac2201953858f06d834b1831aa1a22fe3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247279"
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>SQL Server 2005 からアップグレードしますか?
  SQL Server 2005 の延長サポートの終了は、新しいバージョンの SQL Server や Azure SQL Database への早めのアップグレードをお勧めする 1 つの理由です。 アップグレードすると、セキュリティとコンプライアンスを維持し、パフォーマンスを大きく改善し、データ プラットフォームのインフラストラクチャを最適化できます。  
  
 アップグレードまたは移行の計画と自動化を行うための情報、ガイダンス、ツールの詳細については、「 [SQL Server 2005 のサポート終了](https://www.microsoft.com/server-cloud/products/sql-server-2005/)」をご覧ください。  
  
## <a name="why-upgrade"></a>アップグレードする理由  
  
> [!IMPORTANT]  
>  SQL Server 2005 の延長サポートは 2016 年 4 月 12 日で終了します。 2016 年 4 月 12 日を過ぎても SQL Server 2005 を実行している場合、セキュリティ更新プログラムを受け取れなくなります。  
  
 SQL Server 2005 からのアップグレードに関するデータシートを PDF 形式で取得するには、[ここをクリックし](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf)てください (下のサムネイル画像ではありません)。  
  
 ![SQL Server 2005 からのアップグレードに関するデータ シート](../../../2014/sql-server/install/media/sqlserver2005eos.png "SQL Server 2005 からのアップグレードに関するデータ シート")  
  
## <a name="choose-your-upgrade-option"></a>アップグレード オプションの選択  
 SQL Server 2005 からリレーショナルデータベースをアップグレードする場合は、Microsoft プラットフォームでのリレーショナルストレージのオプションを次に示します。  
  
 これらのオプションの包括的な分析の詳細を確認するには、 [こちら](https://sql05upgrade.azurewebsites.net/)をクリックします。  
  
|リレーショナル ストレージのオプション|メリット|その他の考慮すべき要素|  
|-------------------------------|--------------|-------------------------------|  
|**オンプレミスの SQL Server**<br /><br /> トランザクション システムからデータ ウェアハウスまで、あらゆる種類のデータベース アプリケーションに対して、このオプションをご検討ください。<br /><br /> 詳細については、「 [SQL Server 2014](https://www.microsoft.com/EN-US/server-cloud/products/sql-server/)」を参照してください。|ハードウェアとソフトウェアの両方を管理するので、機能と拡張性の大部分を制御できます。<br /><br /> SQL Server 2005 からアップグレードする場合は、これが最も類似した環境です。|自前のハードウェアとソフトウェアを購入、維持、管理する必要があるため、必要な先行投資は最大で、管理は最も継続的なものとなります。|  
|**Azure virtual machines でホストされている SQL Server**<br /><br /> 次のことが必要な場合は、このオプションをご検討ください。<br />-ホストされた環境への移行の利点。<br />-オペレーティング環境を制御します。<br />-SQL Server の使い慣れた機能セット。<br /><br /> 詳細については、「 [Azure Virtual Machines の概要」の SQL Server](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)を参照してください。<br /><br /> 移行について詳しくは、「 [Azure VM の SQL Server へのデータベースの移行](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/)」をご覧ください。|仮想マシン イメージのライブラリからすばやく展開できます。<br /><br /> SQL Server の完全な機能セットが利用できます。<br /><br /> ハードウェアとサーバー ソフトウェアのコストを節約できます。 1 時間単位で使用した分だけ課金されます。|SQL Server と、オペレーティング システム ソフトウェアの両方を構成して管理する必要があります。|  
|**ホストされるデータベースサービスの Azure SQL Database**<br /><br /> メンテナンスが容易で低コストのソリューションをお探しなら、このオプションをご検討ください。<br /><br /> このオプションは、必要なキャパシティがいつも同じではないアプリ、または外部アクセスを許可する必要のあるアプリに、特に適しています。<br /><br /> 詳細については、「 [SQL Database](https://azure.microsoft.com/services/sql-database/)」を参照してください。<br /><br /> 移行の詳細については、「 [Azure SQL Database への SQL Server データベースの移行](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/)」を参照してください。|すばやく展開でき、簡単にスケール アップできます。<br /><br /> 1 時間単位で使用した分だけ課金されます。<br /><br /> サービスのコストには、ストレージだけでなく高可用性の自動バックアップが含まれています。|Azure SQL Database には、ホストされるクラウド環境には当てはまらない一部の SQL Server の機能が装備されていません。 詳しくは、「 [Azure SQL Database の Transact-SQL 情報](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/)」を参照してください。<br /><br /> また、Azure SQL Database のデータベースの最大サイズは 500 GB である一方、SQL Server は 524 PB です。|  
  
 また、特定のデータおよびアプリケーションに対して、非リレーショナル ソリューションまたは NoSQL ソリューションを検討することもできます。  
  
|非リレーショナル ソリューション|メリット|  
|------------------------------|--------------|  
|**Azure DocumentDB**<br /><br /> JSON データを使用し、かつ堅牢なクエリ処理とトランザクション データ処理の組み合わせを必要とする最新のスケーラブルなモバイル アプリケーションや Web アプリケーションには、このオプションをご検討ください。<br /><br /> 詳しくは、「 [DocumentDB](https://azure.microsoft.com/services/documentdb/)」をご覧ください。|ドキュメントにはインデックスが作成されるので、使い慣れた SQL 構文を使用してクエリを実行することができます。<br /><br /> データベースはスキーマ フリーです。<br /><br /> インデックスを再構築せずに、ドキュメントにプロパティを追加できます。<br /><br /> データベース エンジンの中でも JSON および JavaScript のサポートを利用できます。<br /><br /> 地理空間データがネイティブでサポートされており、Azure Search、HDInsight、Data Factory などの他のAzure サービスと統合できます。<br /><br /> 確保されたスループット レベルで、待機時間の短い、高パフォーマンスのストレージを利用できます。|  
|**Azure テーブルストレージ**<br /><br /> ペタバイト級の半構造化データをコスト効率の高いソリューションで保存するには、このオプションをご検討ください。<br /><br /> 詳しくは、「 [テーブル ストレージ](https://azure.microsoft.com/services/storage/tables/)」をご覧ください。|データをオフラインにせずに、アプリとテーブル スキーマを改善できます。<br /><br /> シャーディングせずに、データセットをスケール アップできます。<br /><br /> 複数の領域間でデータをレプリケートする地理的冗長ストレージを利用できます。|  
  
 アップグレード オプションの詳細を含むレポート「SQL Server 2005 からの移行」を、Microsoft の指示によりダウンロードするには、 [こちらをクリック](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) してください (下のサムネイル画像ではありません)。  
  
 ![SQL Server 2005 からの移行に関するレポート](../../../2014/sql-server/install/media/sqlserver2005migratingdoc.png "SQL Server 2005 からの移行に関するレポート")  
  
## <a name="plan-your-upgrade"></a>アップグレードの計画  
  
-   アップグレードを計画する方法については、SQL Server チームからの次の一連のブログ投稿をご確認ください。  
  
    -   [SQL Server 2005 からの効率的なアップグレードの計画: ステップ1/3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [SQL Server 2005 からの効率的なアップグレードの計画: ステップ2/3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [SQL Server 2005 からの効率的なアップグレードの計画: ステップ3/3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   [SQL Server 2014 をインストールするためのハードウェアとソフトウェアの要件](hardware-and-software-requirements-for-installing-sql-server.md)など、 [SQL Server インストールの計画](../../../2014/sql-server/install/planning-a-sql-server-installation.md)に関する要件と考慮事項を確認します。  
  
-   アップグレードする方法をご確認ください。  
  
    -   トピック「 [Upgrade Database Engine](../../database-engine/install-windows/upgrade-database-engine.md)」で使用可能なアップグレード方法を確認し、計画方法とテスト方法を学習します。  
  
        > [!IMPORTANT]  
        >  SQL Server 2005 サーバーを SQL Server 2014 サーバーにイン プレースでアップグレードすることはできません。 SQL Server 2014 をインストールしてから、SQL Server 2005 データベースを新規インストールに移行する必要があります。  
  
    -   詳細が記載されている「テクニカル アップグレード ガイド」を PDF 形式で入手するには、 [こちらをクリック](https://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf)してください。  
  
-   アップグレードまたは移行の計画と自動化を行うための情報、ガイダンス、ツールの詳細については、「 [SQL Server 2005 のサポート終了](https://www.microsoft.com/server-cloud/products/sql-server-2005/)」をご覧ください。  
  
## <a name="get-sql-server-2014"></a>SQL Server 2014 の取得  
 SQL Server 2014 の評価版をダウンロードするには、[ここをクリック](https://www.microsoft.com/evalcenter/evaluate-sql-server-2014)してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014](https://www.microsoft.com/server-cloud/products/sql-server/default.aspx)   
 [SQL Server 2005 のサポート終了](https://www.microsoft.com/server-cloud/products/sql-server-2005/)   
 [SQL Server 2005 から SQL Server 2016 へのアップグレード](https://msdn.microsoft.com/library/mt168847.aspx)  
  
  
