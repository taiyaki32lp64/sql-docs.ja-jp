---
title: スクリプトの生成 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: mathoma
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 800153a20651b649d644fecfeacf11d48958fab8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265452"
---
# <a name="generate-scripts-sql-server-management-studio"></a>スクリプトの生成 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを生成するための 2 つのメカニズムが用意されています。 複数のオブジェクト用のスクリプトは、**スクリプトの生成とパブリッシュ ウィザード**を使用して作成できます。 また、個々のオブジェクトまたは複数のオブジェクト用のスクリプトを、 **オブジェクト エクスプローラー** の **[スクリプト化]** メニューを使用して生成することもできます。  

SQL Server Management Studio (SSMS) を使用してさまざまなオブジェクトのスクリプトを作成する方法の詳細なチュートリアルについては、[チュートリアル:SSMS でのスクリプトの作成](https://docs.microsoft.com/sql/ssms/tutorials/scripting-ssms)に関するページをご覧ください。

  
## <a name="before-you-begin"></a>はじめに  
 要件に最も適したメカニズムを選択します。  
  
###  <a name="GenPubScriptWiz"></a> スクリプトの生成とパブリッシュ ウィザード  
 **スクリプトの生成とパブリッシュ ウィザード** を使用し、多数のオブジェクトの [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを作成できます。 このウィザードでは、データベース内の全オブジェクトのスクリプトを生成することも、選択したオブジェクトのサブセットのスクリプトを生成することもできます。 ウィザードには、権限、照合順序、制約、その他を含めるかどうかなど、スクリプトのさまざまなオプションがあります。 ウィザードの使用方法の詳細については、「 [スクリプトの生成とパブリッシュ ウィザード](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md)」を参照してください。  
  
###  <a name="OEScriptAsMenu"></a> オブジェクト エクスプローラーの [スクリプト化] メニュー  
 **オブジェクト エクスプローラーの [スクリプト化]** メニューを使用し、単一オブジェクト、複数オブジェクト、または単一オブジェクトの複数のステートメントのスクリプトを作成できます。 いずれか 1 つのスクリプト タイプを選択できます。たとえば、オブジェクトの作成、変更、削除を選択できます。 スクリプトは、クエリ エディター ウィンドウ、ファイル、またはクリップボードに保存できます。 スクリプトは Unicode 形式で作成されます。  
  
##  <a name="ScriptSingleObject"></a> 単一のオブジェクトのスクリプトを生成するには  
 **単一のオブジェクトのスクリプトを生成するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、スクリプト化するオブジェクトを含むデータベースを展開します。  
  
3.  オブジェクトのカテゴリを展開します。 たとえば、 **[テーブル]** または **[ビュー]** ノードを展開します。  
  
4.  オブジェクトを右クリックし、 **[\<オブジェクト タイプ をスクリプト化]** をポイントします。たとえば、 **[テーブルをスクリプト化]** をポイントします。  
  
5.  **[CREATE]** または **[ALTER]** などのスクリプト タイプをポイントします。  
  
6.  スクリプトを保存する場所を選択します。 **[新しいクエリ エディター ウィンドウ]** や **[クリップボード]** などを選択します。  

    ![スクリプト タスク](media/generate-scripts-sql-server-management-studio/scripttable.png)
  
  
 **[オブジェクト エクスプローラーの詳細]** ペインを使用し、同じカテゴリに含まれる複数のオブジェクトのスクリプトを生成できます。  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、スクリプト化するオブジェクトを含むデータベースを展開します。  
  
3.  スクリプトを作成するオブジェクトの種類のカテゴリ ノード ( **[テーブル]** ノードなど) を展開します。  
  
4.  **F7** キーを押すか、 **[表示]** メニューの **[オブジェクト エクスプローラーの詳細]** をクリックして、 **[オブジェクト エクスプローラーの詳細]** ペインを開きます。  
  
5.  スクリプトを作成するオブジェクトのいずれかを左クリックします。  
  
6.  Ctrl キーを押しながら、スクリプトを作成する 2 番目のオブジェクトを左クリックします。  
  
7.  選択したオブジェクトのいずれかを右クリックし、 **[\<オブジェクト タイプ をスクリプト化]** をクリックします。  

    ![オブジェクト エクスプローラー](media/generate-scripts-sql-server-management-studio/objectexplorerdetails.png)
  
  
