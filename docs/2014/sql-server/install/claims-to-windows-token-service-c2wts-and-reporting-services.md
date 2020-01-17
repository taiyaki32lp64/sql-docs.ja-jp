---
title: Windows トークンサービスに対するクレーム (C2WTS) と Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0ec82b7cca2062e1ed918e300eeb76dad16cbb20
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245619"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) と Reporting Services
  Sharepoint ファームの外部にあるデータソースに対して windows 認証[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]を使用する場合、sharepoint モードでは、Windows トークンサービスに対する sharepoint クレーム (c2WTS) が必要です。 これは、Web フロントエンド (WFE) と [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービス間の通信が常に要求認証になるため、ユーザーが Windows 認証を使用してデータ ソースにアクセスする場合にも当てはまります。  
  
 c2WTS は、データ ソースが共有サービスと同じコンピューター上にある場合でも必要です。 ただし、このシナリオでは、制約付き委任は必要ありません。  
  
 c2WTS によって作成されたトークンは、制約付き委任 (特定のサービスへの制約) と "認証プロトコルの使用" 構成オプションでのみ機能します。 既に述べたとおり、データ ソースが共有サービスと同じコンピューター上にある場合は、制約付き委任は必要ありません。  
  
 Kerberos の制約付き委任を使用する環境では、SharePoint Server サービスと外部データ ソースが同じ Windows ドメインに属している必要があります。 Claims to Windows Token Service (c2WTS) に依存する任意のサービスでは、Kerberos の **制約付き** 委任を使用して、c2WTS が Kerberos プロトコル遷移を使用して要求を Windows 資格情報に変換できるようにする必要があります。 これらの要件は、すべての SharePoint 共有サービスに共通です。 詳細については、「 [Microsoft SharePoint 2010 製品の Kerberos 認証のhttps://technet.microsoft.com/library/gg502594.aspx)概要」 (](https://technet.microsoft.com/library/gg502594.aspx)を参照してください。  
  
 このトピックでは、手順をまとめています。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124; sharepoint 2010|  
  
## <a name="prerequisites"></a>前提条件  
  
> [!NOTE]  
>  注: 構成手順によっては、変更されたり、特定のファーム トポロジで機能しない場合があります。 たとえば、シングル サーバー インストールでは Windows Identity Foundation c2WTS サービスをサポートしていないため、Windows トークンに対するクレームの委任シナリオは、このファーム構成では可能でありません。  
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>c2WTS の構成に必要な基本的な手順  
  
1.  c2WTS サービス アカウントを構成します。 c2WTS を実行する各アプリケーション サーバーのローカルの Administrators グループにサービス アカウントを追加します。 さらに、アカウントに次のローカル セキュリティ ポリシー権限があることを確認します。  
  
    -   オペレーティング システムの一部として機能  
  
    -   認証後にクライアントを借用する  
  
    -   サービスとしてログオン  
  
     C2WTS に使用するアカウントは、プロトコル遷移を使用した制約付き委任用に構成する必要があります。また、通信に必要なサービス (SQL Server エンジン、SQL Server Analysis Services) に委任するためのアクセス許可が必要です。委任を構成するには、Active Directory ユーザーとコンピューターのスナップインを使用します。  
  
    1.  各サービス アカウントを右クリックして、プロパティ ダイアログを開きます。 ダイアログで **[委任]** タブをクリックします。  
  
        > [!NOTE]  
        >  注: 委任タブは、オブジェクトに SPN が割り当てられている場合にのみ表示されます。 c2WTS では、c2WTS アカウントに SPN は必要ありませんが、SPN がない場合、[**委任**] タブは表示されません。 制約付き委任を構成する別の方法として、 **ADSIEdit**などのユーティリティを使用するという方法もあります。  
  
    2.  委任タブで重要な構成オプションは、次のとおりです。  
  
        -   [指定されたサービスへの委任でのみこのユーザーを信頼する] を選択します。  
  
        -   [任意の認証プロトコルを使用する] を選択します。  
  
         詳細については、ホワイトペーパー「 [SharePoint 2010 および SQL Server 2008 R2 製品の kerberos 認証の構成](https://blogs.technet.com/b/tothesharepoint/archive/2010/07/22/whitepaper-configuring-kerberos-authentication-for-sharepoint-2010-and-sql-server-2008-r2-products.aspx)」の「コンピューターとサービスアカウント用に kerberos の制約付き委任を構成する」セクションを参照してください。  
  
2.  C2WTS ' AllowedCallers 元 ' を構成します  
  
     c2WTS では、構成ファイル**c2wtshost.exe.confi**に明示的にリストされた ' 呼び出し元 ' id が必要です。c2WTS は、そのように構成されている場合を除き、システム内のすべての認証済みユーザーからの要求を受け入れません。 この場合、"呼び出し元" は WSS_WPG Windows グループです。 c2wtshost.exe.confi ファイルは次の場所に保存されます。  
  
     **Foundation\v3.5\c2wtshost.exe.config Files\Windows Identity**  
  
     構成ファイルの例を次に示します。  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```  
  
3.  オペレーティング システム c2WTS サービスを起動します。  
  
    1.  前の手順で構成したサービス アカウントを使用するようにサービスを構成します。  
  
    2.  [スタートアップの種類] を [**自動**] に変更し、サービスを開始します。  
  
4.  SharePoint の [Windows トークンサービスに対する要求] を開始する: [**サーバーのサービスの管理**] ページで、sharepoint サーバーの全体管理を使用して、Windows トークンサービスに対するクレームを開始します。 このサービスは、アクションを実行するサーバーで起動する必要があります。 たとえば、WFE サーバーと [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスを実行しているアプリケーション サーバーを持っている場合は、アプリケーション サーバーで c2WTS を起動するだけでかまいません。 c2WTS は WFE では必要ありません。  
  
## <a name="see-also"></a>参照  
 [Windows トークンサービスに対するクレーム (c2WTS) の概要 (https://msdn.microsoft.com/library/ee517278.aspx)](https://msdn.microsoft.com/library/ee517278.aspx)   
 [Microsoft SharePoint 2010 製品の Kerberos 認証の概要 (https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)  
  
