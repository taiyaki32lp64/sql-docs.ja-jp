---
title: Microsoft Connector for SAP BW のインストール | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 24c7f4c128998484be5d75d5db554de605feead7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284416"
---
# <a name="installing-the-microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW のインストール

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW for SQL Server 2016 は、SQL Server 2016 の Feature Pack のコンポーネントです。 Connector for SAP BW およびそのドキュメントをインストールするには、 [SQL Server 2016 Feature Pack Web ページ](https://go.microsoft.com/fwlink/?LinkId=746297)からインストーラーをダウンロードして実行します。  

> [!IMPORTANT]
> Microsoft では、更新されたバージョンの Connector for SAP BW を提供する予定はありません。 サード パーティによって開発されているため、Microsoft は SAP BW コンポーネントのソース コードを所有していません。そのため、ソース コードの更新はできません。 [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html) などの Microsoft ISV パートナーからの最新の SAP 接続コンポーネントの購入を検討してください。 Microsoft の ISV パートナーは、Azure で SSIS をインストールするために SAP 接続コンポーネントを適応させています。

> [!IMPORTANT]  
>  Microsoft Connector for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
## <a name="required-sap-files"></a>必要な SAP のファイル  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW を使用するために、SAP フロント エンド ソフトウェア (SAP GUI) をローカル コンピューターにインストールする必要はありません。  
  
 ただし、SAP の .NET コネクタ ファイルである librfc32.dll を、Windows フォルダー内の system サブフォルダーにコピーする必要があります (通常は、このフォルダーの場所は、 **C:\Windows\system32**です)。  
  
## <a name="considerations-for-64-bit-computers"></a>64 ビット コンピューターに関する注意事項  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW は、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows の 64 ビット バージョンを完全サポートしています。 64 ビット コンピューターでは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW に次の要件があります。  
  
-   任意の 64 ビット Windows オペレーティング システムで、パッケージを 64 ビット モードで実行するには、SAP GUI ファイルの 64 ビット バージョンである librfc32.dll を、Windows フォルダー内の **system32** フォルダーにコピーします (通常は、このファイルの場所は、 **C:\Windows\system32**です)。  
  
-   任意の 64 ビット Windows オペレーティング システムで、パッケージを 32 ビット モードで実行するには、SAP GUI ファイルである librfc32.dll を、Windows フォルダー内の **SysWow64** フォルダーにコピーします (通常は、このフォルダーの場所は、 **C:\Windows\SysWow64**です)。  
  
  
