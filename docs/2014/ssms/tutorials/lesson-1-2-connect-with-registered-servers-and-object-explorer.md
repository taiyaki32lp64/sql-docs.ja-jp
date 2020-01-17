---
title: 登録済みサーバーおよびオブジェクト エクスプローラーを使用した接続 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: d6b3911f-68b4-4483-831b-df89d6400add
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 374d75c18adc091eaf6a01ae1164a529a34accee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636426"
---
# <a name="connect-with-registered-servers-and-object-explorer"></a>登録済みサーバーおよびオブジェクト エクスプローラーを使用した接続
  このチュートリアルでは、登録済みサーバーとオブジェクト エクスプローラーの使用方法について説明します。  
  
 このチュートリアルでは [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを使用します。 セキュリティ強化のため、既定ではサンプル データベースはインストールされません。 詳細については、「 [SQL Server のサンプルとサンプル データベースのインストール](http://sqlserversamples.codeplex.com)」を参照してください。  
  
## <a name="connecting-to-servers"></a>サーバーへの接続  
 [登録済みサーバー] コンポーネントのツール バーには、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、および [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のボタンがあります。 これらの種類のサーバーを 1 つ以上登録しておけば、その後の管理が容易になります。 次の手順で、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを登録してください。  
  
#### <a name="to-register-the-database"></a>データベースを登録するには  
  
1.  [登録済みサーバー] ツール バーの **[データベース エンジン]** をクリックします。 (通常は既に選択されています)。  
  
2.  **[データベース エンジン]** を展開します。  
  
3.  **[ローカル サーバー グループ]** を右クリックし、 **[新規サーバーの登録]** をクリックします。  
  
4.  **[新規サーバーの登録]** ダイアログ ボックスの **[サーバー名]** ボックスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの名前を入力します。  
  
5.  **[登録済みサーバーの名前]** ボックスに「 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]」と入力します。  
  
6.  **接続プロパティ**] タブで、**データベースへの接続**一覧で、[ **\<サーバーの参照 ...> >** します。  
  
7.  **[データベースの参照]** ダイアログ ボックスで、 **[はい]** をクリックします。  
  
8.  **[サーバーでデータベースを参照]** ダイアログ ボックスで、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]を選択して **[OK]** をクリックします。  
  
9. サーバーが正しく登録されていることを確認するには、 **[テスト]** をクリックします。  
  
10. **[新規サーバーの登録]** ダイアログ ボックスで、 **[保存]** をクリックします。  
  
## <a name="connecting-with-object-explorer"></a>オブジェクト エクスプローラーを使用した接続  
 [登録済みサーバー] と同様に、オブジェクト エクスプローラーから [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、および [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]に接続できます。  
  
#### <a name="to-connect-with-object-explorer"></a>オブジェクト エクスプローラーを使用して接続するには  
  
1.  オブジェクト エクスプローラーのツール バーで **[接続]** をクリックし、選択可能な接続の種類の一覧から **[データベース エンジン]** を選択します。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスの **[サーバー名]** ボックスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの名前を入力します。  
  
3.  **[オプション]** をクリックし、選択内容を確認します。  
  
4.  サーバーに接続するため、 **[接続]** をクリックします。 サーバーに既に接続している場合はオブジェクト エクスプローラーが表示され、そのサーバーが強調表示されます。  
  
     オブジェクト エクスプローラーでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント、レプリケーション、およびデータベース メールを管理できます。 このほか、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、および [!INCLUDE[ssIS](../../includes/ssis-md.md)]の一部の機能を管理できます。 これらのコンポーネントには、それぞれ新しい特殊なツールがあります。  
  
5.  オブジェクト エクスプローラーで、 **[データベース]** フォルダーを展開し、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]を選択します。  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、システム データベースが別のフォルダーに表示される点に注意してください。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [環境レイアウトの変更](lesson-1-3-change-the-environment-layout.md)  
  
  
