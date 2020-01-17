---
title: 作成、削除、または共有データ ソースを変更 (レポート マネージャー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- removing shared data sources
- data sources [Reporting Services], shared
- deleting shared data sources
- modifying shared data sources
ms.assetid: cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c554215ba716a35f3e2851a5042be1989ee5648c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109611"
---
# <a name="create-delete-or-modify-a-shared-data-source-report-manager"></a>共有データ ソースを作成、削除、または変更する (レポート マネージャー)
  共有データ ソースでは、1 つのデータ ソースに対する接続プロパティを指定します。 多数のレポート、モデル、またはデータ ドリブン サブスクリプションで 1 つのデータ ソースを使用する場合は、共有データ ソースを作成することにより、同じ接続情報を複数箇所で管理するオーバーヘッドを低減できます。  
  
 次のアイコンは、レポート マネージャーのフォルダー階層内の共有データ ソースを示します。  
  
 ![共有データ ソースのアイコン](media/hlp-16datasource.png "共有データ ソースのアイコン")  
共有データ ソースのアイコン  
  
### <a name="to-create-a-shared-data-source"></a>共有データ ソースを作成するには  
  
1.  [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) を開始します。  
  
2.  レポート マネージャーで **[コンテンツ]** ページに移動します。  
  
3.  **[新しいデータ ソース]** をクリックします。 **[新しいデータ ソース]** ページが開きます。  
  
4.  アイテムの名前を入力します。 名前は 1 文字以上で、文字で始まる必要があります。 特定の記号を含めることもできますが、スペースまたは ; ? : \@ & = + , $ / * \< > | " /.  
  
5.  必要に応じて説明を入力し、接続に関する情報をユーザーに提供します。 この説明は、レポート マネージャーの **[コンテンツ]** ページに表示されます。  
  
6.  **[データ ソースの種類]** の一覧で、データ ソースから取得したデータの処理に使用するデータ処理拡張機能を指定します。  
  
7.  **[接続文字列]** でレポート サーバーがデータ ソースへの接続に使用する接続文字列を指定します。 接続文字列には資格情報を指定しないことをお勧めします。  
  
     以下に、ローカルの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースへの接続に使用する接続文字列の例を示します。  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  **[接続に使用する認証]** では、レポートが実行される際に資格情報を取得する方法を指定します。  
  
    -   ユーザーにログオン名とパスワードを要求する場合は、 **[レポートの実行者により指定された資格情報]** をクリックします。 ユーザーが入力する資格情報を Windows 資格情報として使用するには、 **[データ ソースへの接続時に Windows 資格情報として使用する]** をクリックします。 ユーザー名とパスワードがデータベースの資格情報である場合は、このオプションを選択しないでください。  
  
    -   データ ソースの使用目的が、保存された資格情報によって所有者が管理する共有データ ソースとしての使用や、サブスクリプションやその他のスケジュール設定された操作 (自動レポート履歴生成など) をサポートするレポートでの使用である場合は、 **[レポート サーバーに保存され、セキュリティで保護された資格情報]** をクリックします。 データベース サーバーが権限の借用または委譲をサポートしている場合は、 **[データ ソースへの接続が確立した後に、認証されているユーザーの権限を借用する]** を選択できます。  
  
    -   レポート サーバーが、レポートにアクセスするユーザーの資格情報を、外部データ ソースをホストするサーバーに渡す場合は、 **[Windows 統合セキュリティ]** をクリックします。 この場合、ユーザーはユーザー名やパスワードを入力することを要求されません。  
  
    -   データ ソースで資格情報を使用しない場合 (ファイル システムからアクセス可能な XML ファイルをデータ ソースとして使用する場合など) は、 **[資格情報は必要ありません]** をクリックします。 この資格情報オプションは、使用するデータ ソースで妥当と考えられる場合にのみ指定してください。 認証を必要とするデータ ソースに対してこのオプションを選択した場合、接続エラーが発生します。 このオプションを選択する場合は、ユーザーの資格情報を利用できない場合に、レポート サーバーが他のコンピューターに接続して、データまたはファイルを取得できるように、必ず自動実行アカウントを構成してください。  
  
     資格情報の構成の詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。 自動実行アカウントについては、「[自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。  
  
9. データ ソース構成を検証するには、 **[接続テスト]** をクリックします。  
  
    > [!NOTE]  
    >  [接続テスト] ボタンは、XML データ ソースの種類ではサポートされません。  
  
10. **[OK]** をクリックします。  
  
### <a name="to-modify-a-shared-data-source"></a>共有データ ソースを変更するには  
  
1.  レポート マネージャーで [コンテンツ] ページに移動します。  
  
2.  共有データ ソース アイテムに移動し、アイテムの上にマウス ポインターを移動して、ドロップダウン リストをクリックし、コンテキスト メニューから **[管理]** をクリックします。 **[プロパティ]** ページを開きます。  
  
3.  データ ソースを変更し、 **[適用]** をクリックします。  
  
### <a name="to-delete-a-shared-data-source"></a>共有データ ソースを削除するには  
  
-   レポート マネージャーで、 **[コンテンツ]** ページに移動し、次のいずれかの操作を行います。  
  
    -   共有データ ソース アイテムに移動します。  
  
         アイテムをクリックして開きます。 [全般プロパティ] ページが開きます。  
  
         **[削除]** をクリックして、 **[OK]** をクリックします。  
  
    -   **[コンテンツ]** ページで、削除するデータ ソースを含むフォルダーに移動します。  
  
         アイテムの上にマウス ポインターを移動して、ドロップダウン リストをクリックし、コンテキスト メニューから **[削除]** をクリックします。  
  
         [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [データ接続、データ ソース、および Reporting Services の接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [[コンテンツ] ページ (レポート マネージャー)](../../2014/reporting-services/contents-page-report-manager.md)   
 [共有データ ソースを作成、変更、および削除する (SSRS)](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [レポート データ ソースを管理する](report-data/manage-report-data-sources.md)   
 [レポートのデータ ソースのプロパティを構成する (レポート マネージャー)](report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
