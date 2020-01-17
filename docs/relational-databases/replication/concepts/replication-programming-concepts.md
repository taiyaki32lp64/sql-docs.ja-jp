---
title: レプリケーションのプログラミング概念 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- replication [SQL Server], planning
- programming [SQL Server replication], planning
- programming [SQL Server replication]
ms.assetid: 2cd846e7-5bf3-4144-8772-703c4f439a2a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: af2e1ff51864215d3f5709463ab8d49e6737747e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768756"
---
# <a name="replication-programming-concepts"></a>レプリケーションのプログラミング概念
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  レプリケーション機能を利用するアプリケーションを開発する前に、次に示す一般的な計画手順を実行してください。  
  
1.  レプリケーション トポロジを定義します。  
  
2.  アプリケーションの機能を定義します。  
  
3.  セキュリティを計画します。  
  
4.  開発環境を選択します。  
  
5.  適切なレプリケーション プログラミング インターフェイスを選択します。  
  
 以下に、この手順の詳細を説明します。 計画のプロセスについてわかりやすく説明するために、例も示します。  
  
## <a name="defining-the-replication-topology"></a>レプリケーション トポロジの定義  
 レプリケーションのプログラミングの最初の手順は、アプリケーションのレプリケーション トポロジを定義することです。 既存のサブスクライバー上のデータにアクセスするクライアント アプリケーションなど、既存のレプリケーション トポロジを使用するアプリケーションを作成する場合は、次の手順に進んでください。  
  
> [!NOTE]  
>  レプリケーション トポロジの配置だけがアプリケーションの目的である場合もあります。  
  
 レプリケーション トポロジの定義は、次のような多くの要因によって決まります。  
  
-   レプリケートされたデータの更新が必要か、まただれが更新するか。  
  
-   データ ディストリビューションでは、関連する一貫性、自律性、待機時間を必要とするか。  
  
-   ビジネス ユーザー、技術的なインフラストラクチャ、ネットワークとセキュリティ、データ特性などのレプリケーション環境。  
  
-   レプリケーションの種類とレプリケーション オプション。  
  
-   レプリケーション トポロジと、そのレプリケーションの種類との対応。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーションを初めて使用する場合は、「[レプリケーションの種類](../../../relational-databases/replication/types-of-replication.md)」を参照してください。  
  
## <a name="defining-application-functionality"></a>アプリケーションの機能の定義  
 レプリケーション トポロジを定義した後で、アプリケーションに備える機能を決定します。 サブスクリプションをアプリケーションに同期させるスクリプトから、レプリケーションを構成するためのユーザー インターフェイスを備えたアプリケーションまで、幅広い機能を定義できます。 レプリケーションでは次の一般的なプログラミング作業がサポートされます。  
  
-   レプリケーションのセットアップ  
  
-   サブスクライバーの同期  
  
-   レプリケーション トポロジの保持  
  
-   レプリケーション トポロジの監視  
  
-   レプリケーションのトラブルシューティング  
  
 レプリケーション機能と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の他の機能を組み合わせることで、アプリケーションを拡張することもよく行われます。 次の表に、レプリケーション アプリケーションで提供できる拡張機能の一部を示します。  
  
|機能|例|  
|-------------------|-------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) を使用したサーバー管理|管理者がレプリケーション トポロジ内でデータベースをパブリッシャーとしてアタッチし、構成できるアプリケーション|  
|ADO.NET を使用したデータ アクセス|ユーザーがオフライン時にローカル サブスクライバー データベース内のレプリケート済み販売データにプログラムからアクセスして変更でき、さらにボタンをクリックすることでプル サブスクリプションに接続して同期できるアプリケーション|  
  
## <a name="planning-for-security"></a>セキュリティの計画  
 セキュリティはどのようなアプリケーションでも重要です。セキュリティの計画は、コードを作成する前に完成しておく必要があります。 アプリケーションのセキュリティは、データベースのセキュリティ保護、レプリケーションのセキュリティ保護、安全なコードの作成の 3 つに大きく分類されます。  
  
 セキュリティの詳細については、次のトピックで解説します。  
  
