---
title: データ処理拡張機能の Connection クラスの実装 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- connections [Reporting Services], data processing extensions
- Connection class
- data processing extensions [Reporting Services], connections
ms.assetid: 7047d29e-a2c9-4e6f-ad02-635851a38ed7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fbd293c156f373de0cdad53b4419633ded15af8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63164134"
---
# <a name="implementing-a-connection-class-for-a-data-processing-extension"></a>データ処理拡張機能の Connection クラスの実装
  **Connection** オブジェクトはデータベース接続や類似するリソースを表し、ユーザーにとっては [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能の出発点です。 このオブジェクトはデータベース サーバーへの接続を表しますが、類似する動作を持つエンティティが **Connection** として表示される可能性があります。  
  
 **Connection** オブジェクトを実装するには、<xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> を実装し、オプションで <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> を実装するクラスを作成します。  
  
 実装では、接続が作成され、開かれていることを確認した後でコマンドを実行する必要があります。 実装にはクライアントが接続を明示的に開閉する必要があります。実装がクライアントの接続を暗黙的に開閉するのではありません。 接続を取得したら、セキュリティ チェックを実行します。 [!INCLUDE[ssRS](../../../includes/ssrs.md)] データ処理拡張機能で他のクラスの既存接続が必要な場合は、データ ソースの操作時にセキュリティ チェックが常に確実に実行されるようにします。  
  
 該当する接続のプロパティは、接続文字列として表されます。 OLE DB によって定義されている使い慣れた名前と値のペアを使用して、[!INCLUDE[ssRS](../../../includes/ssrs.md)] データ処理拡張機能で <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection.ConnectionString%2A> プロパティをサポートすることを強くお勧めします。  
  
> [!NOTE]  
>  **Connection** オブジェクトの取得にリソースが大きく消費されることがあるため、接続のプールなどの技法を検討してこの問題を緩和してください。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> は、<xref:Microsoft.ReportingServices.Interfaces.IExtension> から継承されます。 <xref:Microsoft.ReportingServices.Interfaces.IExtension> インターフェイスは、Connection クラス実装の一部として実装する必要があります。 <xref:Microsoft.ReportingServices.Interfaces.IExtension> インターフェイスによって、クラスがローカライズされた拡張機能名を実装し、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成ファイルに格納された拡張機能固有の構成情報を処理できるようになります。  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension> の実装によって、**Connection** オブジェクトに <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> プロパティが含まれます。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能で <xref:Microsoft.ReportingServices.Interfaces.IExtension.LocalizedName%2A> プロパティをサポートすることを強くお勧めします。これにより、レポート マネージャーなどのユーザー インターフェイスの拡張機能に、ローカライズされた使い慣れた名前がユーザーに表示されます。  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension> によって、**Connection** オブジェクトが RSReportServer.config ファイルに格納されたカスタム構成データを取得し、処理することもできます。 カスタム構成データの処理の詳細については、<xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A> メソッドを参照してください。  
  
 <xref:Microsoft.ReportingServices.Interfaces.IExtension> を実装するクラスは、残りのデータ処理拡張機能のクラスが読み込まれていない場合は、メモリから読み込まれません。 このため、**Extension** クラスを使用して、相互接続状態の情報を格納することや、キャッシュできるデータをメモリに格納することができます。 **Extension** クラスは、レポート サーバーを実行中はメモリに残ります。  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> を実装することによって、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] の資格情報のサポートを含むように **Connection** クラスを拡張できます。 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> インターフェイスの <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.IntegratedSecurity%2A>、<xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.UserName%2A>、および <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension.Password%2A> の各プロパティを実装する場合は、レポート デザイナーの **[データ ソース]** ダイアログ ボックスで **[統合セキュリティ]** チェック ボックスをオンにし、 **[ユーザー名]** ボックスと **[パスワード]** ボックスに必要な情報を入力します。 これによって、レポート デザイナーは承認をサポートするデータ ソースの資格情報を格納および取得できます。 資格情報は、セキュリティによって保護されて格納され、プレビュー モードでレポートを表示する場合に使用されます。  
  
> [!NOTE]  
>  <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> を暗黙的に実装するには、<xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> インターフェイスと <xref:Microsoft.ReportingServices.Interfaces.IExtension> インターフェイスのメンバーを実装する必要があります。  
>   
>  **Connection** クラス実装の例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services の製品サンプル) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../reporting-services-extensions.md)   
 [データ処理拡張機能の実装](implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
