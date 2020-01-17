---
title: Data Migration Assistant を使用して SQL Server ログインを移行する
description: Data Migration Assistant を使用して SQL Server ログインを移行する方法について説明します
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.custom: seo-lt-2019
ms.openlocfilehash: 368372ab7324b11e9f7fdaa6af94d5ba2c0534ad
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056479"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Data Migration Assistant を使用して SQL Server ログインを移行する

この記事では、Data Migration Assistant を使用した SQL Server ログインの移行の概要について説明します。

> [!IMPORTANT]
> このトピックは、オンプレミスの製品の新しいバージョンへの SQL Server のアップグレード、または Azure Virtual Machines での SQL Server に関連するシナリオに適用されます。

## <a name="which-logins-are-migrated"></a>移行されるログイン

- Windows プリンシパル (ドメインユーザーや Windows ドメイングループなど) に基づいてログインを移行できます。 SQL 認証に基づいて作成されたログインを移行することもできます (SQL Server ログインとも呼ばれます)。

- 現在、Data Migration Assistant では、スタンドアロンのセキュリティ証明書 (証明書にマップされたログイン) に関連付けられているログイン、スタンドアロンの非対称キー (非対称キーにマップされたログイン)、および資格情報にマップされたログインはサポートされていません。

- Data Migration Assistant では、 **sa**ログインとサーバーの原則を、2つのハッシュマーク (\#\#) で囲まれた名前で移動しません。これは内部でのみ使用されます。

- 既定では、Data Migration Assistant は、移行するすべての修飾されたログインを選択します。 必要に応じて、移行する特定のログインを選択できます。 すべての修飾されたログインを Data Migration Assistant 移行する場合、ログインユーザーマッピングは、移行されるデータベース内にそのまま残ります。

  特定のログインを移行する場合は、移行対象として選択したデータベース内の1人以上のユーザーにマップされているログインを選択してください。

- ログインの移行の一部として、Data Migration Assistant は、ユーザー定義のサーバーロールを移動し、ユーザー定義のサーバーロールにサーバーレベルの権限を追加します。 ロールの所有者は、 **sa**プリンシパルに設定されます。

## <a name="during-and-after-migration"></a>移行中および移行後

- ログインの移行の一部として、Data Migration Assistant はソース SQL Server に存在するため、ターゲット SQL Server の securables にアクセス許可を割り当てます。

  ログインがターゲット SQL Server に既に存在する場合、Data Migration Assistant は securables に割り当てられたアクセス許可のみを移行し、ログイン全体は再作成されません。

- Data Migration Assistant を使用すると、ログインが対象サーバーに既に存在する場合に、ログインをデータベースユーザーにマップすることができます。

- 移行の結果を確認して、ログインの移行の全体的な状態と、推奨される移行後の操作について理解することをお勧めします。

## <a name="resources"></a>リソース

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Data Migration Assistant: 構成設定](../dma/dma-configurationsettings.md)
