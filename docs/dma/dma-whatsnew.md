---
title: Data Migration Assistant の新機能 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 83009008745a696919aa5ae5795d60ddfe9ba80b
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632886"
---
# <a name="whats-new-in-data-migration-assistant"></a>Data Migration Assistant の新機能

この記事では、Data Migration Assistant の各リリースで追加された機能の一覧を示します。

## <a name="data-migration-assistant-v-50"></a>Data Migration Assistant v 5.0

Data Migration Assistant の v1.0 リリースでは、次の機能がサポートされています。

- 評価とアップグレードのターゲットとして、Windows の場合は2019、Linux の場合は SQL Server 2019 SQL Server。
- 以前のバージョンの Data Migration Assistant で作成された評価の保存と読み込みのサポートを含む、評価の保存と読み込み。
- SSISDB およびパッケージストアでホストされている SSIS パッケージでホストされている SQL Server Integration Services (SSIS) プロジェクトを評価します。 データベース Migration Assistant は、ソースパッケージで使用されているサポートされていない、部分的にサポートされている機能や非推奨の機能、互換性に関する問題を検出し、これらの問題に対処するための推奨事項を提供
- 外部アプリケーションからの SQL クエリ (ソースコード内のC# sql クエリなど) の評価。 ユーザーは、データアクセス移行ツールキットを使用して、ソースコードでC#使用される SQL クエリの完全な JSON レポートを生成し、そのレポートを Data Migration Assistant にアップロードできます。

さらに、このリリースの Data Migration Assistant には追加の機能強化とバグ修正が含まれており、このツールは .Net 4.7.2 に更新されました。

## <a name="data-migration-assistant-v45"></a>Data Migration Assistant version 4.5

Data Migration Assistant の version 4.5 リリースでは、ファイルシステムでホストされている SQL Server Integration Services (SSIS) パッケージを Azure SQL Database または Azure SQL Database マネージインスタンスに移行するための評価がサポートされています。

## <a name="data-migration-assistant-v44"></a>Data Migration Assistant v1.0

Data Migration Assistant の version 4.4 リリースでは、Azure Migrate への評価のアップロードがサポートされています。

## <a name="data-migration-assistant-v43"></a>Data Migration Assistant v1.0

Data Migration Assistant の v1.0 リリースでは、次のことがサポートされています。

- ワークロード評価に基づく Azure SQL Database マネージインスタンスの SKU に関する推奨事項。
- RDS SQL Server 評価のソースとして使用されます。
- ターゲットとして Azure SQL Database マネージインスタンスのエージェントジョブの評価。
- 特定の評価規則を無視する機能。DMA で構成された ' ignoreErrorCodes ' プロパティに指定されているエラーコードの一覧は、DMA 評価の結果に表示されません。
- ジョブアクティビティステップでの T-sql クエリの評価と適切な推奨事項の提供
- 拡張イベントの評価 (パブリックプレビュー)。

さらに、このリリースの DMA では、データベース内の多数のスキーマオブジェクトを処理するパフォーマンスが向上し、に関連するバグの修正が行われています。

- ネイティブコンパイルを使用してコンパイルされたプロシージャ (場合によっては)。
- 複雑なデータベーススキーマ。

## <a name="data-migration-assistant-v42"></a>Data Migration Assistant v5.0

Data Migration Assistant のバージョン4.2 リリースでは、オンプレミスの SQL Server から Azure SQL Database マネージインスタンスに移行するときに、1つまたは複数のサーバーインスタンスのターゲット準備状態評価がコマンドラインでサポートされます。 Data Migration Assistant コマンドラインを使用して、データベーススキーマに関するメタデータを収集し、ブロッカーを検出し、Azure SQL Database マネージインスタンスへの移行に影響する部分的にサポートされている機能またはサポートされていない機能について学習できるようになりました。 その後、提供された Power BI テンプレートを使用して結果を表示できます。

## <a name="data-migration-assistant-v41"></a>Data Migration Assistant v1.0

Data Migration Assistant の v2.0 リリースでは Azure SQL Database マネージインスタンスに移行するオンプレミスの SQL Server データベースの包括的な評価がサポートされるようになりました。

評価ワークフローは、Azure SQL Database マネージインスタンスへの移行に影響する可能性がある次の問題を検出するのに役立ちます。

- サポート**されていない機能または部分的にサポートされる機能**。 Data Migration Assistant は、ターゲット Azure SQL Database Managed Instance で部分的にサポートされているかサポートされていない使用中の機能について、ソース SQL Server データベースを評価します。 このツールでは、一連の推奨事項、Azure で利用可能なその他のアプローチ、および移行プロジェクトを計画する際にお客様がこの情報を考慮できるようにするための対策を講じます。

- **互換性の問題**。 Data Migration Assistant は、次の領域に関連する互換性の問題も識別します。

  - 重大な変更: ターゲットデータベースに移行する機能を損なう可能性のある特定のスキーマオブジェクト。  これらのスキーマオブジェクトは、データベースの移行後に修正することをお勧めします。
  - 動作の変更: 報告されたスキーマオブジェクトは引き続き機能しますが、パフォーマンスの低下など、動作が異なる場合があります。
  - 情報に関する問題: これらのオブジェクトは移行に影響を与えることはありませんが、機能 SQL Server のリリースで非推奨とされる可能性があります。

評価が完了したら、 [Azure Database Migration Service](https://azure.microsoft.com/services/database-migration/) (DMS) を使用して、SQL Server データベースの Azure SQL Database Managed Instance への移行を実行します。  DMS では、[オフライン](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)(1 回限り) と[オンライン](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)(最小限のダウンタイム) のデータベース移行の両方がサポートされており、Azure SQL Database Managed Instance になります。

## <a name="data-migration-assistant-v40"></a>Data Migration Assistant v4.0

Data Migration Assistant の v2.0 リリースでは、Azure SQL Database SKU 推奨事項機能が導入されています。これにより、ユーザーは、をホストしているコンピューターから収集されたパフォーマンスカウンターに基づいて、推奨される最小 Azure SQL Database SKU を特定できます。データベース. この機能では、価格レベル、コンピューティングレベル、最大データサイズに関連する推奨事項に加え、月あたりの推定コストも提供します。 また、すべてのデータベースを Azure に一括してプロビジョニングする機能も提供されます。

> [!NOTE]
> 現在、この機能は、コマンドラインインターフェイス (CLI) を介してのみ使用できます。

詳細については、[オンプレミスデータベースの適切な AZURE SQL DATABASE SKU の特定に](dma-sku-recommend-sql-db.md)関する記事を参照してください。

## <a name="data-migration-assistant-v36"></a>Data Migration Assistant v1.0

Data Migration Assistant の v1.0 リリースでは、最も一般的な移行ブロックの影響を受けるスキーマオブジェクトに対して "自動修正" が導入されています。

このリリースでは、次の移行ブロックと動作の変更に関する問題の autofix が提供されています。

- 非修飾結合構文を使用するスキーマオブジェクト。
- レガシ RAISEERROR ステートメントを使用するスキーマオブジェクト。
- Order By 整数リテラルを使用する SQL ステートメント。

Data Migration Assistant は、一覧にある問題の影響を受けるオブジェクトに対してスキーマの自動変換を実行し、スキーマ変換を続行する前にユーザーに確認を求めるメッセージを表示します。 ユーザーは、提案されたコードの変更を確認し、特定のデータベースオブジェクトのすべての変換を受け入れるか拒否するかを選択できます。

Data Migration Assistant は、Microsoft プログラム合成 (PROSE) テクノロジを使用してコード修正を提案します。 [PROSE](https://microsoft.github.io/prose/)の詳細については、こちらを参照してください。

## <a name="data-migration-assistant-v35"></a>Data Migration Assistant v1.0

Data Migration Assistant の v2.0 リリースには、次の追加情報が含まれています。

- Azure SQL Database への移行におけるパフォーマンスの大幅な向上 (ベンチマークテストでは、以前のバージョンの Data Migration Assistant) よりも4倍高速に処理が行われることを示しています。
- メモリフットプリントは、移行ワークフローの安定性を向上させるためにさらに最適化されています。
- スキーマおよびデータの移行中に評価をスキップする機能 (既に評価を実行済みで、移行前にスキーマオブジェクトの互換性を解消している場合)。
- 古いバージョンの SQL Server オンプレミスからそれ以降のバージョンへのアップグレードを実行する場合、または Azure Vm 上で SQL Server する場合に、バックアップファイルに無効なネットワーク共有パスが指定されているときに、ツールがクラッシュする問題に対処するための修正。

## <a name="data-migration-assistant-v34"></a>Data Migration Assistant 3.4

Data Migration Assistant の v1.1 リリースには、次の追加情報が含まれています。

- Azure SQL Database への移行のソースとして SQL Server 2017 がサポートされます。
- 安定性、パフォーマンス、および評価ルールの正確性に関する機能強化。

## <a name="ddata-migration-assistant-v33"></a>DData Migration Assistant v1.0

Data Migration Assistant の v2.0 リリースでは、Windows と Linux の両方で、オンプレミスの SQL Server インスタンスを SQL Server 2017 の新しいバージョンに移行できます。 Windows と Linux の移行の全体的なワークフローは同じですが、Linux 用の SQL Server 2017 に移行する場合は、いくつかの追加の考慮事項が必要です。

### <a name="specifying-the-back-up-path"></a>バックアップパスの指定

Linux と Windows では、異なるパス形式を使用します。 結果として、Linux 上の SQL Server 2017 に移行するには、ユーザーがパスの Windows と Linux の両方のバージョンを物理ファイルの場所に提供する必要があります。 物理ファイルの場所に応じて、パスの両方のバージョンをさまざまな方法で指定できます。
物理バックアップファイルが、を実行しているコンピューター上にある場合は、次のようになります。

- Linux では、"samba" 共有を使用して、ネットワーク上の他のコンピューターとファイルを共有します。
- Windows では、' mnt ' コマンドを使用して、Linux を実行しているコンピューターに共有をマウントします。

> [!NOTE]
> ' Samba ' 共有または ' mnt ' コマンドの使用の詳細については、この記事では説明しません。

### <a name="migrating-windows-logins"></a>Windows ログインの移行

Active Directory (AD) ログインの移行は Linux 上の SQL Server 2017 で正式にサポートされていますが、正常に機能するためには追加の構成が必要です。 Linux での SQL Server 2017 での Active Directory ログインの設定の詳細については、 [SQL Server on Linux での認証の Active Directory](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication)に関する記事を参照してください。 必要な構成を実行すると、セットアップが完了し、Active Directory ログインを通常どおりに移行できるようになります。 標準の SQL 認証は、追加の設定を行わなくても期待どおりに動作します。

## <a name="data-migration-assistant-v32"></a>Data Migration Assistant 3.2

Data Migration Assistant の v2.0 リリースには、次の追加情報が含まれています。

- スキーマとデータの移行は、新しい移行ワークフローで Azure SQL Database するために、オンプレミスの SQL Server データベースから有効になります。
- Azure SQL Database へのスキーマの移行中に、ソースデータベースオブジェクトに対して DMA スクリプトを実行し、潜在的な互換性の問題を修正してから Azure にスキーマをデプロイする方法に関するガイダンスを提供します。

## <a name="data-migration-assistant-v31"></a>Data Migration Assistant v1.0

Data Migration Assistant のバージョン3.1 リリースには、次の追加機能が含まれています。

- データベース照合順序、サポートされていないシステムストアドプロシージャの使用、および CLR オブジェクトに関して、Azure SQL データベースの評価に関する推奨事項が改善されました。
- Azure SQL データベースに移行するときの互換性レベル130、120、110、および100の評価ガイダンス。

## <a name="data-migration-assistant-v30"></a>Data Migration Assistant v1.0

Data Migration Assistant の v2.0 リリースでは Azure SQL Database 評価が拡張され、に関連する問題の解決に役立つ包括的な推奨事項が提供されます。

- 移行のブロックの問題。
- 部分的またはサポートされていない機能と機能。

## <a name="data-migration-assistant-v21"></a>Data Migration Assistant v1.0

Data Migration Assistant のバージョン2.1 リリースには、次の追加機能が含まれています。

- 評価を大規模に実行するのに役立つ無人モードで評価を実行するためのコマンドラインサポート。 詳細については、「[コマンドラインから Data Migration Assistant を実行](dma-commandline.md)する」を参照してください。
- ユーザーが DMA を起動して閉じるときのパフォーマンスが向上しました。
- SQL 接続のタイムアウトを構成する権限です。詳細については、「 [Data Migration Assistant の構成設定](dma-configurationsettings.md)」を参照してください。

## <a name="data-migration-assistant-v20"></a>Data Migration Assistant v2.0

V2.0 リリースの Data Migration Assistant には、ストレージの節約を最大化する適切な優先順位のテーブルを提供する拡張データベース機能の推奨事項が強化されています。

## <a name="data-migration-assistant-v10"></a>Data Migration Assistant v1.0

Data Migration Assistant の v1.0 リリースは最初のリリースであり、次の機能を備えています。

- オンプレミスバージョンの SQL Server へのアップグレードに影響する可能性がある問題の検出。 すべての結果は互換性の問題として記述されており、次の領域に分類されています。
  - 重大な変更
  - 動作の変更
  - 非推奨の機能
- アップグレード後にデータベースが恩恵を受けることのできるターゲット SQL Server プラットフォームの新機能の検出。 すべての結果は、機能に関する推奨事項として説明されており、次の領域に分類されています。
  - パフォーマンス
  - セキュリティ
  - ストレージ
- 評価を実行する最新のユーザーエクスペリエンス。

## <a name="see-also"></a>参照

[Data Migration Assistant の概要](../dma/dma-overview.md)
