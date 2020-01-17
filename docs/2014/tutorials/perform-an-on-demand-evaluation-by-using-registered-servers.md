---
title: 登録済みサーバーを使用して、時評価を実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a3a79a6ec655e91264d6fcc00db5a920ad82a21e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822374"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>登録済みサーバーを使用した要求時評価の実行

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の 1 つ以上のインスタンスに対して登録済みサーバーを使用して、ベスト プラクティス ポリシーの要求時評価を実行できます。 使用できるのは、ローカル サーバー グループまたは中央管理サーバーのいずれかです。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 以降のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を実行しているサーバー グループ メンバーに対して、ベスト プラクティス ポリシーの要求時評価を実行できます。 ただし、[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] または [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] でサポートされていない一部のプロパティがポリシーによって参照される場合は、例外エラーが発生することがあります。  
  
## <a name="prerequisites"></a>前提条件  
 この作業を実行するには、登録済みサーバーでサーバー登録を 1 つ以上構成しておく必要があります。 詳細については、次の各トピックを参照してください。  
  
-   [サーバー グループの作成または編集 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [接続のサーバーの登録&#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)します。  
  
-   [中央管理サーバーとサーバー グループの作成 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>サーバー グループに対してベスト プラクティス ポリシーを評価するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]で、 **[表示]** メニューの **[登録済みサーバー]** をクリックします。  
  
2.  展開**データベース エンジン**、いずれかを展開**ローカル サーバー グループ**、または**中央管理サーバー**構成に応じて、します。  
  
3.  以下のいずれかを実行します。  
  
    -   ローカル サーバー グループによって管理されているすべてのサーバーまたは中央管理サーバーに対してポリシーを評価するため、ローカル サーバー グループ名または中央管理サーバー名を右クリックし、**ポリシーの評価**.  
  
        > [!NOTE]  
        >  中央管理サーバーを通じてポリシーを評価する場合、ポリシーは中央管理サーバー自体に対しては評価されません。  
  
    -   特定のサーバーまたはサーバー グループに対してポリシーを評価するには展開**ローカル サーバー グループ**または中央管理サーバー名、サーバーまたはサーバー グループをクリックして、ポリシーの評価を右クリックして**ポリシー評価**します。  
  
4.  **ポリシーの評価** ダイアログ ボックスの横に、**ソース**ボックスで、省略記号ボタンをクリックします ( **.** ) ボタンをクリックします。  
  
5.  **ソースの選択**ダイアログ ボックスで、いずれかを選択できます**ファイル**または**Server**を評価するポリシー ファイルのソースとして。 クリックすると**Server**、ローカルまたはリモート サーバー上のポリシー ベースの管理に以前インポートされたすべてのベスト プラクティス ポリシーのオンデマンドで評価を行うことができます。 このチュートリアルをクリックして**ファイル**、し評価する個々 のポリシー ファイルを選択します。 これを行うには、次の手順を実行します。  
  
    1.  クリックして**ファイル**します。  
  
    2.  横に**ファイル**、省略記号をクリックします ( **.** ) ボタンをクリックします。  
  
    3.  クリックして、評価、1 つまたは複数の .xml ポリシー ファイルを選択します。**オープン**します。  
  
         選択したファイルの一覧に表示されます、**ファイル**ボックス。  
  
    4.  **ソースの選択**ダイアログ ボックスで、をクリックして**OK**します。  
  
    5.  場合、**ポリシーを読み込んでいます** ダイアログ ボックスが表示されたら、をクリックして**閉じる**します。  
  
     選択したポリシーが表示されて、**ポリシーの選択**ページ。 ポリシーの横に警告アイコンが表示された場合、そのポリシーにスクリプトが含まれていることを示します。  
  
6.  クリックして**Evaluate**ポリシーを評価します。  
  
7.  一部のポリシー エラーでは、ポリシー ベースの管理機能によってポリシーへの準拠を対象に直ちに適用できます。 このようなエラーの場合、エラーが発生したポリシーの横にチェック ボックスが表示されます。 チェック ボックスが表示される場合は、チェック ボックスを選択するか、行、失敗したポリシーをクリックすると、**対象の詳細**評価に失敗した対象インスタンスの横にあるウィンドウ。 チェック ボックスのいずれかが選択されている場合、**適用**ボタンが使用可能になります。 クリックすると**適用**、準拠していない設定が自動的に選択したターゲット インスタンスに更新されます。  
  
    > [!CAUTION]  
    >  ポリシー設定を十分に理解してから、対象インスタンスを自動更新してください。 1 つまたは複数のチェック ボックスを選択した後にクリックすることをお勧めします。**スクリプト**、基になるかを確認することができます、出力場所を選択し[!INCLUDE[tsql](../includes/tsql-md.md)]コードの変更を適用する前にします。  
  
8.  ポリシーの詳細な結果を表示するでポリシーをクリックして、**結果**テーブル。 **対象の詳細**テーブルには、各インスタンスの詳細が表示されます。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 2:スケジュールされた単位でベスト プラクティス ポリシーを評価します。](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>参照  
 [監視し、ポリシー ベースの管理を使用してベスト プラクティスを適用します。](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [中央管理サーバーを使用した複数のサーバーの管理](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
