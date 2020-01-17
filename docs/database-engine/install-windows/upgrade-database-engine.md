---
title: データベース エンジンのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7dcf58da00887f396568367982da97b9c75e32ad
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531559"
---
# <a name="upgrade-database-engine"></a>データベース エンジンのアップグレード

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
  このセクションの記事は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のリリースから [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードするときに役立ちます。  
  
1.  [データベース エンジンのアップグレード方法の選択](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)。 アップグレードを開始する前に、さまざまなアップグレード方法を理解する必要があります。 この記事では、アップグレードの方法と各アップグレード方法で実行する手順について説明します。  
  
2.  [データベース エンジンのアップグレード計画の策定およびテスト](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)。 アップグレードの方法を確認した後、環境に合ったアップグレード方法を開発し、既存の環境をアップグレードする前にアップグレード方法をテストします。 この記事では、アップグレード計画の開発とテストの方法について説明します。  
  
3.  [データベース エンジンのアップグレードの完了](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)。 データベース エンジンを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードし、データベースがオンラインになった後、新しいバックアップの作成、データベース機能のアップグレードによる新しい機能の有効化、フルテキスト カタログの再設定など、追加の手順を実行する必要があります。 この記事では、これらの手順について説明します。  
  
4.  [データベース互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)をアップグレードします (**適用先:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] の新しいバージョンでデータベースがオンラインになった後に行う手順の 1 つに、データベース互換性レベルを変更し、データベース機能モードをアップグレードして新しい機能を有効にするという作業があります。 これは手動で行うか、クエリ調整アシスタントで行うことができます。 

    - [データベース互換性モードの変更とクエリ ストアの使用](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。 データベース互換性レベルを手動で変更した後、クエリ ストアを使用してパフォーマンスを監視し、回帰の可能性を特定します。 この記事では、推奨プロセスについて説明し、推奨ワークフローを示します。  

    - [クエリ調整アシスタントを使用してデータベース互換性モードを変更する](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)。 手動で変更する代わりに、**クエリ調整アシスタント (QTA)** を使用し、データベース互換性レベルの推奨変更プロセスを手順に従って実行します。 この記事では、このプロセスについて説明し、QTA ワークフローの指示を示します。  

    データベース互換性レベルの変更後に利用できる新しい機能と改善された動作については、[互換性レベル間の違い](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-stored-procedures)に関するページを参照してください。

5.  [SQL Server の新機能を利用する](https://www.microsoft.com/sql-server/sql-server-2019) 最後に、前の手順を完了した時点で、新しいデータベース エンジンの特定の拡張機能を利用できる状態になっています。 この記事では、これらの拡張機能のいくつかを提案し、詳細情報へのリンクを示します。  
  
  
