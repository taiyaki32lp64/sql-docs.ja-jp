---
title: データベースのパブリッシュ (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 98b2914e-7147-40af-ba7d-87253bbe8bf9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b11aa11f942e6f0f801de36c7d15e17cae4141b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916622"
---
# <a name="publish-a-database-sql-server-management-studio"></a>データベースのパブリッシュ (SQL Server Management Studio)
  **スクリプトの生成とパブリッシュ ウィザード** を使用して、データベース全体または個々のデータベース オブジェクトを Web ホスティング プロバイダーにパブリッシュできます。  
  
> [!NOTE]  
>  以前のバージョンでは、このトピックで説明する機能がデータベース パブリッシュ ウィザードで提供されていました。 今回のバージョンから、パブリッシュ機能はスクリプトの生成とパブリッシュ ウィザードに追加され、データベース パブリッシュ ウィザードは廃止されました。  
  
## <a name="generate-and-publish-scripts-wizard"></a>スクリプトの生成とパブリッシュ ウィザード  
 スクリプトの生成とパブリッシュ ウィザードを使用し、データベース全体または選択したデータベース オブジェクトを Web ホスティング プロバイダーにパブリッシュできます。 SQL Server Web ホスティング プロバイダーは、Web サービスの接続インターフェイスを提供します。 この Web サービスを作成するには、CodePlex 上にある SQL Server Hosting Toolkit の Database Publishing Services プロジェクトを使用します。 この Web サービスにより、Web ホスティング事業者の顧客は、スクリプトの生成とパブリッシュ ウィザードを使用して、各自のデータベースをサービスに簡単にパブリッシュできるようになります。 SQL Server Hosting Toolkit のダウンロードの詳細については、「 [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)」をご覧ください。  
  
 スクリプトの生成とパブリッシュ ウィザードを使用して、データベース転送用のスクリプトを作成することもできます。  
  
#### <a name="to-publish-a-database-to-a-web-service"></a>Web サービスにデータベースをパブリッシュするには  
  
1.  オブジェクト エクスプローラーで **[データベース]** を展開してデータベースを右クリックし、 **[タスク]** をポイントして **[スクリプトの生成とパブリッシュ]** をクリックします。 ウィザードの手順に従って、パブリッシュするデータベース オブジェクトのスクリプトを作成します。  
  
2.  **[オブジェクトの選択]** ページで、Web ホスティング サービスにパブリッシュするオブジェクトを選択します。  
  
3.  **[スクリプト作成オプションの設定]** ページで、 **[Web サービスにパブリッシュ]** を選択します。  
  
    1.  **[プロバイダー]** ボックスで、使用する Web サービスのプロバイダーを指定します。 Web ホスティング プロバイダーを構成していない場合は、 **[プロバイダーの管理]** をクリックして **[プロバイダーの管理]** ダイアログ ボックスを表示し、使用する Web サービスのプロバイダーを構成します。  
  
    2.  パブリッシングの詳細オプションを指定するには、 **[Web サービスにパブリッシュ]** セクションの **[詳細設定]** をクリックします。  
  
4.  **[概要]** ページで選択内容を確認します。 選択内容を変更するには、 **[戻る]** をクリックします。 選択したオブジェクトをパブリッシュするには、 **[次へ]** をクリックします。  
  
5.  **[スクリプトの保存またはパブリッシュ]** ページで、パブリケーションの進行状況を監視します。  
  
## <a name="see-also"></a>参照  
 [スクリプトの生成 &#40;SQL Server Management Studio&#41;](../scripting/generate-scripts-sql-server-management-studio.md)   
 [他のサーバーへのデータベースのコピー](copy-databases-to-other-servers.md)  
  
  
