---
title: データ接続では Windows 認証を使用しており、ユーザーの資格情報を借用できませんでした。 次の接続の更新に失敗しました:PowerPivot データ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b11e1510213aefa98c6bf2c0c779cebaeed85e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071029"
---
# <a name="the-data-connection-uses-windows-authentication-and-user-credentials-could-not-be-delegated-the-following-connections-failed-to-refresh-powerpivot-data"></a>データ接続では Windows 認証を使用しており、ユーザーの資格情報を借用できませんでした。 次の接続の更新に失敗しました:[PowerPivot データ]
  PowerPivot データを含む Excel ブックで、Excel Services は、SharePoint の PowerPivot サーバー インスタンスに接続できない場合にこのエラーを返します。  
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|対象|PowerPivot for SharePoint|  
|製品バージョン|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|PowerPivot データ プロバイダーを使用しようとしたときに接続が失敗しました。|  
|メッセージ テキスト|データ接続では Windows 認証を使用しており、ユーザーの資格情報を借用できませんでした。 次の接続の更新に失敗しました:[PowerPivot データ]|  
  
## <a name="explanation"></a>説明  
 このエラー メッセージには複数の原因があります。 それらの原因に共通する要因は、Excel Services が SharePoint のクレーム トークンから有効な Windows ユーザー ID を取得できないことです。 PowerPivot データを含む Excel ブックの場合、次のいずれかの条件に当てはまるときは、このエラーが発生します。  
  
-   Windows トークン サービスに対するクレームが実行されていない。 SharePoint ログ ファイルを表示して、このエラーの原因を確認できます。 SharePoint ログに、"パイプ エンドポイント 'net.pipe://localhost/s4u/022694f3-9fbd-422b-b4b2-312e25dae2a2' が、ローカル コンピューター上で見つかりませんでした" というメッセージがある場合、Windows トークン サービスに対するクレームは実行されていません。 このサービスを開始するには、サーバーの全体管理を使用します。その後、[サービス] コンソール アプリケーションでサービスが実行されていることを確認します。  
  
-   ユーザー ID の検証にドメイン コントローラーを使用できない。 Windows トークン サービスに対するクレームでは、キャッシュされた資格情報は使用されません。 接続ごとにユーザー ID が検証されます。 SharePoint ログ ファイルを表示して、このエラーの原因を確認できます。 SharePoint ログに、"IClaimsIdentity から WindowsIdentity を取得できませんでした" というメッセージがある場合、ユーザー ID を認証できなかったことを示します。  
  
-   コンピューターは同じドメインまたは双方向の信頼関係を持つドメインのメンバーである必要がある。  
  
-   Windows ドメイン ユーザー アカウントを使用する必要がある。 これらのアカウントにはユニバーサル プリンシパル名 (UPN) が必要です。  
  
-   オブジェクトを照会するために、Excel Services サービス アカウントに Active Directory のアクセス許可が必要である。  
  
## <a name="user-action"></a>ユーザーの操作  
 次の手順に従って、Windows トークン サービスに対するクレームの状態を確認します。  
  
 その他の場合については、ネットワーク管理者に確認してください。  
  
#### <a name="enable-claims-to-windows-token-service"></a>Windows トークン サービスに対するクレームの有効化  
  
1.  サーバーの全体管理で、[システム設定] の **[サーバーのサービスの管理]** をクリックします。  
  
2.  **[Windows トークン サービスに対するクレーム]** を選択し、 **[開始]** をクリックします。  
  
3.  [サービス] コンソールでサービスが実行されていることも確認します。  
  
    1.  [管理ツール] で、[サービス] をクリックします。  
  
    2.  Windows トークン サービスに対するクレームが実行されていない場合は開始します。  
  
## <a name="see-also"></a>参照  
 [PowerPivot サービス アカウントの構成](configure-power-pivot-service-accounts.md)  
  
  
