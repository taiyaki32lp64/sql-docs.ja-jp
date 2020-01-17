---
title: CLR データベースオブジェクトの配置 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- deployment script [CLR integration]
- common language runtime [SQL Server], deploying
- deploying assemblies [CLR integration]
- deploying [CLR integration]
ms.assetid: 00752573-3367-41a7-af98-7b7a29e8e2f2
author: rothja
ms.author: jroth
ms.openlocfilehash: e82705236ec04c5618a4b43526078a6c218ceef9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908680"
---
# <a name="deploying-clr-database-objects"></a>CLR データベース オブジェクトの配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  配置は、完了したアプリケーションまたはモジュールを別のコンピューターにインストールし、実行するために配布するプロセスです。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio を使用して、共通言語ランタイム (CLR) データベース オブジェクトを開発し、これらをテスト サーバーに配置することができます。 また、Visual Studio ではなく [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework の再配布ファイルを使用して、マネージド データベース オブジェクトをコンパイルすることも可能です。 コンパイルすると、CLR データベース オブジェクトを含むアセンブリを、Visual Studio または [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、テスト サーバーに配置することができます。 Visual Studio .NET 2003 は、CLR 統合プログラミングまたは配置には使用できない点に注意してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には .NET Framework がプレインストールされていますが、Visual Studio .NET 2003 では .NET Framework 2.0 アセンブリを使用できません。  
  
 CLR メソッドをテスト サーバーでテストおよび検証すると、配置スクリプトを使用してこれらを実稼働サーバーに配布できます。 配置スクリプトは手動で生成するか、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して生成することができます (後に示す手順を参照)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、既定で CLR 統合機能は無効になっており、CLR アセンブリを使用するには、これを有効にする必要があります。 詳細については、「 [CLR 統合の有効化](../../relational-databases/clr-integration/clr-integration-enabling.md)」を参照してください。  
  
## <a name="deploying-the-assembly-to-the-test-server"></a>テスト サーバーへのアセンブリの配置  
 Visual Studio を使用し、CLR 関数、プロシージャ、トリガー、ユーザー定義型 (UDT)、またはユーザー定義集計 (UDA) を開発したり、これらをテスト サーバーに配置することができます。 これらのマネージド データベース オブジェクトは、.NET Framework 再配布ファイルに含まれる csc.exe や vbc.exe などのコマンド ライン コンパイラによりコンパイルすることもできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド データベース オブジェクトを開発するのに、Visual Studio 統合開発環境は必要ありません。  
  
 すべてのコンパイラ エラーおよび警告が解決されていることを確認してください。 これで、Visual Studio または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントを使用して、CLR ルーチンを含むアセンブリを [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースに登録できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visual Studio を使用してリモートで開発およびデバッグを行うには、[!INCLUDE[msCoName](../../includes/msconame-md.md)] インスタンスで TCP/IP ネットワーク プロトコルを有効にする必要があります。 サーバーで TCP/IP プロトコルを有効にする方法の詳細については、「[クライアントプロトコルを構成する](../../database-engine/configure-windows/configure-client-protocols.md)」を参照してください。  
  
#### <a name="to-deploy-the-assembly-using-visual-studio"></a>Visual Studio を使用してアセンブリを配置するには  
  
1.  **ビルド メニュー**の **ビルド**\<プロジェクト名 > を選択して、プロジェクトをビルドします。  
  
2.  アセンブリをテスト サーバーに配置する前に、すべてのビルド エラーおよび警告を解決します。  
  
3.  **[ビルド]** メニューの **[配置]** をクリックします。 これで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロジェクトを最初に Visual Studio で作成したときに指定したデータベース内にアセンブリが登録されます。  

#### <a name="to-deploy-the-assembly-using-transact-sql"></a>Transact-SQL を使用してアセンブリを配置するには  
  
1.  .NET Framework に含まれるコマンド ライン コンパイラを使用して、ソース ファイルからアセンブリをコンパイルします。  
  
2.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# ソース ファイルの場合は、次のコマンドを実行します。  
  
3.  `csc /target:library C:\helloworld.cs`  
  
4.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ソース ファイルの場合は、次のコマンドを実行します。  
  
 `vbc /target:library C:\helloworld.vb`  
  
 これらのコマンドは、 C# **/target**オプションを使用してライブラリ DLL のビルドを指定し、ビジュアルまたは Visual Basic コンパイラを起動します。  
  
1.  アセンブリをテスト サーバーに配置する前に、すべてのビルド エラーおよび警告を解決します。  
  
2.  テスト サーバーで [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開きます。 適切なテスト データベース (AdventureWorks など) に接続して、新しいクエリを作成します。  
  
3.  次の [!INCLUDE[tsql](../../includes/tsql-md.md)] をクエリに追加することにより、サーバーにアセンブリを作成します。  
  
 `CREATE ASSEMBLY HelloWorld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE;`  
  
1.  次に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに、プロシージャ、関数、集計、ユーザー定義型、またはトリガーを作成する必要があります。 **Helloworld**アセンブリに**helloworld**という名前のメソッドが**Procedures**クラスに含まれている場合は、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] をクエリに追加して、 **hello** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]というプロシージャを作成できます。  
  
 `CREATE PROCEDURE hello`  
  
 `AS`  
  
 `EXTERNAL NAME HelloWorld.Procedures.HelloWorld`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのさまざまな種類の管理されたデータベースオブジェクトの作成の詳細については、「 [Clr ユーザー定義関数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)」、「Clr[ユーザー定義集計](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)」、「clr ユーザー定義[型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)」、「clr[ストアドプロシージャ](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)」、および「clr」を参照してください。 [トリガー](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)。  
  
