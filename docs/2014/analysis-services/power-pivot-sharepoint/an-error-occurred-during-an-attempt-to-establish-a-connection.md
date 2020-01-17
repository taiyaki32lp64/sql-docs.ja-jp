---
title: 外部データ ソースへの接続を確立しようとしましたが、エラーが発生しました。 次の接続の更新に失敗しました:PowerPivot データ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c09c8984e964b4bdfa93b0fcebae2e613d484892
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071950"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection-to-the-external-data-source-the-following-connections-failed-to-refresh-powerpivot-data"></a>外部データ ソースへの接続を確立しようとしましたが、エラーが発生しました。 次の接続の更新に失敗しました:[PowerPivot データ]
  このエラーは、PowerPivot for SharePoint がインストールされていないサーバーで PowerPivot データのクエリを実行した場合に発生します。 また、SQL Server Analysis Services (PowerPivot) サービスが停止した場合や、PowerPivot データを以前のバージョンで表示しようとした場合にも発生します。  
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|対象|PowerPivot for SharePoint|  
|製品バージョン|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|データ接続に失敗しました。|  
|メッセージ テキスト|外部データ ソースへの接続を確立しようとしましたが、エラーが発生しました。 次の接続の更新に失敗しました:[PowerPivot データ]|  
  
## <a name="explanation"></a>説明  
 SharePoint にパブリッシュされた Excel ブック内の PowerPivot データのクエリを実行するときに SharePoint 環境に PowerPivot for SharePoint サーバーがないか、SQL Server Analysis Services (PowerPivot) サービスが停止している場合は、Excel Services からこのエラーが返されます。  
  
 このエラーは、クエリ エンジンを使用できないときに PowerPivot データのスライスまたはフィルター処理を行うと発生します。  
  
## <a name="user-action"></a>ユーザーの操作  
 PowerPivot for SharePoint をインストールするか、PowerPivot for SharePoint がインストールされた SharePoint 環境に PowerPivot ブックを移動します。 詳しくは、「 [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)」をご覧ください。  
  
 このソフトウェアがインストールされている場合は、SQL Server Analysis Services (PowerPivot) のインスタンスが実行されていることを確認します。 サーバーの全体管理で、 **[サーバーのサービスの管理]** を確認します。 また、管理ツールの [サービス] コンソール アプリケーションも確認します。  
  
 SQL Server 2008 R2 バージョンの PowerPivot for Excel で作成された PowerPivot ブックの場合、SQL Server 2008 R2 バージョンの Analysis Services OLE DB プロバイダーをインストールする必要があります。 プロバイダーをインストールし、Microsoft.AnalysisServices.ChannelTransport.dll ファイルを登録しなかった場合、このエラーが発生します。 ファイルの登録の詳細については、「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ接続では Windows 認証を使用しており、ユーザーの資格情報を借用できませんでした。次の接続の更新に失敗しました:PowerPivot データ](the-data-connection-user-could-not-be-delegated.md)  
  
  
