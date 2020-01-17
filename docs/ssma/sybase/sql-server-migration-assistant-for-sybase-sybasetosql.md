---
title: Sybase の SQL Server Migration Assistant (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59e63eac-8a7e-4d54-be1c-0633a9bf510d
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 3913ae22155ca5e560db7fee946df0f8062a23b9
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252156"
---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase の SQL Server Migration Assistant (SybaseToSQL)

[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for Sybase Adaptive Server Enterprise (ASE) は、ASE データベースを [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 (Windows および Linux の場合)、[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2019 (Windows と linux の場合)、または [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL Database に移行するためのツールです。 SSMA for Sybase は、ASE データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースオブジェクトに変換し、それらのオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に作成した後、ASE から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database にデータを移行します。
  
このドキュメントでは、SSMA for Sybase について説明します。また、ASE データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database に移行する手順と、移行後に発生する可能性がある問題についての情報を示します。 詳細については、次の記事を参照してください。  
  
## <a name="contents"></a>目次  
  
|セクション|[説明]|
|-----------|---------------|
|[SSMA for Sybase &#40;sybasetosql の新機能&#41;](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|SSMA リリースに対する変更の一覧を示します。|  
|[SSMA for Sybase &#40;sybasetosql のインストール&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|SSMA for Sybase クライアントおよび必要なコンポーネントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを実行しているコンピューターにインストールするための前提条件と手順を説明した記事が含まれています。|  
|[SSMA for Sybase &#40;sybasetosql を使用したはじめに&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|ユーザーインターフェイス、プロジェクト、および構成オプションについて説明します。|  
|[SQL Server への Sybase ASE データベースの移行-Azure &#40;sql DB sybasetosql&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|変換プロセスの概要と、プロセスの各手順に関する詳細情報について説明します。|  
|[ユーザーインターフェイスリファレンス&#40;sybasetosql&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)|SSMA for Sybase のダイアログボックスのドキュメントが含まれています。|  
|[SSMA for Sybase コンソールの使用](working-with-ssma-for-sybase-console-sybasetosql.md)|SSMA コンソールアプリケーションに関するドキュメントが含まれています。|  
|[SSMA for Sybase のサポートを取得する](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|追加のサポートを受ける方法について説明します。|  
