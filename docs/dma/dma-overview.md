---
title: Data Migration Assistant の概要 (SQL Server) |Microsoft Docs
description: Data Migration Assistant を使用して SQL Server データベースを他の SQL Server または Azure データベースに移行する方法について説明します。
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 64c8416a15afd685559fe2d05c436c2e5fc1382d
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632854"
---
# <a name="overview-of-data-migration-assistant"></a>Data Migration Assistant の概要

Data Migration Assistant (DMA) を使用すると、新しいバージョンの SQL Server または Azure SQL Database のデータベース機能に影響する可能性のある互換性の問題を検出することで、最新のデータプラットフォームにアップグレードできます。 DMA は、ターゲット環境でのパフォーマンスと信頼性の向上を推奨します。また、スキーマ、データ、および非包含オブジェクトを移行元サーバーから対象サーバーに移動することもできます。

> [!NOTE]
> 大規模な移行 (データベースの数とサイズの観点から) では、データベースを大規模に移行できる[Azure Database Migration Service](/azure/dms/dms-overview)を使用することをお勧めします。
  
## <a name="get-data-migration-assistant"></a>Data Migration Assistant を入手する

DMA をインストールするには、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=53595)から最新バージョンのツールをダウンロードし、 **DataMigrationAssistant**ファイルを実行します。

## <a name="capabilities"></a>Capabilities

- Azure SQL database に移行するオンプレミスの SQL Server インスタンスを評価します。 評価ワークフローは、Azure SQL database の移行に影響する可能性がある次の問題を検出するのに役立ち、その解決方法についての詳細なガイダンスを提供します。

  - 移行のブロックに関する問題: オンプレミスの SQL Server データベースの Azure SQL Database への移行をブロックする互換性の問題を検出します。 DMA は、これらの問題に対処するための推奨事項を提供します。

  - 部分的にサポートされている機能またはサポートされていない機能: ソース SQL Server インスタンスで現在使用されている機能またはサポートされていない機能を検出します。 DMA は、一連の推奨事項、Azure で利用できる代替アプローチ、および移行プロジェクトに組み込むことができるようにするための手順を軽減します。

- オンプレミスの SQL Server へのアップグレードに影響する可能性がある問題を検出します。 これらは、互換性の問題として記述され、次のカテゴリに分類されます。

  - 重大な変更
  - 動作の変更
  - 非推奨の機能

- アップグレード後にデータベースが恩恵を受けることのできるターゲット SQL Server プラットフォームの新機能について説明します。 これらは、機能に関する推奨事項として説明されており、次のカテゴリに分類されています。

  - パフォーマンス
  - セキュリティ
  - ストレージ

- オンプレミスの SQL Server インスタンスを、オンプレミスでホストされている最新の SQL Server インスタンスに、またはオンプレミスネットワークからアクセス可能な Azure 仮想マシン (VM) に移行します。 Azure VM には、VPN またはその他のテクノロジを使用してアクセスできます。 移行ワークフローは、次のコンポーネントを移行するのに役立ちます。

  - データベースのスキーマ
  - データとユーザー
  - サーバー ロール
  - SQL Server と Windows ログイン

- 移行が成功すると、アプリケーションはターゲット SQL Server データベースにシームレスに接続できるようになります。

- Azure SQL Database または Azure SQL Database マネージインスタンスに移行するオンプレミスの SQL Server Integration Services (SSIS) パッケージを評価します。 この評価は、移行に影響する可能性がある問題を発見するのに役立ちます。 これらは、互換性の問題として記述され、次のカテゴリに分類されます。

  - 移行ブロッカー: ソースパッケージの Azure への移行を妨げる互換性の問題を検出します。 DMA は、これらの問題に対処するための推奨事項を提供します。

  - 情報に関する問題: ソースパッケージで使用される部分的にサポートされている機能または非推奨の機能を検出します。

## <a name="prerequisites"></a>前提条件

評価を実行するには、SQL Server **sysadmin**ロールのメンバーである必要があります。

## <a name="supported-source-and-target-versions"></a>サポートされているソースとターゲットのバージョン

DMA を使用すると、以前のバージョンの SQL Server アップグレードアドバイザーがすべて置き換えられます。ほとんどの SQL Server バージョンでは、アップグレードに使用する必要があります。 サポートされているソースとターゲットのバージョンは次のとおりです。

**文書**

- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Windows での SQL Server 2017

**ターゲット**

- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Windows および Linux での SQL Server 2017
- SQL Server 2019
- Azure SQL Database 単一データベース
- Azure SQL Database マネージド インスタンス
- Azure 仮想マシンで実行されている SQL server

## <a name="see-also"></a>参照

[SQL Server の移行を評価する](../dma/dma-assesssqlonprem.md)

[Data Migration Assistant: 構成設定](../dma/dma-configurationsettings.md)

[Data Migration Assistant を使用したオンプレミスの SQL Server の移行](../dma/dma-migrateonpremsql.md)

[Data Migration Assistant: ベストプラクティス](../dma/dma-bestpractices.md)
