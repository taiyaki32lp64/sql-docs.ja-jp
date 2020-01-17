---
title: Ssma for MySQL コンソール (MySQLToSQL) 作業の開始 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 88cf4716ea02b8c5dbcbd73e9839c6bacfbed10b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075423"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>SSMA for MySQL コンソール入門 (MySQLToSQL)
このセクションを起動し、MySQL のコンソール アプリケーションを使用する手順について説明します。 一覧表示、ここで、規則で使用されます SSMA コンソールの一般的な出力ウィンドウ。  
  
## <a name="launching-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソール アプリケーションを起動するのにには、次の手順を使用します。  
  
1.  移動して**開始** をポイント**すべてのプログラム**します。  
  
2.  をクリックして、 **SQL Server Migration Assistant MySQL コマンド プロンプトの**ショートカット。  
  
    SSMA コンソールの使用状況 メニューを表示および`(/? Help)`、コンソール アプリケーションを使用するためです。  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA コンソールを使用する手順  
コンソールは、Windows システムに正常に起動した後は、作業を次の手順を使用できます。  
  
1.  SSMA コンソールは、スクリプト ファイルを構成します。 このセクションの詳細については、次を参照してください。[スクリプト ファイルの作成&#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-script-files-mysqltosql.md)します。  
  
2.  [変数値ファイルを作成する&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [サーバー接続ファイルを作成する&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [SSMA コンソールの実行&#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)プロジェクトのニーズに基づく  
  
追加機能:  
  
1.  [パスワードをセキュリティで保護する](managing-passwords-mysqltosql.md)とエクスポート]、[ウィンドウの他のマシンにインポート  
  
2.  [レポートの生成](generating-reports-mysqltosql.md)詳細な xml を表示するには、評価/conversion とデータの移行のためのレポートを出力します。 更新および同期コマンドの詳細なエラー レポートを生成こともできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力の規則  
SSMA スクリプト コマンドとオプションを実行すると、コンソール プログラムは、コンソールのユーザーに、結果とメッセージ (情報、エラーなど) を表示します。 または、必要な場合は、xml 出力ファイルにリダイレクトします。 一意の色では、各種のメッセージが出力に表されます。 たとえば、白のカラーにテキスト メッセージがスクリプト ファイルのコマンドを表します緑のカラーで 1 つとユーザーの入力を求めるプロンプトを表します。  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
次の表に、コンソール出力の色解釈:  
  
|色|説明|  
|---------|---------------|  
|[赤]|実行中に致命的なエラー|  
|灰色|日付と時刻スタンプをユーザーに対するメッセージ|  
|White|スクリプト ファイルのコマンド、メッセージの種類|  
|黄|警告|  
|[緑]|ユーザー入力を求めるプロンプト|  
|シアン|開始、終了日と操作の結果|  
  
## <a name="see-also"></a>関連項目  
[SSMA for MySQL のインストール](installing-ssma-for-mysql-mysqltosql.md)  
  
