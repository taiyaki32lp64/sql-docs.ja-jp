---
title: Data Migration Assistant のベスト プラクティス
description: Data Migration Assistant を使用して SQL Server データベースを移行するためのベストプラクティスについて説明します
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: ef953aa369e831e47d38db403b982919bd4bd830
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056556"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Data Migration Assistant を実行するためのベストプラクティス
この記事では、のインストール、評価、移行に関するベストプラクティスについて説明します。

## <a name="installation"></a>インストール
Data Migration Assistant を SQL Server ホストコンピューターに直接インストールして実行しないでください。

## <a name="assessment"></a>調査
- 運用データベースに対して、ピーク時以外の時間帯に評価を実行します。
- 評価期間を短縮するために、**互換性の問題**と**新機能の推奨事項**の評価を個別に実行します。

## <a name="migration"></a>移行
- ピーク時以外の時間帯にサーバーを移行します。

- データベースを移行する場合は、移行元サーバーと移行先サーバーがアクセスできる1つの共有場所を提供し、可能であればコピー操作を回避します。 コピー操作では、バックアップファイルのサイズに基づいて遅延が発生する場合があります。 また、コピー操作により、追加の手順が原因で移行が失敗する可能性も高くなります。 1つの場所が指定されている場合、Data Migration Assistant はコピー操作をバイパスします。
 
    また、移行の失敗を回避するために、共有フォルダーに正しいアクセス許可を与えるようにしてください。 このツールでは、正しいアクセス許可が指定されています。 SQL Server インスタンスがネットワークサービスの資格情報で実行されている場合は、共有フォルダーに対する適切なアクセス許可を SQL Server インスタンスのコンピューターアカウントに付与します。

- ソースサーバーと対象サーバーへの接続時に、暗号化接続を有効にします。 SSL 暗号化を使用すると、Data Migration Assistant と SQL Server インスタンス間のネットワーク経由で転送されるデータのセキュリティが向上します。これは、特に SQL ログインを移行する場合に便利です。 SSL 暗号化を使用せず、攻撃者によってネットワークが侵害された場合、移行される SQL ログインは攻撃者によってすぐに傍受または変更される可能性があります。

    一方、すべてのアクセスにセキュリティで保護されたイントラネット構成が使用される場合には、暗号化は必ずしも必要ありません。 暗号化を有効にすると、パケットの暗号化と暗号化解除に必要な追加のオーバーヘッドが発生するため、パフォーマンスが低下します。 詳細については、「 [SQL Server への接続の暗号化](https://go.microsoft.com/fwlink/?linkid=832513)」を参照してください。
