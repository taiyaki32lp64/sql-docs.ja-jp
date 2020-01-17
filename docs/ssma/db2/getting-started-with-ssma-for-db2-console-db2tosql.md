---
title: Ssma for DB2 コンソール (DB2ToSQL) 作業の開始 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f245c017-023e-4880-8721-8908d339525e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: fbb0a90d9cfd628e9251a55de3df8b66a22f1ef7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989658"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>Ssma for DB2 コンソール (DB2ToSQL) 作業の開始
このセクションを起動し、DB2 のコンソール アプリケーションを使用する手順について説明します。 一覧表示、ここで、規則で使用されます SSMA コンソールの一般的な出力ウィンドウ。  
  
## <a name="launching-ssma-console"></a>SSMA コンソールの起動  
SSMA コンソール アプリケーションを起動するのにには、次の手順を使用します。  
  
1.  移動して**開始** をポイント**すべてのプログラム**します。  
  
2.  をクリックして、  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant DB2 コマンド プロンプトの**ショートカット。  
  
    SSMA コンソールの使用状況 メニューを表示および`(/? Help)`、コンソール アプリケーションを使用するためです。  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA コンソールを使用する手順  
コンソールは、Windows システムに正常に起動した後は、作業を次の手順を使用できます。  
  
1.  SSMA コンソールは、スクリプト ファイルを構成します。 このセクションの詳細については、次を参照してください。[スクリプト ファイルの作成&#40;DB2ToSQL&#41; ](../../ssma/db2/creating-script-files-db2tosql.md)します。  
  
2.  [変数値ファイルを作成する&#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [サーバー接続ファイルを作成する&#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [SSMA コンソールの実行&#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md)プロジェクトのニーズに基づく  
  
追加機能:  
  
1.  [パスワードの管理](https://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94)とエクスポート]、[ウィンドウの他のマシンにインポート  
  
2.  [レポートを生成する](https://msdn.microsoft.com/69ef5fd9-190d-4c58-8199-b3f77d5e1883)詳細な xml を表示するには、評価/conversion とデータの移行のためのレポートを出力します。 更新および同期コマンドの詳細なエラー レポートを生成こともできます。  
  
## <a name="ssma-console-output-conventions"></a>SSMA コンソールの出力の規則  
SSMA スクリプト コマンドとオプションを実行すると、コンソール プログラムは、コンソールのユーザーに、結果とメッセージ (情報、エラーなど) を表示します。 または、必要な場合は、xml 出力ファイルにリダイレクトします。 一意の色では、各種のメッセージが出力に表されます。 たとえば、白のカラーにテキスト メッセージがスクリプト ファイルのコマンドを表します緑のカラーで 1 つとユーザーの入力を求めるプロンプトを表します。  
  
![Ssmaconsoleoutput_oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "ssmaconsoleoutput_oracle")  
  
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
[SSMA for DB2 のインストール](https://msdn.microsoft.com/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
