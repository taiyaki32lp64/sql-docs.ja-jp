---
title: ブック内のデータ接続に関するデータを更新できません。 再試行するか、システム管理者に問い合わせてください。 次の接続の更新に失敗しました:PowerPivot データ |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0f6fd52d-ac72-43e3-aa08-05a2d2bb873d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81e99fc17cb8f369967ff4c26699e67f0ed91d33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070942"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook-try-again-or-contact-your-system-administrator-the-following-connections-failed-to-refresh-powerpivot-data"></a>ブック内のデータ接続に関するデータを更新できません。 再試行するか、システム管理者に問い合わせてください。 次の接続の更新に失敗しました:[PowerPivot データ]
  PowerPivot データを含む Excel ブックで、Excel Services は、PowerPivot サーバーに送信した接続要求が失敗した場合にこのエラーを返します。  
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|適用対象|PowerPivot for SharePoint のインストール|  
|製品バージョン|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|下記を参照。|  
|メッセージ テキスト|ブック内のデータ接続に関するデータを更新できません。 再試行するか、システム管理者に問い合わせてください。 次の接続の更新に失敗しました:[PowerPivot データ]|  
  
## <a name="explanation-and-resolution"></a>説明および解決方法  
 Excel Services が PowerPivot データに接続できないか、PowerPivot データを読み込むことができません。 このエラーは、次のような状況で発生します。  
  
 **シナリオ 1: サービスが開始されていません。**  
  
 SQL Server Analysis Services (PowerPivot) インスタンスが開始されていません。 パスワードの期限が切れると、サービスの実行が停止します。 パスワードを変更する方法についての詳細については、次を参照してください。 [PowerPivot サービス アカウントの構成](configure-power-pivot-service-accounts.md)と[開始または PowerPivot を SharePoint サーバーの停止](start-or-stop-a-power-pivot-for-sharepoint-server.md)します。  
  
 **シナリオ 2 a:以前のバージョンのブック n、サーバーを開く**  
  
 開こうとしているブックが、SQL Server 2008 R2 バージョンの PowerPivot for Excel で作成された可能性があります。 ほとんどの場合、データ接続文字列で指定された Analysis Services データ プロバイダーは、要求を処理しているコンピューター上に存在しません。  
  
 この場合は、ULS ログにこのメッセージが表示されます。"ブック 'PowerPivot データ' の更新に失敗しました '\<ブックへの URL >'"、続いて「接続を取得できません」です。  
  
 ブックのバージョンを決定するには、Excel で開き、接続文字列にどのデータ プロバイダーが指定されているか確認します。 SQL Server 2008 R2 ブックは、MSOLAP.4 をデータ プロバイダーとして使用します。  
  
 この問題を回避するために、ブックをアップグレードすることができます。 または、以下の方法で PowerPivot for SharePoint または Excel Services を実行している物理コンピューター上の SQL Server 2008 R2 バージョンの Analysis Services からクライアント ライブラリをインストールすることができます。  
  
 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 **シナリオ 2 b:クライアント ライブラリのバージョンが間違っているアプリケーション サーバーで Excel Services が実行されています。**  
  
 既定では、SharePoint Server 2010 は、SQL Server 2008 バージョンの Analysis Services OLE DB プロバイダーを Excel Services を実行するアプリケーション サーバーにインストールします。 PowerPivot データ アクセスをサポートするファームでは、Excel Services や PowerPivot for SharePoint など、PowerPivot データを要求するアプリケーションを実行するすべての物理サーバーは、最新バージョンのデータ プロバイダーを使用する必要があります。  
  
 PowerPivot for SharePoint を実行するサーバーは、更新された OLE DB データ プロバイダーを自動的に取得します。 同じコンピューター上の PowerPivot for SharePoint を使用しない、スタンドアロン インスタンスの Excel Services など、その他のサーバーは、新しいクライアント ライブラリを使用するために、更新プログラムを適用する必要があります。 「 [SharePoint サーバーへの Analysis Services OLE DB プロバイダーのインストール](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。  
  
 **シナリオ 3: ドメイン コント ローラーは使用できません。**  
  
 ユーザー ID の検証にドメイン コントローラーを使用できないことが原因である場合があります。 Windows トークン サービスに対するクレームにより各接続で SharePoint ユーザーを認証するには、ドメイン コントローラーが必要です。 Windows トークン サービスに対するクレームでは、キャッシュされた資格情報は使用されません。 接続ごとにユーザー ID が検証されます。  
  
 SharePoint ログ ファイルを表示して、このエラーの原因を確認できます。 SharePoint ログに、"IClaimsIdentity から WindowsIdentity を取得できませんでした" というメッセージがある場合、ユーザー ID を認証できなかったことを示します。  
  
 この問題を回避するには、PowerPivot サーバーと同じドメインにコンピューターを所属させるか、ローカル コンピューターにドメイン コントローラーをインストールします。 2 番目の解決策として、ドメイン コントローラーのインストールを行う場合は、すべてのサービスとユーザーのローカル ドメイン アカウントを作成することが必要になります。 それには、サービス アカウントを構成して、定義したアカウントの SharePoint 権限を構成する必要があります。  
  
 PowerPivot for SharePoint をオフライン状態で使用することを目的とする場合は、コンピューターにドメイン コントローラーをインストールすると便利です。 PowerPivot をオフラインで使用する方法の詳細については、ブログ エントリを参照してください「"PowerPivot サーバーをネットワークから切断を取り入れること」 [ http://www.powerpivotgeek.com](https://go.microsoft.com/fwlink/?LinkId=184241)します。  
  
 **シナリオ 4: 不安定なサーバー**  
  
 1 つ以上のサービスが一貫性のない状態にある可能性があります。 IISRESET を実行すると問題が解決することがあります。  
  
  