## <a name="deploying-the-assembly-to-production-servers"></a>実稼働サーバーへのアセンブリの配置  
 CLR データベース オブジェクトをテスト サーバーでテストおよび検証した後は、実稼働サーバーに配布できます。 マネージデータベースオブジェクトのデバッグの詳細については、「 [CLR データベースオブジェクトのデバッグ](../../relational-databases/clr-integration/debugging-clr-database-objects.md)」を参照してください。  
  
 マネージド データベース オブジェクトの配置は、通常のデータベース オブジェクト (テーブル、[!INCLUDE[tsql](../../includes/tsql-md.md)] ルーチンなど) の配置と似ています。 CLR データベース オブジェクトを含むアセンブリは、配置スクリプトを使用して別のサーバーに配置できます。 配置スクリプトは、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の "スクリプトの生成" 機能を使用して作成できます。 配置スクリプトは、手動で作成することも、また、"スクリプトの生成" を使用して作成した後に手動で変更することもできます。 配置スクリプトの作成後は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスでこれを実行し、マネージド データベース オブジェクトを配置することができます。  
  
#### <a name="to-generate-a-deployment-script-using-generate-scripts"></a>"スクリプトの生成" 機能を使用して配置スクリプトを生成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開き、配置するマネージド アセンブリまたはデータベース オブジェクトを登録する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
2.  **オブジェクトエクスプローラー**で、[ **\<サーバー名 >** および**データベース**] ツリーを展開します。 マネージデータベースオブジェクトが登録されているデータベースを右クリックし、 **[タスク]** 、 **[スクリプトの生成]** の順に選択します。 スクリプト作成ウィザードが開きます。  
  
3.  リストボックスからデータベースを選択し、 **[次へ]** をクリックします。  
  
4.  **[スクリプトオプションの選択]** ウィンドウで **[次へ]** をクリックするか、オプションを変更して **[次へ]** をクリックします。  
  
5.  **[オブジェクトの種類の選択]** ペインで、配置するデータベースオブジェクトの種類を選択します。 **[次へ]** をクリックします。  
  
6.  **[オブジェクトの種類の選択]** ペインで選択したオブジェクトの種類ごとに、 **[\<の種類の選択] >** ペインが表示されます。 このペインでは、指定したデータベースに登録されているデータベース オブジェクトの種類のすべてのインスタンスから、いずれかのオブジェクトを選択できます。 1つまたは複数のオブジェクトを選択し、 **[次へ]** をクリックします。  
  
7.  必要なデータベースオブジェクトの種類がすべて選択されると、 **[出力オプション]** ウィンドウが表示されます。 [**スクリプトをファイルに**作成] を選択し、スクリプトのファイルパスを指定します。 **[次へ]** を選択します。 選択内容を確認し、 **[完了]** をクリックします。 配置スクリプトが指定したファイル パスに保存されます。  
  
## <a name="post-deployment-scripts"></a>配置後スクリプト  
 配置後スクリプトの実行が可能です。  
  
 配置後スクリプトを追加するには、Visual Studio のプロジェクト ディレクトリに postdeployscript.sql というファイルを追加します。 たとえば、**ソリューションエクスプローラー**でプロジェクトを右クリックし、 **[既存項目の追加]** を選択します。 ファイルは、Test Scripts フォルダーではなく、プロジェクトのルートに追加してください。  
  
 [配置] をクリックすると、プロジェクトの配置後に、このスクリプトが Visual Studio によって実行されます。  
  
## <a name="see-also"></a>「  
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
