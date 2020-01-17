---
title: 制御フロー パッケージ パーツを使用することによりパッケージ間で制御フローを再利用する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.toolboxcontrolflowtemplate.f1
- sql13.dts.designer.addcopyexistingtemplate.f1
- sql13.dts.designer.addcopyexistingpackagepart.f1
- sql13.dts.designer.packagepart.general.f1
ms.assetid: 1edc91d9-1fab-4fe5-aed3-6f581fe32c18
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2fa693e4e5c8f21b9d8fc8ad02369bff7623b59e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295782"
---
# <a name="reuse-control-flow-across-packages-by-using-control-flow-package-parts"></a>制御フロー パッケージ パーツを使用することによりパッケージ間で制御フローを再利用する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  よく使用される制御フロー タスクまたはコンテナーをスタンドアロン パーツ ファイル (".dtsxp"ファイル) に保存し、それを、制御フロー パッケージ パーツを使用して 1 つまたは複数のパッケージで複数回、再利用します。 この再利用可能性によって、SSIS パッケージの設計と管理を容易に実行できます。  
  
## <a name="create-a-new-control-flow-package-part"></a>新しい制御フロー パッケージ パーツを作成する  
 新しい制御フロー パッケージ パーツを作成するには、ソリューション エクスプ ローラーで **[パッケージ パーツ]** フォルダーを展開します。 **[制御フロー]** を右クリックし、 **[新しい制御フロー パッケージ パーツ]** を選択します。  
  
 ![新しい制御フロー テンプレートを作成する](../integration-services/media/control-flow-templates-create-new.png "新しい制御フロー テンプレートを作成する")  
  
 **[パッケージ パーツ |制御フロー]** フォルダーの下に拡張子 ".dtsxp" を持つ新しいパーツ ファイルが作成されます。 同時に、同じ名前の新しい項目が SSIS ツールボックスに追加されます (ツールボックスの項目は、パーツを含むプロジェクトを Visual Studio で開いた状態でのみ表示されます)。  
  
 ![ツールボックスの制御フロー テンプレート](../integration-services/media/control-flow-templates-in-toolbox.png "ツールボックスの制御フロー テンプレート")  
  
## <a name="design-a-control-flow-package-part"></a>制御フロー パッケージ パーツを設計する  
 パッケージ パーツ エディターを開くには、ソリューション エクスプ ローラーでパーツ ファイルをダブルクリックします。 パーツの設計は、パッケージの場合と同様に行うことができます。  
  
 ![制御フロー テンプレート設計のステップ 1](../integration-services/media/control-flow-template-design-step-1.png "制御フロー テンプレート設計のステップ 1")  
  
 ![制御フロー テンプレート設計のステップ 2](../integration-services/media/control-flow-template-design-step-2.png "制御フロー テンプレート設計のステップ 2")  
  
 制御フロー パッケージ パーツには、次の制限があります。  
  
-   パーツでは、最上位レベルのタスクまたはコンテナーを 1 つしか保持できません。 複数のタスクまたはコンテナーを含める場合は、それらをすべて 1 つのシーケンス コンテナー内に配置します。  
  
-   デザイナーではパーツを直接実行することもデバッグすることもできません。  
  
## <a name="add-an-existing-control-flow-package-part-to-a-package"></a>既存の制御フロー パッケージ パーツをパッケージに追加する  
 現在の Integration Services プロジェクトまたは別のプロジェクト内に保存されたパーツは再利用することができます。  
  
-   現在のプロジェクトの一部であるパーツを再利用するには、ツールボックスから目的のパーツをドラッグ アンド ドロップします。  
  
-   別のプロジェクトの一部であるパーツを再利用するには、 **[既存の制御フロー パッケージ パーツを追加]** コマンドを使用します。  
  
