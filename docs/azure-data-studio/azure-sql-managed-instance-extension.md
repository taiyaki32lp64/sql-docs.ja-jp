---
title: Azure SQL Database Managed Instance 拡張機能
titleSuffix: Azure Data Studio
description: Azure SQL Managed Instance で Azure Data Studio を使用します
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: a0fdd3c8be7e9cbe128d01736e465ae95a120d0f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258415"
---
# <a name="azure-sql-database-managed-instance-dashboard-for-azure-data-studio-preview"></a>Azure Data Studio 用の Azure SQL Database Managed Instance ダッシュボード (プレビュー)

Azure SQL Database Managed Instance 拡張機能により、[Azure Data Studio](https://github.com/Microsoft/azuredatastudio) で [Azure SQL Database マネージド インスタンス](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index)を操作するためのダッシュボードが提供されます。 この拡張機能には次の機能があります。

- 仮想コアや使用済みストレージなど、マネージド インスタンスのプロパティを表示する
- 過去 2 時間の CPU とストレージの利用状況を監視する
- 構成に関する警告およびチューニングの推奨事項を表示する
- データベース レプリカの状態を表示する
- フィルター処理されたエラー ログを表示する

## <a name="install"></a>インストール

この拡張機能の正式なリリースをインストールすることができます。 [Azure Data Studio のドキュメント](https://docs.microsoft.com/sql/azure-data-studio/extensions)の手順に従ってください。
**[機能拡張]** ウィンドウで「Managed Instance」を検索し、そこでインストールします。 インストールされた後は、拡張機能の更新があれば、自動的に通知されます。

拡張機能をインストールすると、Azure Data Studio に **[Managed Instance]\(マネージド インスタンス\)** タブが表示されます。 ここでは、お使いのマネージド インスタンスに固有の情報を確認できます。

## <a name="properties"></a>Properties

拡張機能により、お使いのマネージド インスタンスの技術的特性といくつかのリソース使用量が表示されます。

[ ![マネージド インスタンスのプロパティ](media/azure-sql-mi-extension/ads-mi-tab1.png )](media/azure-sql-mi-extension/ads-mi-tab1.png#lightbox)

上部のウィンドウには、次の詳細が表示されます。

- **[プロパティ]** 。 使用可能な仮想コア数、メモリ、ストレージなど、お使いのマネージド インスタンスに関する基本的な情報を取得します。 また、現在のサービス レベル、ハードウェアの世代、および IO 特性 (インスタンス ログ書き込みスループットやファイル I/O スループット特性など) も検出されます。
- **[Local SSD storage]\(ローカル SSD ストレージ\)** 。 General Purpose サービス レベルでは、**TempDB** ファイルはローカル環境に格納されます。 Business Critical サービス レベルでは、"_すべての_" データベース ファイルがローカル SSD ストレージに配置されます。 このセクションでは、お使いのマネージド インスタンスによって使用されているローカル ストレージの容量を確認できます。
- **[Azure Premium Disk Storage]** 。 General Purpose サービス レベルをお使いの場合、ユーザーとシステム両方のデータベース ファイルが、Azure Premium Storage に配置されます。 このセクションでは、使用済みデータ量、ファイルの数、および使用可能なストレージを確認できます。 Business Critical サービス レベルでは、このセクションには何も表示されません。
- **[Resource usage]\(リソース使用状況\)** 。 お使いのマネージド インスタンスによって過去 2 時間に使用されたストレージと CPU の割合が表示されます。 これにより、限界に近づいている場合はインスタンス サイズを増やすことができます。

## <a name="recommendations"></a>Recommendations

**[Managed Instance]\(マネージド インスタンス\)** タブで 2 番目のウィンドウを選択すると、マネージド インスタンスの最適化に役立つ推奨事項とアラートが表示されます。

[ ![マネージド インスタンスの推奨事項](media/azure-sql-mi-extension/ads-mi-tab2.png )](media/azure-sql-mi-extension/ads-mi-tab2.png#lightbox)

次の推奨事項のいくつかが表示される場合があります。

- **ストレージ スペースの制限に到達**。 不要なデータを削除するか、インスタンスのストレージ サイズを増やします。 ストレージの上限に達したデータベースでは、読み取りクエリさえ処理できない場合があります。
- **インスタンスのスループット制限に到達**。 サービス レベルの上限近くで読み取りが行われていることをユーザーに通知します: General Purpose では 22 MB/秒、Business Critical では 48 MB/秒。 バックアップを確実に実行できるように、マネージド インスタンスによって負荷が制限されることに注意してください。
- **メモリ不足**。 ページの予測保持期間が低い場合、または `PAGEIOLATCH` 待機統計が高い場合は、インスタンスでページがメモリから削除され、定常的にディスクから多くのページの読み込みが試みられていることを示している可能性があります。
- **ログ ファイルの制限**。 ログ ファイルが [General Purpose サービス レベルのファイル IO 制限](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)に近づいている場合、パフォーマンスを向上させるにはログ ファイル サイズを増やすことが必要な場合があります。
- **データ ファイルの制限**。 データ ファイルが [General Purpose サービス レベルのファイル IO 制限](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)に近づいている場合、パフォーマンスを向上させるにはファイル サイズを増やすことが必要な場合があります。 この問題によって、メモリ不足が発生し、バックアップの速度が低下している可能性があります。
- **可用性の問題**。 仮想ログ ファイルの数が多いと、パフォーマンスに影響することがあります。 ロセスで障害が発生した場合、そのような問題のため、General Purpose サービス レベルでのデータベース復旧に時間がかかる可能性があります。

これらの推奨事項を定期的に確認し、根本原因を調査して、問題を修正するアクションを講じます。 Azure SQL Database Managed Instance 拡張機能を使うと、報告された問題の一部を軽減するために実行できるスクリプトが提供されます。

## <a name="replicas"></a>レプリカ

**[Managed Instance]\(マネージド インスタンス\)** タブの 3 番目のウィンドウには、お使いのマネージド インスタンス内のデータベース レプリカの状態が表示されます。

[ ![マネージド インスタンスのレプリカ](media/azure-sql-mi-extension/ads-mi-tab3.png )](media/azure-sql-mi-extension/ads-mi-tab3.png#lightbox)

General Purpose サービス レベルでは、すべてのデータベースに 1 つの (プライマリ) レプリカがあります。 Business Critical レベルのインスタンスでは、すべてのデータベースに 1 つのプライマリ レプリカと 3 つのセカンダリ レプリカがあり、そのうち 1 つは読み取り専用ワークロードに使用されます。 **[Replicas]\(レプリカ\)** ウィンドウでは、同期プロセスを監視し、すべてのセカンダリ レプリカがプライマリ レプリカと同期されていることを確認できます。

## <a name="logs"></a>ログ

**[Managed Instance]\(マネージド インスタンス\)** の 4 番目のウィンドウには、最新の関連する SQL エラー ログ エントリが表示されます。

[ ![マネージド インスタンスのログ エントリ](media/azure-sql-mi-extension/ads-mi-tab4.png )](media/azure-sql-mi-extension/ads-mi-tab4.png#lightbox)

マネージド インスタンスでによって大量のログ エントリが生成されますが、そのほとんどは内部/システムの情報です。 また、一部のログ エントリでは、実際の論理データベース名ではなく、物理データベース名 (`GUID` の値) が示されます。

Azure SQL Database Managed Instance 拡張機能を使うと、[Dimitri Furman 法](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506)に基づいて不要なログ エントリを除外できます。 また、物理名ではなく実際の論理ファイル名が表示されます。

## <a name="reporting-problems"></a>問題の報告

Azure SQL Database Managed Instance 拡張機能に関して問題が発生した場合は、[Extension GitHub プロジェクト](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues)にアクセスし、問題を報告してください。

## <a name="code-of-conduct"></a>倫理規定

このプロジェクトは、「[Microsoft のオープン ソースの倫理規定][conduct-code]」を採用しています。

詳細については、[倫理規定の FAQ][conduct-FAQ] のページを参照してください。また、追加の質問やコメントがある場合は [opencode@microsoft.com][conduct-email] にお問い合わせください。

## <a name="next-steps"></a>次のステップ

詳細については、[GitHub プロジェクト](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/)を参照してください。

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
