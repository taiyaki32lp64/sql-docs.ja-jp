---
title: Attunity の Change Data Capture Service for Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 22ec8a5c-9550-4d38-8a4a-485ec3e53ea8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 78be5b59dd2397ef361a981219989d27d88b5ae2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294815"
---
# <a name="change-data-capture-service-for-oracle-by-attunity"></a>Attunity の Change Data Capture Service for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC Service for Oracle は、Oracle トランザクション ログをスキャンして目的の Oracle テーブルに対する変更を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変更テーブルにキャプチャする Windows サービスです。 Oracle からキャプチャされた変更が格納される SQL 変更テーブルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネイティブの変更データ キャプチャ機能で使用される変更テーブルと同じ種類のテーブルです。 そのため、このような変更も、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに対して行われた変更を使用する場合と同様に簡単に使用できます。  
  
## <a name="installation"></a>インストール  

Microsoft Change Data Capture Designer および Service for Oracle by Attunity for Microsoft SQL Server 2016 は、SQL Server 2016 Feature Pack に含まれています。 [SQL Server 2016 Feature Pack の Web ページ](https://go.microsoft.com/fwlink/?LinkId=746297)から、Feature Pack のコンポーネントをダウンロードします。
  
 CDC Service for Oracle は、キャプチャするソース Oracle データベースと、対象の CDC データベースが存在する対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにアクセスできる、サポートされているすべての Windows コンピューターにインストールできます。 CDC Service では、Oracle データベースまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのローカル インストールは必要なく、サポートされるクライアントのみが必要です。 必要なデータベース コンポーネントのインストール場所の詳細については、「 **データベースの前提条件** 」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC Service for Oracle をインストールすると、サービス構成 UI とサービス プログラムが選択した場所に配置されます。 CDC Service for Oracle は、Oracle CDC Service 構成コンソールを使用して個別に構成します。 Oracle CDC Service の構成の詳細については、「 [Change Data Capture Service for Oracle by Attunity の F1 ヘルプ](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md)」を参照してください。  
  
 CDC Service for Oracle は、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client がインストールされたサポートされているすべての Windows コンピューターにインストールできます。対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされている同じコンピューターにインストールする必要はありません。  
  
## <a name="supported-windows-environments"></a>サポートされている Windows 環境  
 Change Data Capture Service for Oracle by Attunity は、次の Windows 環境で実行できます。  
  
-   Windows 8 および 8.1  
-   Windows 10  
-   Windows Server 2012 および 2012 R2
-   Windows Server 2016
  
## <a name="database-prerequisites"></a>データベースの前提条件  
 CDC Service for Oracle を使用するには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client Oracle ソフトウェアをインストールする必要があります。 これは、Oracle CDC Service をインストールする前に Oracle から入手してインストールする必要がある必須ソフトウェアです。 さらに、SQL Server セットアップを使用して SQL Server ODBC クライアントをインストールする必要があります。  
  
 CDC Service for Oracle では、次のバージョンがサポートされています。  
  
### <a name="source-oracle-database"></a>ソース Oracle データベース  
  
-   Oracle Database 10 g リリース 2
-   Oracle Database 11g リリース 1 およびリリース 2
-   クラシック インストールでの Oracle Database 12c (マルチテナント インストールはサポートされていません)  
  
### <a name="target-sql-server-database"></a>対象の SQL Server データベース  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
## <a name="running-the-installation-program"></a>インストール プログラムの実行  
 CDC Service for Oracle をインストールするには、使用している Windows プラットフォーム (32/64 ビット) 用のインストール ウィザードを開き、画面の指示に従います。  
  
## <a name="uninstalling-change-data-capture-service-for-oracle-by-attunity"></a>Change Data Capture Service for Oracle by Attunity のアンインストール  
 CDC Service for Oracle をアンインストールするには、コントロール パネルの [プログラムと機能] を使用します。  
  
 CDC Service をアンインストールしても、作成した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースは削除されません。 ツールを完全に削除するには、使用していた対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで作成した MSXDBCDC データベースと特定の CDC データベースを削除する必要があります。  
  
 CDC Service ソフトウェアをアンインストールしてから別のコンピューターにインストールする場合は、次の定義を指定するだけで済みます。  
  
-   サービス アカウント  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続文字列と資格情報  
  
-   マスター パスワード  
  
 他のすべての定義は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に格納されており、別のコンピューター上の以前のインストール環境から取得できます。  
  
## <a name="in-this-documentation"></a>このドキュメントの内容  
  
-   [Change Data Capture Service for Oracle by Attunity のシステム アーキテクチャ](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-system-architecture.md)  
  
-   [Oracle CDC Service](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
-   [Change Data Capture Service for Oracle by Attunity の F1 ヘルプ](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md)  
  
-   [Change Data Capture Service for Oracle by Attunity 操作ガイド](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-how-to-guide.md)  
  
## <a name="see-also"></a>参照  
 [Oracle CDC Service を使用する](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
  
