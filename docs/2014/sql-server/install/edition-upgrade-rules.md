---
title: エディション アップグレード ルール |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 77c4d751-4fea-4e69-a7c8-ab8fc0dbadb2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 755b1b18c6d9c37ebb6052076ec5e5ab1807213c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095376"
---
# <a name="edition-upgrade-rules"></a>エディションのアップグレード規則
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによって、セットアップ操作が完了する前にコンピューターの構成が検証されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップの実行中、システム構成チェッカー (SCC) は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール先コンピューターをスキャンします。 SCC は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ操作の成功を妨げる条件がないかどうかを調べます。 セットアップでエディションのアップグレードが起動する前に、SCC は各項目の状態を取得します。 次に、必要な条件と取得した結果を比較し、ブロックの問題解決に関するガイダンスを提供します。  
  
 システム構成チェッカーは、実行された各ルールの簡単な記述と、実行ステータスを含むレポートを生成します。 システム構成チェッカーのレポートは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
 セットアップ操作を実行する前に、次のトピックを確認してください。  
  
1.  [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [SQL Server 2014 の各エディションがサポートする機能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [SQL Server インストールにおけるセキュリティの考慮事項](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [SQL Server のローカル言語版](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 その他の参考資料:  
  
1.  [サポートされているバージョンとエディションのアップグレード](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [フェールオーバー クラスタリングをインストールする前に](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="see-also"></a>参照  
 [インストール ルール](../../../2014/sql-server/install/install-rules.md)  
  
  