### <a name="drag-and-drop-a-control-flow-package-part"></a>制御フロー パッケージ パーツをドラッグ アンド ドロップする  
 プロジェクト内のパーツを再利用するには、他のタスクやコンテナーと同様にツールボックスからパーツ項目をドラッグ アンド ドロップするだけです。 複数回パーツをパッケージにドラッグ アンド ドロップすることで、パッケージ内の複数の場所でロジックを再利用できます。 現在のプロジェクトの一部であるパーツを再利用するには、この方法を使用します。  
  
 ![パッケージに制御フロー テンプレートを追加する](../integration-services/media/control-flow-templates-add-to-package.png "パッケージに制御フロー テンプレートを追加する")  
  
 ![複数の制御フロー テンプレートが含まれるパッケージ](../integration-services/media/control-flow-templates-in-package.png "複数の制御フロー テンプレートが含まれるパッケージ")  
  
 パッケージを保存すると、パッケージ内にパーツのインスタンスが存在するかどうかが SSIS デザイナーによって確認されます。  
  
-   パッケージ内にパーツ インスタンスが存在する場合は、パーツに関連するあらゆる情報を含めた新しい .dtsx.designer ファイルがデザイナーによって生成されます。  
  
-   パッケージでパーツが使用されない場合、以前にパッケージ用に生成された dtsx.designer ファイル (すなわち、パッケージと同じ名前を持つ dtsx.designer ファイル) はデザイナーによって削除されます。  
  
 ![制御フロー テンプレートが表示されたソリューション エクスプローラー](../integration-services/media/control-flow-templates-in-solution-explorer.png "制御フロー テンプレートが表示されたソリューション エクスプローラー")  
  
### <a name="add-a-copy-of-an-existing-control-flow-package-part-or-a-reference-to-an-existing-part"></a>既存の制御フロー パッケージ パーツのコピーまたは既存のパーツへの参照を追加する  
 ファイル システム内の既存のパーツのコピーをパッケージに追加するには、ソリューション エクスプ ローラーで **[パッケージ パーツ]** フォルダーを展開します。 **[制御フロー]** を右クリックし、 **[既存の制御フロー パッケージ パーツを追加]** を選択します。  
  
 ![メニューから新しい制御フロー テンプレートを追加する](../integration-services/media/control-flow-templates-add-from-menu.png "メニューから新しい制御フロー テンプレートを追加する")  
  
 ![既存テンプレートのコピーの追加ダイアログ ボックス](../integration-services/media/control-flow-templates-add-copy-dialog.png "既存テンプレートのコピーの追加ダイアログ ボックス")  
  
 **[オプション]**  
  
 **パッケージ パーツのパス**  
 パーツ ファイルのパスを入力するか、参照ボタン [...] をクリックして、コピーまたは参照するパーツ ファイル指定します。  
  
 **参照として追加**  
 -   オンにすると、パーツが Integration Services プロジェクトに参照として追加されます。 このオプションは、複数の Integration Services プロジェクトでパーツ ファイルの単一のコピーを参照する場合に選択します。  
  
-   このオプションをオフにすると、パーツ ファイルのコピーはプロジェクトに追加されます。  
  
## <a name="configure-a-control-flow-package-part"></a>制御フロー パッケージ パーツを構成する  
 パッケージの制御フローに制御フロー パッケージ パーツを追加した後で、そのパーツを構成するには、 **[パッケージ パーツの構成]**  ダイアログ ボックスを使用します。  
  
#### <a name="to-open-the-package-part-configuration-dialog-box"></a>[パッケージ パーツの構成] ダイアログ ボックスを開くには  
  
1.  パーツ インスタンスを構成するには、制御フロー内のパーツ インスタンスをダブルクリックします。 または、パーツ インスタンスを右クリックし、 **[編集]** をクリックします。 **[パッケージ パーツの構成]** ダイアログ ボックスが開きます。  
  
2.  パーツ インスタンスのプロパティおよび接続マネージャーを構成します。  
  
