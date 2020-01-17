---
title: 配置ユーティリティを使用したモデル ソリューションの配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- deploying [Analysis Services], command prompt
- command prompt utilities [SQL Server], Microsoft.AnalysisServices.Deployment
- Microsoft.AnalysisServices.Deployment utility
- Analysis Services deployments, command prompt
ms.assetid: 584f78ac-5f18-41e0-b292-d1949ec05196
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0c17ef5426703a666f3d6763f878da3cb129e75c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075353"
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>配置ユーティリティを使用したモデル ソリューションの配置
   **Microsoft.AnalysisServices.Deployment** ユーティリティを使用すると、コマンド プロンプトから [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Deployment Engine を起動することができます。 入力ファイルとして、このユーティリティは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]プロジェクトを構築することによって生成される XML 出力ファイルを使用します。 この入力ファイルを使用すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの配置をカスタマイズするための変更を容易に行うことができます。 生成された配置スクリプトは直ちに実行することも、今後の配置のために保存することもできます。  
  
## <a name="syntax"></a>構文  
  
```  
  
      Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> 引数  
 *ASdatabasefile*  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置スクリプト (.asdatabase) ファイルが格納されているフォルダーの完全パスを指定します。 プロジェクトを [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]に展開するときに、このファイルが生成されます。 このファイルは、プロジェクトの bin フォルダーに配置されます。 .asdatabase ファイルには、配置されるオブジェクト定義が保存されている場所が含まれています。 指定されない場合、現在のフォルダーが使用されます。  
  
 **/s**  
 このユーティリティをサイレント モードで実行し、ダイアログ ボックスが表示されないようにします。 モードの詳細については、このトピックの後半にある「 [モード](#Modes)」を参照してください。  
  
 *logfile*  
 ログ ファイルの完全パスとファイル名を指定します。 指定したログ ファイルにトレース イベントのログが記録されます。 ログ ファイルが既に存在する場合は、ファイルの内容が置き換えられます。  
  
 **/a**  
 このユーティリティをアンサー モードで実行します。 このユーティリティのウィザード部分での応答はすべて入力ファイルに書き戻されますが、実際には、配置ターゲットに変更が加えられることはありません。  
  
 **/o**  
 このユーティリティを出力モードで実行します。 配置は行われません。ただし、通常は配置ターゲットに送信される XML for Analysis (XMLA) スクリプトが、指定された出力スクリプト ファイルに保存されます。 *output_script_file* が指定されない場合、このユーティリティは、配置オプション (.deploymentoptions) 入力ファイルで指定された出力スクリプト ファイルの使用を試みます。 出力スクリプト ファイルが配置オプション入力ファイルで指定されていない場合は、エラーが発生します。  
  
 モードの詳細については、このトピックの後半にある「 [モード](#Modes)」を参照してください。  
  
 *output_script_file*  
 出力スクリプト ファイルの完全パスとファイル名を指定します。  
  
 **/d**  
 **/o** 引数が使用されている場合は、このユーティリティは対象インスタンスに接続しません。 配置ターゲットへ接続されないため、出力スクリプトは、入力ファイルから取得された情報にのみ基づいて生成されます。  
  
> [!NOTE]  
>  **/d** 引数は、出力モードでのみ使用されます。 この引数は、アンサー モードまたはサイレント モードで指定された場合には無視されます。 モードの詳細については、このトピックの後半にある「 [モード](#Modes)」を参照してください。  
  
## <a name="remarks"></a>コメント  
 **Microsoft.AnalysisServices.Deployment** ユーティリティは、オブジェクト定義、配置ターゲット、配置オプション、および構成設定を提供する一連のファイルを利用し、指定された配置オプションと構成設定を使用して、指定された配置ターゲットへのオブジェクト定義の配置を試みます。 このユーティリティは、アンサー ファイルまたは出力モードで呼び出された場合にはユーザー インターフェイスを提供することができます。 このユーティリティで提供されたユーザー インターフェイスを使用してアンサー ファイルを作成する方法の詳細については、「 [配置ウィザードを使用したモデル ソリューションの配置](deploy-model-solutions-using-the-deployment-wizard.md)」をご覧ください。  
  
 このユーティリティは、\Program files (x86)\Microsoft SQL Server\110\Binn\ManagementStudio フォルダーにあります。  
  
##  <a name="Modes"></a> モード  
 次の表は、このユーティリティを実行できるモードを示しています。  
  
|モード|説明|  
|----------|-----------------|  
|サイレント モード|ユーザー インターフェイスは表示されません。また、配置に必要なすべての情報は入力ファイルによって提供されます。 このユーティリティは、サイレント モードでは進行状況を表示しません。 その代わり、オプションのログ ファイルを使用して進行状況やエラー情報をキャプチャし、後で参照することができます。|  
|アンサー モード|配置ウィザードのユーザー インターフェイスが表示され、後で配置する場合に備えて、指定された入力ファイルにユーザーの応答が保存されます。 アンサー モードでは配置は行われません。 アンサー モードは、ユーザーの応答をキャプチャする場合にのみ使用できます。|  
|出力モード|ユーザー インターフェイスは表示されません。また、配置に必要なすべての情報は入力ファイルによって提供されます。<br /><br /> ただし、サイレント モードと異なり、ユーティリティからの出力は出力スクリプト ファイルに書き込まれ、入力ファイルで指定された配置ターゲットには送信されません。 **/d** 引数が指定されない限り、このユーティリティはそれぞれの配置ターゲットに接続して、出力スクリプト ファイルの生成中にメタデータを比較します。|  
  
 [引数に戻る](#Arguments)  
  
## <a name="examples"></a>使用例  
 次の例では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトをサイレント モードで配置する方法を紹介します。また後で参照できるように、進行状況とエラー メッセージのログを記録します。  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>関連項目  
 [コマンド プロンプト ユーティリティ リファレンス &#40;データベース エンジン&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