-   [レプリケーションのセキュリティ設定の表示および変更](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
-   [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
## <a name="choosing-a-development-environment"></a>開発環境の選択  
 レプリケーション アプリケーションの開発時に検討する基本開発環境は、3 種類あります。 どの開発環境からもほぼ同じレプリケーション機能を利用できますが、いくつか例外があります。 レプリケーション アプリケーションは、次の環境で開発できます。  
  
-   **マネージド コード**  
  
     [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] プログラミングと .NET 共通言語ランタイム (CLR) を利用できる、オブジェクト指向開発環境です。 マネージド コードは、.NET 開発と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アプリケーションのどちらにも推奨されるプログラミング環境です。 マネージド レプリケーション インターフェイスを利用することで、[!INCLUDE[tsql](../../../includes/tsql-md.md)] がわからなくてもオブジェクト指向の方法でレプリケーション管理をプログラミングできます。さらに、スクリプトから使用できないレプリケーション エージェントを実行する場合に、コールバック機能も提供できます。 マネージド コードは、再利用可能なコンポーネントおよびユーザー インターフェイス アプリケーションの開発に最適な環境です。  
  
-   **スクリプトの作成**  
  
     一連のコマンドを [!INCLUDE[tsql](../../../includes/tsql-md.md)] スクリプトでレプリケーション システムのストアド プロシージャとして実行するか、バッチ ファイル内のコマンドを実行する単純なアプリケーションです。 プロセス内で管理される [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プロバイダーを使用して、管理対象の環境でスクリプトを実行できますが、管理対象のレプリケーション インターフェイスを使用することで同じ機能を利用できます。さらに、コールバック機能も提供されます。 スクリプトは、たとえばレプリケーション サーバーのインストールなど、数回のみ実行されるタスクを実行する場合や、コールバック機能が不要な場合に最適な環境です。  
  
-   **ネイティブ コード**  
  
     コードが CLR によって管理されない、システム オブジェクトや COM オブジェクトへの直接アクセスを利用するオブジェクト指向開発環境です。 ネイティブ コード レプリケーション インターフェイスは、非推奨または廃止になりました。 詳細については、「[SQL Server レプリケーションの非推奨の機能](../../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)」または「[レプリケーションの旧バージョンとの互換性](../../../relational-databases/replication/replication-backward-compatibility.md)」を参照してください。  
  
## <a name="choose-the-appropriate-replication-programming-interface"></a>適切なレプリケーション プログラミング インターフェイスの選択  
 計画の最後の手順は、選択した開発環境で目的のレプリケーション機能を実装するためのレプリケーション プログラミング インターフェイスを適切に選択することです。 次の表に、使用できるレプリケーション プログラミング インターフェイスを示します。  
  
|インターフェイス|環境|使用法|  
|---------------|-----------------|----------|  
|[レプリケーション管理オブジェクトの概念](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)|マネージド コード|管理、監視、同期|  
|<xref:Microsoft.SqlServer.Replication>|マネージド コード|同期|  
|<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|マネージド コード|カスタム ロジックとマージ同期プロセスを統合するためのビジネス ロジック ハンドラーの作成|  
|[レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|スクリプトの作成|管理と監視。|  
|[Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)|スクリプトの作成|同期|  
  
## <a name="example"></a>例  
 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] では、データを世界中の 200 人の販売担当者にパブリッシュする必要があります。 販売担当者は頻繁に出張するため、ラップトップ コンピューターや携帯情報端末 (PDA) を使用して顧客データを変更したり、新しい発注を追加したりする必要があります。 販売担当者がラップトップ コンピューターをネットワークに接続したときに、このような変更をパブリッシャーと同期する必要があります。  
  
 このアプリケーションの場合、計画手順は次のようになります。  
  
1.  このアプリケーションのレプリケーション トポロジは既に存在しています。 しかし、クライアントで新しいプル サブスクリプションを作成する必要があります。 パブリケーションではパラメーター化されたフィルターを使用して、一意なデータのセットを各販売担当者にレプリケートする必要があります。  
  
2.  販売アプリケーションに必要な一般的なデータ アクセスに加えて、このアプリケーションでは販売担当者が必要なときにボタンをクリックしてプル サブスクリプションを同期できるようにする必要があります。 さらに、販売担当者がこのアプリケーションをインストールして実行するため、クライアント側でサブスクリプションを構成し、初期スナップショットを適用できる必要があります。 場合によっては、このアプリケーションは Windows で提供されているインフラストラクチャを利用してワイヤレス接続を探し、接続が検出された場合はサブスクリプションを自動的に同期します。  
  
3.  パブリッシャーに接続するときには、Windows 認証と仮想プライベート ネットワークの使用を含む、レプリケーションのセキュリティ ガイドラインすべてに従います。 Web 同期を実行する場合は、SSL (Secure Sockets Layer) 接続を使用します。 詳細については、「[Web 同期の構成](../../../relational-databases/replication/configure-web-synchronization.md)」を参照してください。  
  
4.  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] の機能を利用するには、マネージド コード言語を使用してアプリケーションを開発します。  
  
5.  このような要件に基づき、このアプリケーションに必要なレプリケーション機能はレプリケーション管理オブジェクト (RMO) 管理インターフェイスによってすべて提供できます。  
  
 この例のシナリオは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にダウンロード可能な AdventureWorks サンプル アプリケーションで実装されています。  
  
  
