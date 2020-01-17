---
title: Azure SQL Database への移行の準備 SQL Server を評価する
titleSuffix: Data Migration Assistant
description: Data Migration Assistant を使用して、に移行するための SQL Server データ資産を移行する方法について説明し Azure SQL Database
ms.date: 12/19/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.custom: seo-lt-2019
ms.openlocfilehash: 6f9d3d97d939586683015f38ab17c00dd03ca122
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253511"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Data Migration Assistant を使用して Azure SQL Database に移行する SQL Server のデータ資産の準備状況を評価する

1つのサービスとしてのプラットフォーム (PaaS) オファリングは、膨大な数の SQL Server インスタンスと数千のデータベースを Azure SQL Database に移行しています。 このプロセスを可能な限り合理化するには、移行に関する相対的な準備を十分に理解しておく必要があります。 完全に準備されているサーバーやデータベースや、移行の準備を行うために最小限の労力を必要とするサーバーやデータベースを含む、低負荷の果物を特定すると、作業が容易になり、加速します。

この記事では、 [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017)を利用して準備結果を要約し、 [Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)ハブに表示するための詳細な手順について説明します。

>
> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Data-Migration-Assistant/player?WT.mc_id=dataexposed-c9-niner]

## <a name="create-a-project-and-add-a-tool"></a>プロジェクトの作成とツールの追加

Azure サブスクリプションで新しい Azure Migrate プロジェクトを設定し、ツールを追加します。

Azure Migrate のプロジェクトは、評価または移行しようとしている環境から収集された検出、評価、移行のメタデータを格納するために使用されます。 また、プロジェクトを使用して、検出された資産を追跡し、評価と移行を調整します。

