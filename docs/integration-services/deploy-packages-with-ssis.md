---
title: SSIS によるパッケージの配置 | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b873c611c0e997c5033c2efed341f93e0ec5aa5e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290727"
---
# <a name="deploy-packages-with-ssis"></a>SSIS によるパッケージの配置

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージを別のコンピューターへ簡単に配置できるツールが用意されています。 この配置ツールでは、パッケージに必要な構成やファイルなどの依存関係を管理することもできます。 このチュートリアルでは、これらのツールを使用して、ターゲット コンピューターにパッケージとその依存関係をインストールする方法を学習します。    
    
まず、配置の準備を行います。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で新しい [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] プロジェクトを作成し、既存のパッケージとデータ ファイルをプロジェクトに追加します。 新しいパッケージを最初から作成するのではなく、このチュートリアル用に作成された既存のパッケージで作業を行います。 このチュートリアルでパッケージの機能は変更しませんが、パッケージをプロジェクトに追加した後、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでパッケージを開いて内容を確認しておくことをお勧めします。 パッケージの内容を確認すると、ログ ファイルなどのパッケージの依存関係やその他の便利な機能について理解できます。    
    
また、配置の前に、パッケージが構成を使用するように更新しておきます。 構成によって、実行時にパッケージやパッケージ オブジェクトのプロパティを更新できます。 このチュートリアルでは、構成を使用して、ログ ファイルとテキスト ファイルの接続文字列、およびパッケージが使用する XML ファイルと XSD ファイルの場所を更新します。 詳細については、「 [パッケージ構成](../integration-services/packages/package-configurations.md) 」および「 [パッケージ構成を作成する](../integration-services/packages/create-package-configurations.md)」を参照してください。    
    
[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]でパッケージが正常に実行されることを確認したら、パッケージのインストールに使用する配置バンドルを作成します。 配置バンドルは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに追加したパッケージ ファイルとその他の項目、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] に自動的に含まれるパッケージの依存関係、および構築した配置ユーティリティから構成されます。 詳細については、「 [配置ユーティリティを作成する](../integration-services/packages/create-a-deployment-utility.md)」を参照してください。    
    
配置バンドルをターゲット コンピューターにコピーし、パッケージ インストール ウィザードを実行して、パッケージとパッケージの依存関係をインストールします。 パッケージは msdb SQL Server データベースにインストールされ、サポート ファイルと補助ファイルはファイル システムにインストールされます。 配置されたパッケージは構成を使用するので、新しい値に更新して、パッケージを新しい環境で正常に実行できるようにします。    
    
最後に、パッケージ実行ユーティリティを使用して、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でパッケージを実行します。    
    
このチュートリアルの目的は、実際の配置で発生する可能性のある複雑な問題をシミュレーションすることです。 ただし、パッケージを別のコンピューターに配置できない場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のローカル インスタンスの msdb データベースにパッケージをインストールし、パッケージを同じインスタンスの [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] から実行して、このチュートリアルを行うこともできます。    

**このチュートリアルの推定所要時間:** 2 時間

## <a name="what-you-learn"></a>学習する内容    
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の新しいツール、コントロール、機能などに慣れる最良の方法は、実際に使ってみることです。 このチュートリアルでは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成し、パッケージとその他の必要なファイルをプロジェクトに追加する手順を紹介します。 プロジェクトが完成したら、配置バンドルを作成し、バンドルを目的のコンピューターにコピーして、そのコンピューターにパッケージをインストールします。    
    
## <a name="prerequisites"></a>Prerequisites    
このチュートリアルは、ファイル システムの基本的な操作は理解していても、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]の新機能はほとんど使用したことがないユーザーを対象にしています。 このチュートリアルで使用する基本的な [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の概念をよく理解するためには、最初に [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] チュートリアルの「[SSIS ETL パッケージを作成する方法](../integration-services/ssis-how-to-create-an-etl-package.md)」を終えることをお勧めします。    
    
### <a name="on-the-source-computer"></a>ソース コンピューターの場合

配置バンドルを作成するコンピューターには、**次のコンポーネントがインストールされている必要があります。**

- SQL Server : ([SQL Server のダウンロード](https://www.microsoft.com/sql-server/sql-server-downloads)に関するページから無料の Evaluation Edition または Developer Edition の SQL Server をダウンロードします)。

- サンプル データ、完成したパッケージ、構成、Readme。 サンプル データとレッスン パッケージを ZIP ファイルとしてダウンロードする場合は、[SQL Server Integration Services のチュートリアル ファイル](https://www.microsoft.com/download/details.aspx?id=56827)に関するページを参照してください。 Zip ファイル内のファイルのほとんどは、意図しない変更を回避するために読み取り専用になっています。 ファイルに出力を書き込んだり、ファイルを変更したりするには、ファイルのプロパティで読み取り専用属性をオフにする必要がある場合があります。

-   **AdventureWorks2014** サンプル データベース。 **AdventureWorks2014** データベースをダウンロードするには、[AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)から `AdventureWorks2014.bak` をダウンロードし、バックアップを復元します。  

-   AdventureWorks データベースでテーブルを作成および削除するための権限が必要です。
    
-   [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)。    
    
### <a name="on-the-destination-computer"></a>配置先コンピューターの場合

パッケージを配置するコンピューターには、 **次のコンポーネントがインストールされている必要があります。**    
    
- SQL Server : ([SQL Server のダウンロード](https://www.microsoft.com/sql-server/sql-server-downloads)に関するページから無料の Evaluation Edition または Developer Edition の SQL Server をダウンロードします)。

- サンプル データ、完成したパッケージ、構成、Readme。 サンプル データとレッスン パッケージを ZIP ファイルとしてダウンロードする場合は、[SQL Server Integration Services のチュートリアル ファイル](https://www.microsoft.com/download/details.aspx?id=56827)に関するページを参照してください。 Zip ファイル内のファイルのほとんどは、意図しない変更を回避するために読み取り専用になっています。 ファイルに出力を書き込んだり、ファイルを変更したりするには、ファイルのプロパティで読み取り専用属性をオフにする必要がある場合があります。

-   **AdventureWorks2014** サンプル データベース。 **AdventureWorks2014** データベースをダウンロードするには、[AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)から `AdventureWorks2014.bak` をダウンロードし、バックアップを復元します。  
    
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。    
    
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]」を参照してください。 SSIS をインストールする場合は、「[Integration Services のインストール](install-windows/install-integration-services.md)」を参照してください。
    
-   AdventureWorks データベースでテーブルを作成および削除するための権限と、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で SSIS パッケージを実行するための権限が必要です。    
    
-   `sysssispackages` [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] システム データベースの `msdb` テーブルの読み取り権限と書き込み権限が必要です。    
    
配置バンドルを作成したコンピューターにパッケージを配置する場合は、そのコンピューターが配置元コンピューターと配置先コンピューターの両方の必要条件を満たしている必要があります。    
        
## <a name="lessons-in-this-tutorial"></a>このチュートリアルで行うレッスン    
[レッスン 1:配置バンドルを作成する準備](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)    
このレッスンでは、新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成し、パッケージとその他の必要なファイルをプロジェクトに追加して、ETL ソリューションを配置する準備を行います。    
    
[レッスン 2:SSIS での配置バンドルの作成](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)    
このレッスンでは、配置ユーティリティを構築し、配置バンドルに必要なファイルが含まれていることを確認します。    
    
[レッスン 3:SSIS パッケージのインストール](../integration-services/lesson-3-install-ssis-packages.md)    
このレッスンでは、配置バンドルをターゲット コンピューターにコピーし、パッケージをインストールして、パッケージを実行します。    
    

