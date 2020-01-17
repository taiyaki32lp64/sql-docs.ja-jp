---
title: SAP BW 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
f1_keywords:
- sql13.dts.designer.sapbwconnectionmanager.f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0f0ebc393c48562c5fcd783b4c056aa218e8ffaa
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298477"
---
# <a name="sap-bw-connection-manager"></a>SAP BW 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SAP BW 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の接続マネージャー コンポーネントです。 したがって、SAP BW 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の変換元と変換先コンポーネントが必要とする SAP Netweaver BW version 7 システムへの接続を提供します ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW パッケージの一部の SAP BW 変換元と変換先は、SAP BW 接続マネージャーを使用する唯一の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントです)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 SAP BW 接続マネージャーをパッケージに追加する場合、接続マネージャーの **ConnectionManagerType** プロパティを **SAPBI**に設定します。  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>SAP BW 接続マネージャーの構成  
 SAP BW 接続マネージャーは、次の方法で構成できます。  
  
-   接続のクライアント、ユーザー名、パスワード、および言語を指定します。  
  
-   1 つのアプリケーション サーバーまたは負荷分散されたサーバーのグループに接続するかどうかを選択します。  
  
-   単一のアプリケーション サーバーのホストとシステム数を指定するか、負荷分散されたサーバー グループのメッセージ サーバー、グループ、および SID を指定します。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW のコンポーネントに対する RFC 関数呼び出しのカスタム ログを有効にします (このログは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージで有効にできる、省略可能なログとは異なります)。RFC 関数呼び出しのログを有効にするには、RFC の各関数呼び出しの前後に作成されるログ ファイルを格納するディレクトリを指定します (このログ機能は、XML 形式で多くのログ ファイルを作成します。 これらのログ ファイルには転送されるデータのすべての行も含まれるため、大量のディスク領域を消費する可能性があります)。ログ ディレクトリを選択しないと、ログ記録は有効になりません。  
  
    > [!IMPORTANT]  
    >  転送されるデータに機密情報が含まれている場合、ログ ファイルには機密情報も含まれることになります。  
  
-   入力した値を使用して接続をテストします。  
  
 接続マネージャーを構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 SAP BW 接続マネージャー、変換元、変換先の構成および使用方法の詳細については、ホワイト ペーパー「 [SAP BI 7.0 を使用した SQL Server 2008 Integration Services](https://go.microsoft.com/fwlink/?LinkID=137090)」を参照してください。 このホワイト ペーパーには、SAP BW で必要なオブジェクトの構成方法についても説明されています。  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>SSIS デザイナーを使用してソースを構成する  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できる、SAP BW マネージャーのプロパティの詳細については、次のトピックを参照してください。  
  
-   [SAP BW 接続マネージャー エディター](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md)  
  
## <a name="sap-bw-connection-manager-editor"></a>SAP BW 接続マネージャー エディター
  SAP Netweaver BW Version 7 システムへの接続に使用するプロパティを指定するには、 **[SAP BW 接続マネージャー エディター]** を使用します。  
  
 SAP BW 接続マネージャーは、SAP Netweaver BW Version 7 システムに SAP BW 変換元または変換先を接続します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 接続マネージャーの詳細については、「 [SAP BW 接続マネージャー](../../integration-services/connection-manager/sap-bw-connection-manager.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **SAP BW 接続マネージャー エディターを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 接続マネージャーが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[制御フロー]** タブ上にある [接続マネージャー] 領域で、次のいずれかの手順を実行します。  
  
    -   [SAP BW 接続マネージャー] をダブルクリックします。  
  
         \- または -  
  
    -   [SAP BW 接続マネージャー] を右クリックし、 **[編集]** を選択します。  
  
### <a name="options"></a>オプション  
  
> [!NOTE]  
>  接続マネージャーを構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **クライアント**  
 システムのクライアント数を指定します。  
  
 **言語**  
 システムが使用する言語を指定します。 たとえば、英語の場合は、 **[EN]** を指定します。  
  
 **User name**  
 システムへの接続に使用するユーザー名を指定します。  
  
 **パスワード**  
 そのユーザー名のパスワードを指定します。  
  
 **単一のアプリケーション サーバーを使用する**  
 単一のアプリケーション サーバーに接続します。  
  
 負荷分散されたサーバーのグループに接続するには、 **[負荷分散を使用する]** オプションを使用します。  
  
 **ホスト**  
 単一のアプリケーション サーバーに接続する場合、ホスト名を指定します。  
  
> [!NOTE]  
>  このオプションは、 **[単一のアプリケーション サーバーを使用する]** オプションを選択している場合にのみ使用できます。  
  
 **システム数**  
 単一のアプリケーション サーバーに接続する場合、システム数を指定します。  
  
> [!NOTE]  
>  このオプションは、 **[単一のアプリケーション サーバーを使用する]** オプションを選択している場合にのみ使用できます。  
  
 **[負荷分散を使用する]**  
 負荷分散されたサーバーのグループに接続します。  
  
 単一のアプリケーション サーバーに接続するには、 **[単一のアプリケーション サーバーを使用する]** オプションを使用してください。  
  
 **メッセージ サーバー**  
 負荷分散されたサーバーのグループに接続する場合は、メッセージ サーバーの名前を指定します。  
  
> [!NOTE]  
>  このオプションは、 **[負荷分散を使用する]** オプションを選択している場合にのみ使用できます。  
  
 **[グループ]**  
 負荷分散されたサーバーのグループに接続する場合は、サーバー グループの名前を指定します。  
  
> [!NOTE]  
>  このオプションは、 **[負荷分散を使用する]** オプションを選択している場合にのみ使用できます。  
  
 **SID**  
 負荷分散されたサーバーのグループに接続する場合は、接続のシステム ID を指定します。  
  
> [!NOTE]  
>  このオプションは、 **[負荷分散を使用する]** オプションを選択している場合にのみ使用できます。  
  
 **ログ ディレクトリ**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW のコンポーネントに対するログを有効にします。  
  
 ログを有効にするには、RFC の各関数呼び出しの前後に作成されたログ ファイルのディレクトリを指定します (このログ機能は、XML 形式で多くのログ ファイルを作成します。 これらのログ ファイルには転送されるデータのすべての行も含まれるため、大量のディスク領域を消費する可能性があります)。  
  
> [!IMPORTANT]  
>  転送されるデータに機密情報が含まれている場合、ログ ファイルには機密情報も含まれることになります。  
  
 ログ ディレクトリを指定するには、ディレクトリ パスに手動で入力するか、 **[参照]** をクリックし、ログ ディレクトリを参照します。  
  
 ログ ディレクトリを選択しないと、ログ記録は有効になりません。  
  
 **[参照]**  
 ログ ディレクトリのフォルダーを参照して選択します。  
  
 **[接続テスト]**  
 指定した値を使用して接続をテストします。 **[接続テスト]** をクリックすると、接続が成功または失敗したかを示すメッセージ ボックスが表示されます。  
  
## <a name="see-also"></a>参照  
 [Microsoft Connector for SAP BW のコンポーネント](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
