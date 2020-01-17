---
title: Microsoft Connector 1.1 for SAP BW のインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e43a45f9b21e631638dec43a8a126b4f007429d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767754"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>Microsoft Connector 1.1 for SAP BW のインストール
  インストールする、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW およびそのドキュメントをダウンロードして、SQL Server 機能パック Web ページから、Windows インストーラー パッケージを実行します。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
## <a name="required-sap-files"></a>必要な SAP のファイル  
 使用する、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW では、されませんが、ローカル コンピューターに、SAP フロント エンド ソフトウェア (SAP GUI) をインストールします。  
  
 ただし、SAP の .NET コネクタ ファイルである librfc32.dll を、Windows フォルダー内の system サブフォルダーにコピーする必要があります (通常は、このフォルダーの場所は、 **C:\Windows\system32**です)。  
  
## <a name="considerations-for-64-bit-computers"></a>64 ビット コンピューターに関する注意事項  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW の 64 ビット バージョンを完全にサポートする[!INCLUDE[msCoName](../includes/msconame-md.md)]Windows。 64 ビット コンピューターで、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW に次の追加要件。  
  
-   任意の 64 ビット Windows オペレーティング システムで、パッケージを 64 ビット モードで実行するには、SAP GUI ファイルの 64 ビット バージョンである librfc32.dll を、Windows フォルダー内の **system32** フォルダーにコピーします (通常は、このファイルの場所は、 **C:\Windows\system32**です)。  
  
-   任意の 64 ビット Windows オペレーティング システムで、パッケージを 32 ビット モードで実行するには、SAP GUI ファイルである librfc32.dll を、Windows フォルダー内の **SysWow64** フォルダーにコピーします (通常は、このフォルダーの場所は、 **C:\Windows\SysWow64**です)。  
  
  