1. Azure portal にサインインし、[**すべてのサービス**] を選択して、Azure Migrate を検索します。
2. 
  **[サービス]** で **[Azure Migrate]** を選択します。

   ![Azure Migrate-サービスの選択](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. [**概要**] ページで、[**データベースの評価と移行**] を選択します。

   ![Azure Migrate-評価の開始](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. [**データベース**] の [**はじめ**に] で、[**ツールの追加**] を選択します。

   ![Azure Migrate-ツールの追加](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. [**プロジェクトの移行**] タブで、Azure サブスクリプションとリソースグループを選択します (リソースグループをまだ持っていない場合は、作成します)。
6. [**プロジェクトの詳細**] で、プロジェクトの名前とプロジェクトを作成する場所を指定します。

    ![Azure Migrate-[ツール] ダイアログボックスの追加](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    Azure Migrate プロジェクトは、これらのいずれの地域でも作成できます。

    | **Geography**  | **ストレージの場所のリージョン** |
    | ------------- | ------------- |
    | アジア | 東南アジアまたは東アジア |
    | ヨーロッパ | 南ヨーロッパまたは西ヨーロッパ |
    | イギリス | 英国南部または英国西部 |
    | 米国 | 米国中部または米国西部 2 |

    プロジェクトのために指定した地理的な場所は、オンプレミスの VM から収集されたメタデータを格納するためにのみ使用されます。 実際の移行では、任意のターゲット リージョンを選択できます。

7. [**次へ**] を選択し、アセスメントツールを追加します。

   > [!NOTE]
   > プロジェクトを作成するときは、少なくとも1つのアセスメントツールまたは移行ツールを追加する必要があります。

8. [**評価ツールの選択**] タブの [ **Azure Migrate: データベース評価**は、追加する評価ツールとして表示されます。 現在評価ツールが必要ない場合は、[**今すぐの評価ツールの追加をスキップ**する] チェックボックスをオンにします。 
  **[次へ]** を選択します。

    ![Azure Migrate-[評価ツール] タブの選択](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. [**移行ツールの選択**] タブの**Azure Migrate: [データベースの移行**] が、追加する移行ツールとして表示されます。 移行ツールを現在必要としていない場合は、**今すぐ移行ツールの追加をスキップ**します。 
  **[次へ]** を選択します。

    ![Azure Migrate-[移行ツール] タブの選択](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. [**レビュー + ツールの追加**] で、設定を確認し、[**ツールの追加**] を選択します。

    ![Azure Migrate-レビュー + ツールの追加] タブ](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    プロジェクトを作成した後、サーバー、ワークロード、データベース、および web アプリの評価と移行に使用する追加のツールを選択できます。

## <a name="assess-and-upload-assessment-results"></a>評価結果の評価とアップロード

移行プロジェクトを正常に作成した後、[**評価ツール**] の [ **Azure Migrate: データベース評価**] ボックスで、Data Migration Assistant ツールをダウンロードして使用するための手順を説明します。

   ![Azure Migrate 評価ツールが追加されました](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. 提供されたリンクを使用して Data Migration Assistant をダウンロードし、ソース SQL Server インスタンスにアクセスできるコンピューターにインストールします。
2. Data Migration Assistant を開始します。

### <a name="create-an-assessment"></a>評価を作成する

1. 左側で**+** アイコンを選択し、[評価]**プロジェクトタイプ**を選択します。
2. プロジェクト名を指定し、移行元サーバーと移行先サーバーの種類を選択します。

    オンプレミスの SQL Server インスタンスを SQL Server の新しいバージョンまたは Azure VM でホストされている SQL Server にアップグレードする場合は、ソースとターゲットのサーバーの種類を**SQL Server**に設定します。 Azure SQL Database (PaaS) ターゲット準備の評価の対象サーバーの種類を**Azure SQL Database Managed Instance**に設定します。

3. [**作成**] を選択します。

   ![Azure Migrate-Data Migration Assistant インターフェイス](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>評価オプションの選択

1. レポートの種類を選択します。

    次のいずれかまたは両方のレポートの種類を選択できます。
    * データベース互換性をチェックする
    * 機能の類似性をチェックする

   ![Azure Migrate-Data Migration Assistant 評価オプション画面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. 
  **[次へ]** を選択します。

### <a name="add-databases-to-assess"></a>評価するデータベースの追加

1. [**ソースの追加**] を選択し、[接続の開始] メニューを開きます。
2. SQL server インスタンス名を入力し、認証の種類を選択して、適切な接続プロパティを設定し、[**接続**] を選択します。
3. 評価するデータベースを選択し、[**追加**] を選択します。

   > [!NOTE]
   > 複数のデータベースを削除するには、Shift キーまたは Ctrl キーを押しながら選択し、[ソースの削除] をクリックします。 [ソースの追加] ボタンを使用して、複数の SQL Server インスタンスからデータベースを追加することもできます。

4. [**次**へ] を選択して評価を開始します。

   ![Azure Migrate-Data Migration Assistant-[ソースの選択] 画面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. 評価が完了したら、[ **Azure Migrate にアップロード**] を選択します。

   ![Azure Migrate Data Migration Assistant-レビュー結果画面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Azure ポータルにサインインします。

   ![Azure Migrate Data Migration Assistant-レビュー結果画面](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. 評価結果をアップロードするサブスクリプションと Azure Migrate プロジェクトを選択し、[**アップロード**] を選択します。

   評価のアップロードの確認を待ちます。

## <a name="view-target-readiness-assessment-results"></a>ターゲットの準備の評価結果を表示する

1. Azure portal にサインインし、Azure migrate を検索して、select **Azure Migrate**を検索します。

   ![Azure Migrate-Azure portal サービス検索](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. [**データベースの評価と移行**] を選択して、評価結果を取得します。

   ![Azure Migrate-評価結果の確認](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    SQL Server 準備の概要を表示し、適切な移行プロジェクトであることを確認します。それ以外の場合は、[変更] オプションを使用して別の移行プロジェクトを選択します。

    評価結果を Azure migrate プロジェクトに更新するたびに、Azure migrate hub はすべての結果を統合し、概要レポートを提供します。  複数の Data Migration Assistant 評価を並行して実行し、その結果を単一の移行プロジェクトにアップロードして、統合された準備レポートを取得することができます。

   ![Azure Migrate-準備の結果を確認する](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    評価された**データベースインスタンス**: これまでに評価された SQL Server インスタンスの数。
    **評価**されたデータベース: 1 つ以上の SQL Server インスタンスで評価されたデータベースの総数: **SQL DB の準備ができて**いるデータベースの数: Azure SQL Database (PaaS) に移行する準備ができているデータベースの数。
    **AZURE SQL VM の準備ができているデータベース**: データベースの数は、Azure SQL Database (PaaS) に1つ以上の移行ブロックを構成しますが、Azure SQL Server vm に移行する準備ができています。

3. [評価された**データベースインスタンス**] を選択して SQL Server インスタンスレベルビューに移動します。

   ![Azure Migrate-インスタンスの準備状態の確認](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    Azure SQL Database (PaaS) に移行する各 SQL Server インスタンスの準備状態の割合を確認できます。

4. 特定のインスタンスを選択して、データベース準備ビューに移動します。

   ![Azure Migrate-データベースの準備状況の確認](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    各データベースあたりの移行ブロックの数を確認できます。上記のビューの各データベースで推奨されるターゲットです。

5. DMA 評価の結果を確認して、移行ブロッカーの詳細を確認します。

   ![Azure Migrate-移行ブロックの確認](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>参照

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: 構成設定](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: ベストプラクティス](../dma/dma-bestpractices.md)
