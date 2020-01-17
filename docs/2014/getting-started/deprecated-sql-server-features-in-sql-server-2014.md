---
title: 非推奨の SQL Server SQL Server 2014 | の機能Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44fbab98aa017be66cd4dc369a713f44e8d248d5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228217"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 の非推奨の SQL Server 機能
  このトピックでは、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] でまだ使用できるものの、非推奨となった機能について説明します。 これらの機能は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の今後のリリースで削除される予定です。 非推奨の機能を新しいアプリケーションで使用しないでください。  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の次のバージョンでサポートされない機能  
 以下の [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 機能は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の次のバージョンではサポートされません。 新規の開発作業ではこれらの機能を使用しないようにし、現在これらの機能を使用しているアプリケーションはできるだけ早く修正してください。 機能名の列は、トレース イベントには ObjectName として表示され、パフォーマンス カウンターおよび sys.dm_os_performance_counters には instance_name として表示されます。 機能 ID は ObjectId としてトレース イベントに表示されます。  
  
|Category|非推奨の機能|代替|機能名|機能 ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|データ プログラミング|[soap_endpoints &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) または ASP.NET|ネイティブ XML Web サービス|22|  
|データ プログラミング|[endpoint_webmethods &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) または ASP.NET|ネイティブ XML Web サービス|23|  
  
### <a name="slipstream-functionality"></a>スリップストリーム機能  
 [製品の更新プログラム機能](/previous-versions/sql/sql-server-2012/hh231670(v=sql.110)?redirectedfrom=MSDN)は、PCU1 で[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]提供されていたスリップストリーム機能の拡張として SQL Server 2012 で導入されました。 SQL Server 2014 では、SQL Server のスリップストリームには、製品の更新機能を使用することをお勧めします。 そのため、元のスリップストリーム機能に関連付けられているコマンドラインパラメーター/*Pcusource*および/*CUSource*を使用することはできません。 これらのパラメーターは引き続き機能しますが、セットアップの将来の[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]リリースでは削除される可能性があります。 使用する推奨されるパラメーターは、元のスリップストリームパラメーター (/*Pcusource*および/*CUSource*) の機能を組み合わせた/*updatesource*です。  
  
 PCU1 で[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]提供されていたスリップストリーム機能の詳細については、https://go.microsoft.com/fwlink/?LinkId=219945)「 [SQL Server 更新プログラムのスリップストリーム](https://go.microsoft.com/fwlink/?LinkId=219945)(」を参照してください。  
 /*Updatesource*を使用して SQL Server ビルドをスリップストリームする方法については、次を参照してください。
 
 - [更新されたセットアップパッケージを使用して SQL Server 2012 セットアップにパッチを適用する方法 (UpdateSource を使用してスマートセットアップを取得する)](https://blogs.msdn.microsoft.com/jason_howell/2012/08/28/how-to-patch-sql-server-2012-setup-with-an-updated-setup-package-using-updatesource-to-get-a-smart-setup/)
 
 - [SQL Server 2012 セットアップがよりスマートになりました...](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2012-Setup-just-got-smarter-8230/ba-p/317440)
 
## <a name="see-also"></a>参照  
 [旧バージョンとの互換性](../../2014/getting-started/backward-compatibility.md)  
  
  
