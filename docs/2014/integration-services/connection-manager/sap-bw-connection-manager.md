---
title: SAP BW 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b3ee629cd7701d8b06351e8932daac57637b195e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833677"
---
# <a name="sap-bw-connection-manager"></a>SAP BW 接続マネージャー
  SAP BW 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の接続マネージャー コンポーネントです。 したがって、SAP BW 接続マネージャーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の変換元と変換先コンポーネントが必要とする SAP Netweaver BW version 7 システムへの接続を提供します ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW パッケージの一部の SAP BW 変換元と変換先は、SAP BW 接続マネージャーを使用する唯一の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントです)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 SAP BW 接続マネージャーをパッケージに追加する場合、接続マネージャーの `ConnectionManagerType` プロパティを `SAPBI` に設定します。  
  
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
  
-   [SAP BW 接続マネージャー エディター](../sap-bw-connection-manager-editor.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft Connector 1.1 for SAP BW のコンポーネント](../microsoft-connector-for-sap-bw-components.md)  
  
  
