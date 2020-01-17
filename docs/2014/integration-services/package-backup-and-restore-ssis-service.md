---
title: パッケージのバックアップと復元 (SSIS サービス) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, backup and restore
- backing up packages [Integration Services]
- packages [Integration Services], backup and restore
- SQL Server Integration Services packages, backup and restore
- restoring packages [Integration Services]
- Integration Services packages, backup and restore
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5c775393f7815084e8a79aae4be7f0974886f3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056929"
---
# <a name="package-backup-and-restore-ssis-service"></a>パッケージのバックアップと復元 (SSIS サービス)
    
> [!IMPORTANT]  
>  このトピックでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスについて説明します。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では、以前のリリースの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]との互換性を維持するために、このサービスをサポートしています。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]以降では、Integration Services サーバー上のパッケージなどのオブジェクトを管理できます。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージは、ファイル システムや [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] システム データベースの msdb に保存できます。 msdb に保存されたパッケージは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバックアップおよび復元機能を使用してバックアップおよび復元できます。  
  
 msdb データベースのバックアップおよび復元の詳細については、次のトピックのいずれかを参照してください。  
  
-   [SQL Server データベースのバックアップと復元](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [システム データベースのバックアップと復元 &#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージの管理に使用する **dtutil** コマンド プロンプト ユーティリティ (dtutil.exec) が付属しています。 詳細については、「 [dtutil ユーティリティ](dtutil-utility.md)」を参照してください。  
  
## <a name="configuration-files"></a>構成ファイル  
 パッケージに含まれるすべての構成ファイルはファイル システムに格納されています。 msdb データベースをバックアップするとき、これらのファイルはバックアップされません。したがって、msdb に保存されたパッケージの安全を確保するための計画の一部として、構成ファイルを定期的にバックアップする必要があります。 msdb データベースのバックアップに構成を含めるには、ファイル ベースの構成の代わりに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の構成の種類の使用を検討してください。  
  
## <a name="packages-stored-in-the-file-system"></a>ファイル システムに保存されたパッケージ  
 サーバーのファイル システムのバックアップ計画には、ファイル システムに保存されるパッケージのバックアップも含める必要があります。 既定で MsDtsSrvr.ini.xml という名前を持つ [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービス構成ファイルには、このサービスで監視されるサーバー上のフォルダーが定義されています。 これらのフォルダーを必ずバックアップしてください。 さらに、パッケージをサーバー上の他のフォルダーに格納している場合は、これらのフォルダーもバックアップに含める必要があります。  
  
  
