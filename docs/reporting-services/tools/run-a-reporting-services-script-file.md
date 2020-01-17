---
title: Reporting Services スクリプト ファイルを実行する | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8ad3c0bb7ea7700f457cfaa9e7cb08684624dc73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571534"
---
# <a name="run-a-reporting-services-script-file"></a>Reporting Services スクリプト ファイルを実行する
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] スクリプト ファイルは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] スクリプト環境 (RS.exe) を使用してコマンド プロンプトから実行します。 RS.exe には、ユーザーが使用できるコマンド プロンプト引数が多数用意されています。 コマンド プロンプト オプションの詳細については、「[RS.exe ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)」を参照してください。 他のスクリプトのサンプルについては、「 [SQL Server Reporting Services 製品サンプル](https://go.microsoft.com/fwlink/?LinkId=177889)」を参照してください。  
  
## <a name="sample-command-lines"></a>コマンド ラインでの実行例  
  
-   スクリプト環境で Script.rss を次のように実行すると、ターゲット レポート サーバーが指定されます。 既定では、Windows 認証が適用されます。  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver  
    ```  
  
-   スクリプト環境で Script.rss を次のように実行すると、Web サービスの呼び出しを認証するためのユーザー名とパスワードが指定されます。  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   スクリプト環境で Script.rss を次のように実行すると、30 秒のサーバー タイムアウトが指定されます。  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -l 30  
    ```  
  
-   スクリプト環境で Script.rss を次のように実行すると、 *report*と呼ばれるグローバル スクリプト変数が指定されます。  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -v report="Company Sales"  
    ```  
  
-   スクリプト環境で Script.rss を次のように実行すると、スクリプト ファイルの Web サービス操作がバッチとして実行するように指定されます。  
  
    ```  
    rs -i Script.rss -s https://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>参照  
 [テクニカル リファレンス (SSRS)](../../reporting-services/technical-reference-ssrs.md)  
  
  
