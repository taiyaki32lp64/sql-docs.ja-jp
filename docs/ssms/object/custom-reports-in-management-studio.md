---
title: Management Studio におけるカスタム レポート | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.new.custom.report.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 1ba3f758-f39b-4f5f-91ca-516cedc78979
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f2fd6eb4e5c3c6b50f7fd96a0dd5ff51034d305
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259516"
---
# <a name="custom-reports-in-management-studio"></a>Management Studio におけるカスタム レポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、[!INCLUDE[msCoName](../../includes/msconame_md.md)] で作成された一連の標準レポートが多数のオブジェクト エクスプローラー ノードに表示されます。 これらのレポートは、要求されることの多いサーバー情報を要約表示できるように設計されています。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 以降は、管理者が [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] で作成されたカスタム レポートを [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]から実行できるようになりました。  
  
## <a name="implementation"></a>実装  
カスタム レポートはレポート定義言語 (RDL) を使用して作成し、レポート定義 (.rdl) ファイルとして保存します。 RDL には、レポートのデータ取得情報とレイアウト情報が XML 形式で含まれています。 RDL はオープン スキーマです。 開発者は、属性や要素を追加して RDL を拡張することができます。 レポートは、任意の有効な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントをレポート内で実行できます。  
  
オブジェクト エクスプローラーがサーバーに接続されている場合、オブジェクト エクスプローラーで現在選択されている内容のコンテキストでカスタム レポートを実行できます (ただし、そのノードのレポート パラメーターがレポートで参照されている必要があります)。 これにより、現在のデータベースなど現在のコンテキストをレポートで使用することができます。あるいは、カスタム レポートに含まれている [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに特定のデータベースを使用するなどの形態で、一貫したコンテキストをレポートで使用することもできます。  
  
## <a name="running-a-custom-report"></a>カスタム レポートの実行  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では次の方法でカスタム レポートを実行できます。  
  
-   オブジェクト エクスプローラーでノードを右クリックし、 **[レポート]** をポイントして、 **[カスタム レポート]** を左クリックします。 **[ファイルを開く]** ダイアログ ボックスで .rdl ファイルを含むフォルダーを見つけ、適切なレポート ファイルを開きます。  
  
-   オブジェクト エクスプローラーでノードを右クリックして、 **[レポート]** 、 **[カスタム レポート]** の順にポイントし、最近使用したファイル一覧からカスタム レポートを選択します。  
  
## <a name="limitations"></a>制限事項  
カスタム レポートを操作する場合は、次の制限事項に注意してください。  
  
-   悪意あるコードが誤って実行されないようにするために、ファイル システムで .rdl ファイルが [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] に関連付けられていても、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でレポートの自動実行を構成できないようになっています。 レポートは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] でプログラムから実行することも、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のコマンド ラインから実行することもできません。  
  
-   カスタム レポートは、意図した値が生成されないコンテキストでも実行できます。 たとえば、レプリケーションに関係のないデータベースのコンテキストでレプリケーションに関するレポートを実行することも、正確なレポートの生成に必要な情報にアクセスする権限のないユーザーとしてレポートを実行することもできます。 レポートの構造およびコンテキストの妥当性については、カスタム レポートの作成者が注意する必要があります。  
  
-   カスタム レポートを標準レポートの一覧に追加することはできません。  
  
-   レポートでのコード処理が、サーバーのパフォーマンスに影響することがあります。  
  
-   カスタム レポートではサブレポートがサポートされません。  
  
-   レポート内の各クエリのコマンド テキストを式で定義しないでください。  
  
-   コマンド (クエリ) で使用されるクエリ パラメーターでは、1 つのレポート パラメーターのみを参照でき、式演算子は使用できません。  
  
-   レポート コマンド (クエリ) でサポートされるコマンドの種類は、テキストとストアド プロシージャのみです。  
  
-   レポート フレームワークには、クエリのパラメーター エスケープ機能がありません。 クエリの作成者は、クエリが SQL インジェクション攻撃を受けないことを確認する必要があります。  
  
## <a name="managing-custom-reports"></a>カスタム レポートの管理  
カスタム レポートが多数ある場合は、適切な NTFS ファイル システム権限を持つファイル システム フォルダーを使用してカスタム レポートを整理することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
カスタム レポートは、現在のユーザーの権限を使用して実行されます。 レポートで実行されるクエリが悪意あるユーザーによって変更されないようにするために、レポート ファイルが格納されるファイル システム フォルダーに権限を設定してアクセスを制限する必要があります。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスによって使用されるユーザーとアカウントの両方に、レポート ファイルが格納されるファイル システム フォルダーへの読み取りアクセスが必要です。  
  
レポートには任意の有効な [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] コマンドを埋め込むことができますが、そのコマンドは実行されません。  
  
> [!CAUTION]  
> レポートには任意の有効な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを埋め込み、レポートから実行することができます。 高い特権を持つユーザー アカウントでレポートを実行すると、このように埋め込まれた命令を容易に実行できるようになります。  
  

  
## <a name="see-also"></a>参照  
[Management Studio へのカスタム レポートの追加](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[カスタム レポート実行時の警告の抑制を解除する方法](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[カスタム レポートでのオブジェクト エクスプローラー ノード プロパティの使用](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  
