---
title: Ssma for Access コンソール (AccessToSQL) 作業の開始 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 899070b1405b031e919f50a6d16bc5d6df3adf3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68222220"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Ssma for Access コンソール (AccessToSQL) 作業の開始
このセクションを起動し、Access のコンソール アプリケーションを使用する手順について説明します。 一覧表示、ここで、規則で使用されます SSMA コンソールの一般的な出力ウィンドウ。  
  
## <a name="launching-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソール アプリケーションを起動するのにには、次の手順を使用します。  
  
1.  移動して**開始** をポイント**すべてのプログラム**します。  
  
2.  をクリックして、 **SQL Server Migration Assistant へのアクセス コマンド プロンプトの**ショートカット。  
  
    SSMA コンソールの使用状況 メニューを表示および`(/? Help)`、コンソール アプリケーションを使用するためです。  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA コンソールを使用する手順  
コンソールは、Windows システムに正常に起動した後は、作業を次の手順を使用できます。  
  
1.  SSMA コンソールは、スクリプト ファイルを構成します。 このセクションの詳細については、次を参照してください。[スクリプト ファイルの作成&#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md)します。  
  
2.  [変数値ファイルを作成する&#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [サーバー接続ファイルを作成する&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [SSMA コンソールの実行&#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md)プロジェクトのニーズに基づく  
  
追加機能:  
  
1.  [パスワードを指定して](managing-passwords-accesstosql.md)とエクスポート]、[ウィンドウの他のマシンにインポート  
  
2.  [レポートの生成](generating-reports-accesstosql.md)詳細な xml を表示するには、評価/conversion とデータの移行のためのレポートを出力します。 更新および同期コマンドの詳細なエラー レポートを生成こともできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力の規則  
SSMA スクリプト コマンドとオプションを実行すると、コンソール プログラムは、コンソールのユーザーに、結果とメッセージ (情報、エラーなど) を表示します。 または、必要な場合は、xml 出力ファイルにリダイレクトします。 一意の色では、各種のメッセージが出力に表されます。 たとえば、白のカラーにテキスト メッセージがスクリプト ファイルのコマンドを表します緑のカラーで 1 つとユーザーの入力を求めるプロンプトを表します。  
  
![SSMA コンソールの出力](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA コンソールの出力")  
  
次の表に、コンソール出力の色解釈:  
  
|色|説明|  
|---------|---------------|  
|[赤]|実行中に致命的なエラー|  
|灰色|日付と時刻スタンプをユーザーに対するメッセージ|  
|White|スクリプト ファイルのコマンド、メッセージの種類|  
|黄|警告|  
|[緑]|ユーザー入力を求めるプロンプト|  
|シアン|開始、終了日と操作の結果|  
  
## <a name="see-also"></a>参照  
[SQL Server Migration Assistant for Access をインストールします。](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
