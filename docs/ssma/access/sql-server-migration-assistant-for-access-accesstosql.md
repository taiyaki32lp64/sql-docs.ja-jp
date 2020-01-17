---
title: アクセスの SQL Server Migration Assistant (アクセス可能な Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: dfa640787f42d06ed65b713c9fea415dc9560a2e
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252205"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>アクセスのための SQL Server Migration Assistant (アクセス可能な Sql)

[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) のアクセスは、[!INCLUDE[msCoName](../../includes/msconame_md.md)] Access バージョン97から2010にデータベースを移行するためのツールであり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017、windows および Linux 上の [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2019、[!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL Database。 SSMA for Access は、Access データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL database オブジェクトに変換し、それらのオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に読み込み、Access から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database にデータを移行します。
  
このドキュメントでは、アクセスのための SSMA について説明します。また、Access データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に移行するための詳細な手順と、移行後に発生する可能性がある問題についての情報を提供します。  
  
## <a name="contents"></a>目次  
  
|セクション|[説明]|
|-----------|---------------|
|[SSMA for Access の新機能](https://msdn.microsoft.com/a24d3fc0-6911-4bfa-828a-197abf222e02)|SSMA リリースに対する変更の一覧を示します。|  
|[アクセスのための SQL Server Migration Assistant のインストール](installing-sql-server-migration-assistant-for-access-accesstosql.md)|SSMA をインストールするための前提条件、SSMA をインストールおよびライセンスする手順、および最新バージョンへのリンクを示します。|  
|[アクセスアクセス&#40;用の SQL Server Migration Assistant によるはじめに&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|SSMA とそのユーザーインターフェイスについて説明します。|  
|[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)|Access データベースを準備して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure に変換する方法について説明します。|  
|[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)|変換プロセスの概要と、プロセスの各手順に関する詳細情報について説明します。|  
|[Access アプリケーションの SQL Server へのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で既存の Access アプリケーションを使用する方法について説明します。|  
|[ユーザー インターフェイス リファレンス](user-interface-reference-accesstosql.md)|SSMA ダイアログボックスのドキュメントが含まれています。|  
|[SSMA for Access コンソールの操作](working-with-ssma-for-access-console-accesstosql.md)|SSMA コンソールアプリケーションに関するドキュメントが含まれています。|  
|[SSMA のアクセス権の取得](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|追加のサポートを受ける方法について説明します。|  
