---
title: マスター データ マネージャー Web アプリケーションのセキュリティ保護 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2bcbdacd6d08a6139975c20bb8f1d5010195375b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479354"
---
# <a name="secure-a-master-data-manager-web-application"></a>マスター データ マネージャー Web アプリケーションのセキュリティ保護
  HTTPS を使用して [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションをセキュリティ保護できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションは、HTTP または HTTPS のいずれかを使用できますが、両方を使用することはできません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] がインストールされている Web サーバーの管理者である必要があります。  
  
-   MDS が Web サーバーにインストールされていて、Web アプリケーションが存在する必要があります。 詳細については、「[マスター データ サービスのインストール](install-master-data-services.md)」および「[マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](create-a-master-data-manager-web-application-master-data-services.md)」を参照してください。  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>HTTPS を使用してマスター データ マネージャー Web アプリケーションをセキュリティ保護するには  
  
1.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションが HTTP を使用して正しく構成されていることを確認した後、IIS で証明書を作成します。 詳細については、「 [IIS 7 でサーバー証明書を構成する](https://technet.microsoft.com/library/cc732230\(WS.10\).aspx)」を参照してください。  
  
2.  **[接続]** ペインの **[サイト]** で、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションをホストするサイトをクリックします。  
  
3.  **[アクション]** ペインで、 **[バインド]** をクリックします。  
  
4.  **[追加]** をクリックします。  
  
5.  一覧から、 **[https]** を選択します。  
  
6.  SSL 証明書を選択します。  
  
7.  [**OK**] をクリックします。  
  
8.  任意。 HTTP を削除してユーザーが HTTPS のみを使用してサイトにアクセスできるようにするには、一覧の **[http]** の行をクリックします。 **[削除]** をクリックし、確認のダイアログ ボックスで **[はい]** をクリックします。  
  
    > [!IMPORTANT]  
    >  HTTP を削除した後に basicHttp 構成および wsHttpBinding 構成を変更する必要があります。  
  
9. **[サイト バインド]** ダイアログ ボックスを閉じるには、 **[閉じる]** をクリックします。  
  
10. Web.config ファイルを開くようになりました*ドライブ*: \Program Files\Microsoft SQL server \120\master Data services \webapplication です。  
  
11. " `<security mode="Message">` " という文字列を探して、" `<security mode="Transport">`" に変更します。  
  
12. ファイルを保存して閉じます。 エラーが発生した場合は、UAC が有効になっている可能性があります。 詳細については、 [ユーザー アカウント制御の無効化](https://technet.microsoft.com/library/cc709691\(WS.10\).aspx)に関する記事を参照してください。 これで、ユーザーが HTTPS を使用してサイトにアクセスできるようになりました。  
  
## <a name="see-also"></a>関連項目  
 [マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](create-a-master-data-manager-web-application-master-data-services.md)  
  
  
