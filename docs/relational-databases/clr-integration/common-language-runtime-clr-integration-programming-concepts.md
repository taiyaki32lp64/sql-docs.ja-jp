---
title: 共通言語ランタイム (CLR) プログラミング
description: 共通言語ランタイム (CLR) プログラミングに関する記事へのリンク
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
ms.openlocfilehash: c314745122f0735b2b26ac2bb021f20f637b2a28
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75256189"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>CLR (共通言語ランタイム) 統合のプログラミング概念
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、.NET Framework for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows の CLR (共通言語ランタイム) コンポーネントが統合されました。 つまり、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET や [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# などの .NET Framework 言語を使用して、ストアド プロシージャ、トリガー、ユーザー定義型、ユーザー定義関数、ユーザー定義集計、およびストリーミング テーブル値関数を記述できるようになります。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] における CLR プログラミングのためのコア機能は、Microsoft.SqlServer.Server 名前空間に存在します。 ただし、Microsoft.SqlServer.Server 名前空間については、.NET Framework SDK ドキュメントをご覧ください。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックには、このドキュメントが含まれていません。  
  
> [!IMPORTANT]  
>  既定では、.NET Framework は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と共にインストールされますが、.NET Framework SDK はインストールされません。 SDK がコンピューターにインストールされていない場合やオンライン ブックに含まれていない場合は、このセクションにある SDK のコンテンツへのリンクが機能しません。 .NET Framework SDK をインストールしてください。 インストールが完了したら、「 [.NET FRAMEWORK sdk のインストール](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)」の手順に従って、Sdk をオンラインブックコレクションと目次に追加します。  
  
> [!NOTE]  
>  Clr ユーザー関数などの CLR 機能は、Azure SQL Database ではサポートされて*いません*。  
  
 次の表に、このセクションの各トピックの一覧を示します。  
  
 [CLR&#41; 統合の概要 &#40;共通言語ランタイム](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
 CLR の概要を簡単に紹介し、このテクノロジが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用される方法と理由について説明します。 CLR を使用してデータベース オブジェクトを作成する利点についても説明します。  
  
 [アセンブリ &#40;データベースエンジン&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではなく、[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework CLR (共通言語ランタイム) がサポートするマネージド コード言語の 1 つを使用して作成された関数、ストアド プロシージャ、トリガー、ユーザー定義集計、ユーザー定義型の配置に、[!INCLUDE[tsql](../../includes/tsql-md.md)] でアセンブリがどのように使用されるかについて説明します。  
  
 [CLR&#41; 統合 &#40;共通言語ランタイムを使用したデータベースオブジェクトの構築](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 CLR を使用して作成できるオブジェクトの種類について説明し、CLR データベース オブジェクトの作成要件を確認します。  
  
 [CLR データベース オブジェクトからのデータ アクセス](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに格納されているデータに CLR ルーチンからアクセスする方法について説明します。  
  
 [CLR 統合のセキュリティ](../../relational-databases/clr-integration/security/clr-integration-security.md)  
 CLR 統合のセキュリティ モデルについて説明します。  
  
 [CLR データベース オブジェクトのデバッグ](../../relational-databases/clr-integration/debugging-clr-database-objects.md)  
 CLR データベース オブジェクトをデバッグする場合の制限事項と要件について説明します。  
  
 [CLR データベース オブジェクトの配置](../../relational-databases/clr-integration/deploying-clr-database-objects.md)  
 実稼働サーバーへのアセンブリの配置について説明します。  
  
 [CLR 統合アセンブリの管理](../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
 CLR 統合のアセンブリの作成および削除方法について説明します。  
  
 [マネージデータベースオブジェクトの監視とトラブルシューティング](../../relational-databases/clr-integration/monitoring-and-troubleshooting-managed-database-objects.md)  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行されるマネージド データベース オブジェクトとアセンブリの監視およびトラブルシューティングに使用できるツールに関する情報を提供します。  
  
 [CLR&#41; 統合 &#40;共通言語ランタイムの使用シナリオと例](https://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
 CLR オブジェクトを使用する使用シナリオとコード サンプルについて説明します。  
  
## <a name="see-also"></a>参照  
 [アセンブリ &#40;データベースエンジン&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [.NET Framework SDK のインストール](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