### <a name="properties-tab"></a>[プロパティ] タブ  
 **[パッケージ パーツの構成]** ダイアログ ボックスの **[プロパティ]**  タブを使用してパーツのプロパティを指定します。  
  
 ![テンプレートの構成ダイアログ ボックスの [プロパティ] タブ](../integration-services/media/template-configuration-properties-tab.png "テンプレートの構成ダイアログ ボックスの [プロパティ] タブ")  
  
 左側のウィンドウのツリー ビュー階層に、パーツ インスタンスの構成可能なプロパティがすべて一覧表示されます。  
  
-   オフにすると、パーツ インスタンスのプロパティは構成されません。 パーツ インスタンスではプロパティの既定値を使用します。既定値は制御フロー パッケージ パーツで定義されています。  
  
-   オンにすると、入力または選択した値が既定値をオーバーライドします。  
  
 右側のウィンドウのテーブルに構成対象のプロパティが一覧表示されます。  
  
-   **[プロパティのパス]** 。 プロパティのプロパティ パスです。  
  
-   **[プロパティの型]** 。 プロパティのデータ型。  
  
-   **値**。 構成された値です。 この値は既定値をオーバーライドします。  
  
### <a name="connection-managers-tab"></a>[接続マネージャー] タブ  
 パーツ インスタンス用の接続マネージャーのプロパティを指定するには、 **[パッケージ パーツの構成]** ダイアログ ボックスの **[接続マネージャー]**  タブを使用します。  
  
 ![テンプレートの構成 ダイアログ ボックスの [接続マネージャー] タブ](../integration-services/media/template-configuration-connection-managers-tab.png "テンプレートの構成 ダイアログ ボックスの [接続マネージャー] タブ")  
  
 左側のウィンドウのテーブルに、制御フロー パーツで定義されているすべての接続マネージャーが一覧表示されます。 構成する接続マネージャーを選択します。  
  
 右側のウィンドウのリストに、選択した接続マネージャーのプロパティが一覧表示されます。  
  
-   **[設定]** 。 オンの場合、パーツ インスタンスのプロパティが構成されます。  
  
-   **[プロパティ名]** プロパティの名前。  
  
-   **値**。 構成された値です。 この値は既定値をオーバーライドします。  
  
## <a name="delete-a-control-flow-part"></a>制御フロー パーツを削除する  
 パーツを削除するには、ソリューション エクスプローラーで、対象のパーツを右クリックし、 **[削除]** をクリックします。 削除を確認するには **[OK]** を、パーツを削除しないで残すには **[キャンセル]** を選択します。  
  
 プロジェクトからパーツを削除すると、ファイル システムから完全に削除されるため、復元することはできません。  
  
> [!NOTE]  
>  パーツを Integration Services プロジェクトから削除するが、他のプロジェクトではまだ使用する必要がある場合、 **[削除]**  オプションではなく、 **[プロジェクトから削除]** オプションを使用します。  
  
## <a name="package-parts-are-a-design-time-feature-only"></a>パッケージ パーツは設計時専用の機能  
 パッケージ パーツは設計時専用の機能です。 SSIS デザイナーでは、パーツの作成、オープン、保存、および更新のほか、構成の追加またはパッケージ内のパーツ インスタンスの削除を行います。 ただし、SSIS ランタイムではパーツを認識しません。 ここでは、デザイナーでこの分離がどのように実現されるかを示します。  
  
-   デザイナーは、構成されたプロパティを持つパッケージ パーツ インスタンスを ".dtsx.designer" ファイルに保存します。  
  
-   デザイナーは ".dtsx.designer" ファイルを保存すると、さらに、このファイルが参照するパーツからコンテンツを抽出し、パッケージ内のパーツ インスタンスをパーツのコンテンツに置き換えます。  
  
-   最後に、パーツ情報がもはや含まれていないコンテンツが ".dtsx" パッケージ ファイルに再び保存されます。 これは、SSIS ランタイムで実行されるファイルです。  
  
 次の図に、パーツ (".dtsxp" ファイル)、SSIS デザイナー、および SSIS ランタイムの間の関係を示します。  
  
 ![制御フロー テンプレート ファイルとフロー](../integration-services/media/control-flow-templates-intro.png "制御フロー テンプレート ファイルとフロー")  
  
  
