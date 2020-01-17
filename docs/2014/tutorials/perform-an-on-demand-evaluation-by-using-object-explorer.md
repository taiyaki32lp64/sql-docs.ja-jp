---
title: オブジェクト エクスプ ローラーを使用して、時評価を実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d2aadd055334c7ee64871c2fdfe5239c9849e90
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210943"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>オブジェクト エクスプローラーを使用した要求時評価の実行
  ここでは、オブジェクト エクスプローラーを使用して、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] の単一インスタンス上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に対して、ベスト プラクティス ポリシーの要求時評価を実行します。  
  
> [!NOTE]  
>  単一インスタンス上のポリシーの評価は、登録済みサーバーを通じて行うこともできます。 詳細については、次を参照してください。[登録済みサーバーを使用して、オンデマンド評価の実行](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)します。  
  
## <a name="prerequisites"></a>前提条件  
 このレッスンでは、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のバージョンを使用します。  
  
> [!NOTE]  
>  オンデマンドで実行しているインスタンスに対してベスト プラクティス ポリシーの評価を実行する[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、トピックの手順を使用する必要があります[登録済みサーバーを使用して、オンデマンド評価の実行](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)します。  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>オブジェクト エクスプローラーを使用して要求時評価を実行するには  
  
1.  開始[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]に接続し、[!INCLUDE[ssDE](../includes/ssde-md.md)]します。  
  
2.  オブジェクト エクスプ ローラーで、**管理**、展開**ポリシーの管理**、右クリック**ポリシー**、順にクリックします**Evaluate**します。  
  
    > [!NOTE]  
    >  既定では、ローカル インスタンスがポリシーのソースとして使用されます。 ベスト プラクティス ポリシーを以前にインポートしている場合は、作成済みのポリシーがあれば、それと共に一覧表示されます。 インポートしたベスト プラクティス ポリシーのいずれかを選択してクリックして**Evaluate**します。 ベスト プラクティス ポリシーをインポートしていない場合には、この手順を続行します。  
  
3.  **ポリシーの評価** ダイアログ ボックスの横に、**ソース**ボックスで、省略記号ボタンをクリックします ( **.** ) ボタンをクリックします。  
  
4.  **ソースの選択**ダイアログ ボックスで、いずれかを選択できます**ファイル**または**Server**を評価するポリシー ファイルのソースとして。 クリックすると**Server**、ローカルまたはリモート サーバー上のポリシー ベースの管理に以前インポートされたすべてのベスト プラクティス ポリシーのオンデマンドで評価を行うことができます。 このチュートリアルをクリックして**ファイル**、し評価する個々 のポリシー ファイルを選択します。 これを行うには、次の手順を実行します。  
  
    1.  クリックして**ファイル**します。  
  
    2.  横に**ファイル**、省略記号をクリックします ( **.** ) ボタンをクリックします。  
  
    3.  **ポリシーの選択** ダイアログ ボックスで、ベスト プラクティス ポリシーを格納している次のフォルダーを参照します。  
  
         **ある C:\Program Files (x86) \Microsoft SQL server \110\tools\policies\databaseengine\1033**  
  
        > [!NOTE]  
        >  ファイル パスは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プログラム ファイルのインストール先、32 ビットまたは 64 ビットのどちらのオペレーティング システムを実行しているか、および言語識別子によって異なることがあります。  
  
    4.  クリックして、評価、1 つまたは複数の .xml ポリシー ファイルを選択します。**オープン**します。  
  
         選択したファイルの一覧に表示されます、**ファイル**ボックス。  
  
    5.  **ソースの選択**ダイアログ ボックスで、をクリックして**OK**します。  
  
    6.  場合、**ポリシーを読み込んでいます** ダイアログ ボックスが表示されたら、をクリックして**閉じる**します。  
  
     選択したポリシーが表示されて、**ポリシーの選択**ページ。 ポリシーの横に警告アイコンが表示された場合、そのポリシーにスクリプトが含まれていることを示します。  
  
5.  クリックして**Evaluate**ポリシーを評価します。  
  
     **結果**テーブルの場合は、各ポリシーの結果。 赤い "x" アイコンは、ポリシーに準拠していないことを示しています。  
  
6.  一部のポリシー エラーでは、ポリシー ベースの管理機能によってポリシーへの準拠を対象に直ちに適用できます。 このようなエラーの場合、エラーが発生したポリシーの横にチェック ボックスが表示されます。 チェック ボックスを選択した場合、**適用**ボタンが使用可能になります。 クリックすると**適用**、ターゲット インスタンスで、準拠していない設定を自動的に更新されます。  
  
    > [!CAUTION]  
    >  ポリシー設定を十分に理解してから、対象インスタンスを自動更新してください。 1 つまたは複数のチェック ボックスを選択した後にクリックすることをお勧めします。**スクリプト**、基になるかを確認することができます、出力場所を選択し[!INCLUDE[tsql](../includes/tsql-md.md)]コードの変更を適用する前にします。  
  
7.  ポリシーの詳細な結果を表示するでポリシーをクリックして、**結果**テーブル。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [登録済みサーバーを使用した要求時評価の実行](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
