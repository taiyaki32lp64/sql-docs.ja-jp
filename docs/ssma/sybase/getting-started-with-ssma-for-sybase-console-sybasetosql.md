---
title: 概要、SSMA for Sybase Console (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: bad08c06028a64a0423135b15641ebf6fa4e895e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029110"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>概要、SSMA for Sybase Console (SybaseToSQL)
このセクションでは、起動、SSMA for Sybase のコンソール アプリケーションの概要と手順を説明します。 記載されている規則ウィンドウで使用される、一般的な SSMA コンソール出力。  
  
## <a name="launching-the-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソール アプリケーションを起動するのにには、次の手順を使用します。  
  
1.  開始に移動し、すべてのプログラム をポイントします。  
  
2.  をクリックして、 **SQL Server Migration Assistant Sybase コマンド プロンプトの**ショートカット。  
  
    SSMA コンソールの使用状況 メニューを表示および`(/? Help)`、コンソール アプリケーションを使用するためです。  
  
## <a name="using-the-ssma-console"></a>SSMA コンソールの使用  
コンソールは、Windows システムに正常に起動した後は、作業を次の手順を使用できます。  
  
1.  SSMA コンソールは、スクリプト ファイルを構成します。 このセクションの詳細については、次を参照してください。[スクリプト ファイルの作成&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)します。  
  
2.  [変数値ファイルを作成する&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [サーバー接続ファイルを作成する&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [SSMA コンソールの実行&#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)プロジェクトのニーズに基づいて。 
  
追加機能:  
  
1.  [パスワードを指定して](managing-passwords-sybasetosql.md)とエクスポート/インポート、ウィンドウの他のコンピューターにします。  
  
2.  [レポートの生成](generating-reports-sybasetosql.md)詳細な xml を表示するには、評価/変換とデータの移行のためのレポートを出力します。 更新および同期コマンドの詳細なエラー レポートを生成することもできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力の規則  
SSMA スクリプト コマンドとオプションを実行すると、コンソール プログラム、コンソールのユーザーに、結果とメッセージ (情報、エラーなど) を表示します。 または、必要に応じて、xml 出力ファイルにリダイレクトします。 一意の色では、各種のメッセージが出力に表されます。 たとえば、白のカラーにテキスト メッセージがスクリプト ファイルのコマンドを表します緑のカラーで 1 つとユーザーの入力を求めるプロンプトを表します。  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
コンソール出力の色の解釈は、次の表に表示されます。  
  
|色|説明|  
|---------|---------------|  
|[赤]|実行中に致命的なエラー|  
|灰色|日付と時刻スタンプをユーザーに対するメッセージ|  
|White|スクリプト ファイルのコマンド、メッセージの種類|  
|黄|警告|  
|[緑]|ユーザー入力を求めるプロンプト|  
|シアン|開始、終了、および操作の結果|  
  
## <a name="see-also"></a>関連項目  
[SSMA for SAP ASE のインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
