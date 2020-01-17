---
title: Data Migration Assistant を使用して SSIS 移行評価を作成する
description: Azure SQL Database または Azure SQL Database マネージインスタンスに移行する前に、Data Migration Assistant を使用してオンプレミスの SQL Server 統合サービス (SSIS) を評価する方法について説明します。
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.custom: seo-lt-2019
ms.openlocfilehash: 1652d5eec9d6419e7b39f96a8b854eef8651bf26
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74687160"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>Data Migration Assistant を使用して SQL Server 統合サービスの移行評価を実行する

## <a name="prerequisites"></a>前提条件

SQL Server 統合サービス (SSIS) パッケージを評価するには、以下のコンポーネントを Data Migration Assistant と共にインストールする必要があります。

- を評価する SSIS パッケージと同じバージョンの統合サービスを SQL Server します。
- Azure Feature Pack または他のサードパーティ製のコンポーネント (評価する SSIS パッケージにこれらのコンポーネントがある場合)。  

パッケージストアの SSIS パッケージを評価するには、**管理者**アクセス権を使用して DMA を実行する必要があります。

## <a name="performance-assessments"></a>パフォーマンス評価

次の手順では、Data Migration Assistant を使用して、SQL Server 統合サービス (SSIS) パッケージを Azure SQL Database または Azure SQL Database マネージインスタンスに移行するための最初の評価を行う方法について説明します。

## <a name="create-an-assessment"></a>評価を作成する

1. [**新規**] (+) アイコンを選択し、[**統合サービス**] として**評価**プロジェクトの種類を選択します。

1. ソースとターゲットのサーバーの種類を設定します。

    ソースを**SQL Server**として選択し、対象サーバーの種類を**Azure SQL Database**または**Azure SQL Database マネージインスタンス**として設定します。

1. 
  **[作成]** をクリックします。

    ![評価の作成](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="connect-to-a-server"></a>サーバーに接続する

1. 既定のオプションに従い、[ソースの**選択**] の横にある [**次へ**] をクリックします。
1. SQL server インスタンス名を入力し、認証の種類を選択して、適切な接続プロパティを設定します。
1. OptionalSSIS パッケージが格納されているフォルダーパスを入力します。
1. Optional該当する場合は、パッケージ暗号化パスワードを入力します。
1. [転送元の SQL server に**接続**する] をクリックします。
  ![ソースの追加](media/dma-assess-ssis/dma-assess-ssis-addsource.png)

## <a name="add-sources-to-assess"></a>評価するソースの追加

1. 評価する SSIS パッケージのストレージの種類を選択し、[**追加**] を選択します。
![ソースの追加](media/dma-assess-ssis/dma-assess-ssis-addsource-type.png)
1. [**ソースの追加**] を選択して接続のフライアウトメニューを開きます (複数のフォルダーを評価する必要がある場合)。
1. 
    **[Start Assessment]** (評価の開始) をクリックします。
![評価の開始](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>結果の表示

互換性の問題カテゴリでは、オンプレミスの SSIS パッケージの Azure-SSIS Integration Runtime への移行をブロックする、部分的にサポートされている機能またはサポートされていない機能が提供 その後、これらの問題に対処するための推奨事項を提供します。

![結果の表示](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>次の手順

- [オンプレミスの SSIS ワークロードを ADF の SSIS に移行する方法の概要](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)
- [SQL Server Integration Services パッケージを Azure SQL Database マネージドインスタンスに移行する](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [SQL Server Integration Services パッケージを Azure SQL Database に再デプロイする](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages)
