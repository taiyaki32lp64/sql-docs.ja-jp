---
title: ワークロード比較プロセスの概要
description: Database Experimentation Assistant (DEA) は、アップグレードや新しいインデックスなど、SQL Server 環境で変更を行うための A/B テストソリューションです。
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: rajsell
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 36e36060e16ff85ba2b1fa58d9d900231cf6581f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258520"
---
# <a name="overview-of-the-workload-comparison-process"></a>ワークロード比較プロセスの概要

Database Experimentation Assistant (DEA) を使用すると、(現在の環境の) 移行元サーバーのワークロードが新しい環境でどのように動作するかを評価できます。 DEA では、次の3つの段階を実行して A/B テストを実行します。

- 移行元サーバーでワークロードトレースをキャプチャする。
- ターゲット1とターゲット2でキャプチャされたワークロードトレースを再生しています。
- ターゲット1とターゲット2から収集された、再生されたワークロードトレースを分析しています。

この記事では、このプロセスの概要について説明します。

## <a name="capturing-a-workload-trace"></a>ワークロードトレースのキャプチャ

A/B テスト SQL Server の最初の段階では、移行元サーバーでトレースをキャプチャします。 通常、ソース サーバーは実稼働サーバーです。 トレースファイルは、タイムスタンプを含む、そのサーバー上のクエリワークロード全体をキャプチャします。

考慮事項:

- 開始する前に、トレースをキャプチャするデータベースを必ずバックアップしてください。
- DEA ユーザーは、Windows 認証を使用してデータベースに接続できる必要があります。
- SQL Server サービスアカウントは、ソーストレースファイルのパスにアクセスできる必要があります。
- DEA でクエリのパフォーマンスが向上したか低下しているかを判断するには、そのクエリがキャプチャ期間中に少なくとも15回実行される必要があります。

## <a name="replaying-a-workload-trace"></a>ワークロードトレースの再生

A/B テスト SQL Server の2番目の段階では、2つの対象サーバーでキャプチャしたトレースファイルを再生します。

ターゲット1は、提案されたターゲット環境を模倣する移行元サーバーターゲット2を模倣します。

ターゲット1とターゲット2のハードウェア構成は、提案された変更のパフォーマンスの影響を SQL Server が正確に分析できるようにできるだけ類似している必要があります。

考慮事項:

- ワークロードトレースを再生するには、分散再生 (DReplay) トレースを実行するようにコンピューターを設定する必要があります。
- 移行元サーバーのバックアップを使用して、対象サーバー上のデータベースを復元してください。
- 評価結果の一貫性を向上させるには、サービスアプリケーションで SQL Server サービス (MSSQLSERVER) を再起動することをお勧めします。 SQL Server のクエリキャッシュは、評価結果に影響を与える可能性があります。

## <a name="analyzing-the-replayed-workload-traces"></a>再生されたワークロードトレースの分析

プロセスの最後の段階では、再生トレースを使用して分析レポートを生成し、提案された変更によって生じる可能性のあるパフォーマンスへの影響についての洞察をレポートに確認します。

考慮事項:

- 1つ以上のコンポーネントが不足している場合は、新しい分析レポートを生成しようとすると (インターネット接続が必要)、[前提条件] ページがダウンロードのリンクと共に表示されます。
- 以前のバージョンのツールで生成されたレポートを表示するには、最初にスキーマを更新する必要があります。

## <a name="see-also"></a>参照

- サーバーで発生するイベントのログを使用してトレースファイルを生成する方法については、「 [Database Experimentation Assistant でトレースをキャプチャ](database-experimentation-assistant-capture-trace.md)する」を参照してください。