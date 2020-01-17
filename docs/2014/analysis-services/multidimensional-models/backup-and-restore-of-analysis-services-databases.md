---
title: Analysis Services データベースのバックアップと復元 |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.Backup.f1
- sql12.asvs.ssmsimbi.Restore.f1
helpviewer_keywords:
- backing up databases [Analysis Services]
- encryption [Analysis Services]
- databases [Analysis Services], restoring
- cryptography [Analysis Services]
- databases [Analysis Services], backing up
- restoring databases [Analysis Services]
- recovery [Analysis Services]
ms.assetid: 947eebd2-3622-479e-8aa6-57c11836e4ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f591a5a8c8099e496c10958b43694e98ae7a24b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077027"
---
# <a name="backup-and-restore-of-analysis-services-databases"></a>Analysis Services データベースのバックアップと復元
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] には、特定の時点からデータベースとそのオブジェクトを復旧できるように、バックアップと復元機能が用意されています。 また、バックアップと復元は、アップグレードされたサーバーへのデータベースの移行、サーバー間でのデータベースの移動、実稼働サーバーへのデータベースの配置を行うための有効な方法でもあります。 バックアップ計画をまだ確立しておらず、重要なデータを保持している場合は、データ復旧のために、できるだけ早く計画を作成して実行してください。  
  
 バックアップと復元のコマンドは、配置済みの Analysis Services データベースで実行されます。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のプロジェクトおよびソリューションの場合、ソース管理を使用して特定のバージョンのソース ファイルを復旧できるようにし、使用するソース管理システムのリポジトリのデータ復旧プランを作成する必要があります。  
  
 ソース データを含む完全バックアップでは、詳細データを含むデータベースをバックアップする必要があります。 具体的には、ROLAP または DirectQuery データベース ストレージを使用している場合、詳細データは Analysis Services データベースとは異なる外部の SQL Server リレーショナル データベースに格納されます。 すべてのオブジェクトがテーブルまたは多次元の場合は、Analysis Services バックアップにはメタデータとソース データの両方が含まれます。  
  
 バックアップを自動化する明らかな利点の 1 つは、自動バックアップ頻度の指定に応じて、データのスナップショットが常に最新の状態に保たれることです。 自動スケジューラにより、バックアップの実行漏れはなくなります。 データベースの復元も自動化が可能です。これはデータをレプリケートする場合に適していますが、レプリケート先のインスタンスの暗号化キー ファイルを必ずバックアップする必要があります。 同期機能は [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのレプリケーションに特化していますが、最新でないデータに対してのみ実行されます。 ここで説明する機能はすべて、ユーザー インターフェイス、XML/A コマンド、または AMO 経由でのプログラムの実行によって実装できます。  
  
 このトピックのセクションは次のとおりです。  
  
-   [バックアップの準備](#bkmk_prep)  
  
-   [多次元データベースまたはテーブル データベースのバックアップ](#bkmk_cube)  
  
-   [Analysis Services データベースの復元](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> 前提条件  
 Analysis Services インスタンス上に管理権限を持っている、またはバックアップしようとしているデータベース上に、フル コントロール (管理者) 権限を持っている必要があります。  
  
 復元の場所は、バックアップが作成されたインスタンスと同じバージョン、またはそれよりも新しいバージョンの Analysis Services インスタンスである必要があります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンスから以前のバージョンの Analysis Services にデータベースを復元することはできませんが、新しい [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インスタンスで SQL Server 2012 などの以前のバージョンのデータベースを復元するのはよくあることです。  
  
 復元の場所は、同じサーバーの種類である必要があります。 テーブル データベースは、表形式モードで実行されている Analysis Services にしか復元できません。 多次元データベースには、多次元モードで実行されているインスタンスが必要です。  
  
##  <a name="bkmk_prep"></a> バックアップの準備  
 次のチェック リストに従って、バックアップの準備をします。  
  
-   バックアップ ファイルを格納する場所を確認します。 リモートの場所を使用している場合は、UNC フォルダーとして指定する必要があります。 UNC パスにアクセスできることを確認します。  
  
-   フォルダーの権限を調べて、Analysis Services のサービス アカウントにフォルダーの Read/Write 権限があることを確認してください。  
  
-   ターゲット サーバー上に十分なディスク領域があることを確認してください。  
  
-   同じ名前の既存のファイルを確認してください。 同じ名前のファイルが既に存在する場合、ファイルを上書きするオプションを指定しないと、バックアップは失敗します。  
  
##  <a name="bkmk_cube"></a> 多次元データベースまたはテーブル データベースのバックアップ  
 管理者は [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのサイズにかかわらず、データベースを 1 つの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] バックアップ ファイル (.abf) にバックアップできます。 手順の詳細については、「 [Analysis Services データベースをバックアップする方法 (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) 」と「 [Analysis Services データベースのバックアップの自動化 (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html)」を参照してください。  
  
> [!NOTE]  
>  SharePoint 環境で PowerPivot データ モデルの読み込みとクエリを実行する際に使用される [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] は、SharePoint コンテンツ データベースからそのモデルを読み込みます。 これらのコンテンツ データベースはリレーショナル データベースであり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース エンジン上で動作します。 このため、PowerPivot データ モデルについては、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のバックアップと復元の方法はありません。 SharePoint コンテンツ用のディザスター リカバリー計画がある場合、その計画では、コンテンツ データベースに格納されている PowerPivot データ モデルが対象となります。  
  
 **リモート パーティション**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースにリモート パーティションが含まれている場合は、リモート パーティションもバックアップする必要があります。 リモート パーティションを含むデータベースをバックアップすると、各リモート サーバーのすべてのリモート パーティションが、各リモート サーバーにある 1 つのファイルにそれぞれバックアップされます。 このため、これらのリモート バックアップを各ホスト コンピューター以外の場所に作成する場合は、バックアップ ファイルを指定の記憶域に手動でコピーする必要があります。  
  
 **バックアップ ファイルの内容**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースをバックアップすると、データベース オブジェクトで使用されるストレージ モードに応じて内容が異なるバックアップ ファイルが作成されます。 バックアップ内容が異なる理由は、各ストレージ モードでは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内の異なる情報のセットが格納されるためです。 たとえば、多次元ハイブリッド OLAP (HOLAP) パーティションおよびディメンションでは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの集計とメタデータが格納されますが、リレーショナル OLAP (ROLAP) パーティションおよびディメンションでは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのメタデータのみが格納されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの実際の内容は各パーティションのストレージ モードによって異なるので、バックアップ ファイルの内容も異なります。 次の表では、バックアップ ファイルの内容と、オブジェクトによって使用されるストレージ モードを関連付けています。  
  
|ストレージ モード|バックアップ ファイルの内容|  
|------------------|-----------------------------|  
|多次元 MOLAP パーティションおよびディメンション|メタデータ、ソース データ、および集計|  
|多次元 HOLAP パーティションおよびディメンション|メタデータおよび集計|  
|多次元 ROLAP パーティションおよびディメンション|メタデータ|  
|テーブル インメモリ モデル|メタデータとソース データ|  
|テーブル DirectQuery モデル|メタデータのみ|  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースをバックアップしても、リレーショナル データベースなど、基になるデータ ソースのデータはバックアップされません。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの内容のみがバックアップされます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースをバックアップするときは、次のオプションを選択できます。  
  
-   データベースのバックアップをすべて圧縮するかどうか。 既定ではバックアップは圧縮されます。  
  
-   バックアップ ファイルの内容を暗号化し、ファイルの復号化および復元の前にパスワードの入力を求めるかどうか。 既定ではバックアップ データは暗号化されません。  
  
    > [!IMPORTANT]  
    >  バックアップ ファイルごとに、バックアップ コマンドを実行するユーザーは、各ファイルに指定されたバックアップ場所に対する書き込み権限を持っている必要があります。 また、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのサーバー ロールのメンバーであるか、バックアップするデータベースに対してフル コントロール (管理者) 権限を持つデータベース ロールのメンバーであることが条件となります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのバックアップの詳細については、「 [バックアップ オプション](backup-options.md)」 (Backup Options) を参照してください。  
  
##  <a name="bkmk_restore"></a> Analysis Services データベースの復元  
 管理者は、1 つまたは複数のバックアップ ファイルから [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを復元できます。  
  
> [!NOTE]  
>  バックアップ ファイルが暗号化されている場合は、そのファイルを使用して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを復元する前に、バックアップ時に指定したパスワードを入力する必要があります。  
  
 復元時には、次のオプションを選択できます。  
  
-   データベースは元のデータベース名で復元することも、新しいデータベース名を指定することもできます。  
  
-   既存のデータベースは上書きできます。 データベースを上書きする場合は、既存のデータベースを上書きすることを明示的に指定する必要があります。  
  
-   既存のセキュリティ情報を復元するか、セキュリティ メンバーシップ情報を省略するかを選択できます。  
  
-   復元コマンドを使用して、復元する各パーティションの復元先フォルダーを変更できます。 ローカル パーティションは、データベースの復元先の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに対してローカルな任意のフォルダーに復元できます。 リモート パーティションは、ローカル サーバー以外のサーバーにある任意のフォルダーに復元できます。リモート パーティションをローカルにすることはできません。  
  
    > [!IMPORTANT]  
    >  バックアップ ファイルごとに、復元コマンドを実行するユーザーは、各ファイルに指定されたバックアップ場所から読み取る権限を持っている必要があります。 サーバーにインストールされていない [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを復元する場合、ユーザーは、その [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのサーバー ロールのメンバーであることも必要です。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを上書きするには、ユーザーは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのサーバー ロールのメンバーか、復元するデータベースに対してフル コントロール (管理者) 権限を持つデータベース ロールのメンバーのいずれかである必要があります。  
  
    > [!NOTE]  
    >  既存のデータベースを復元すると、データベースを復元したユーザーは、復元されたデータベースにアクセスできなくなる可能性があります。 バックアップの実行時に、ユーザーがサーバー ロールのメンバー、またはフル コントロール (管理者) 権限を持つデータベース ロールのメンバーではなかった場合、このようにアクセスできなくなることがあります。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの復元の詳細については、「 [復元オプション](restore-options.md)」 (Restore Options) を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベースのバックアップ、復元、および同期 &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   
 [Analysis Services PowerShell](../analysis-services-powershell.md)  
  
  
