---
title: SQL Server エージェントのプロパティ ([警告システム] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.alert.f1
ms.assetid: 3e6d3bfd-20ee-4593-86cc-f65b1c08c69d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00e3643a1beb3f69f8b370715001317e536c42e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245752"
---
# <a name="sql-server-agent-properties-alert-system-page"></a>[SQL Server エージェントのプロパティ] \([警告システム] ページ)
  このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告によって送信されるメッセージの設定を表示および変更できます。  
  
## <a name="options"></a>および  
 **[メール セッション]**  
 このセクションのオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのメールを構成します。  
  
 **[メール プロファイルを有効にする]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのメールを有効にします。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのメールは有効ではありません。  
  
 **[メール システム]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用するメール システムを設定します。 データベース メール  
  
> [!NOTE]  
>  電子メール システムを変更したら、変更内容を有効にするために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを再起動する必要があります。  
  
 **[メール プロファイル]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで使用するプロファイルを設定します。 **[\<新しいデータベース メール プロファイル>]** を選択して新しいプロファイルを作成できます。  
  
 **[ポケットベル メール]**  
 このセクションのオプションを使用すると、ポケットベル アドレスに送信される電子メール メッセージをポケットベル システムに対応させることができます。  
  
 **[ポケットベル メールのアドレス形式]**  
 このセクションでは、アドレスの形式とポケットベル メールに含める件名行を指定できます。  
  
 **[[宛先] 行]**  
 メッセージの **[宛先]** 行のオプションを指定します。  
  
 **プレフィックス**  
 ポケットベルに送信されるメッセージの **[宛先]** 行の先頭に、システムから要求される固定テキストを入力します。  
  
 **ポケットベル**  
 メッセージの電子メール アドレスを、プレフィックスとサフィックスの間に含めます。  
  
 **サフィックス**  
 ポケットベルに送信されるメッセージの **[宛先]** 行の末尾に、ポケットベル システムから要求される固定テキストを入力します。  
  
 **[[CC] 行]**  
 メッセージの **[CC]** 行のオプションを指定します。  
  
 **プレフィックス**  
 ポケットベルに送信されるメッセージの **[CC]** 行の先頭に、システムから要求される固定テキストを入力します。  
  
 **ポケットベル**  
 メッセージの電子メール アドレスを、プレフィックスとサフィックスの間に含めます。  
  
 **サフィックス**  
 ポケットベルに送信されるメッセージの **[CC]** 行の末尾に、ポケットベル システムから要求される固定テキストを入力します。  
  
 **Subject**  
 メッセージの件名のオプションを指定します。  
  
 **Prefix**  
 ポケットベルに送信されるメッセージの **[件名]** 行の先頭に、ポケットベル システムから要求される固定テキストを入力します。  
  
 **サフィックス**  
 ポケットベルに送信されるメッセージの **[件名]** 行の末尾に、ポケットベル システムから要求される固定テキストを入力します。  
  
 **[通知メッセージに電子メールの本文を含める]**  
 ポケットベルに送信されるメッセージに、電子メールの本文を含めます。  
  
 **[緊急時のオペレーター]**  
 このセクションでは、緊急時のオペレーターのオプションを指定できます。  
  
 **[緊急時のオペレーターを有効にする]**  
 緊急時のオペレーターを指定します。  
  
 **[オペレーター]**  
 緊急時の通知を受け取るオペレーターを指定します。  
  
 **[通知方法]**  
 緊急時のオペレーターへの通知方法を設定します。  
  
 **[トークンの置換]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント警告によって実行されるジョブで使用するジョブ ステップ トークンを有効にできます。 ジョブ ステップ トークンの詳細については、「 [ジョブ ステップでのトークンの使用](use-tokens-in-job-steps.md)」をご覧ください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント警告でアクティブになるジョブ ステップには、Windows イベント ログに書き込み権限を持つ任意の Windows ユーザーがアクセスできます。 このセキュリティ上のリスクを避けるために、警告によってアクティブになるジョブで使用できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント トークンは、既定で無効になっています。 無効になっているトークンは、 **$(A-DBN)** 、 **$(A-SVR)** 、 **$(A-ERR)** 、 **$(A-SEV)** 、 **$(A-MSG)** です。  
>   
>  これらのトークンを使用する必要がある場合は、有効にする前に、信頼された Windows セキュリティ グループ (Administrators など) のメンバーだけが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が動作するコンピューターのイベント ログに書き込み権限を持つことを確認してください。  
  
 **[警告に応答するすべてのジョブのトークンを置き換える]**  
 このチェック ボックスをオンにすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってアクティブになるジョブに対してトークンの置換が有効になります。  
  
## <a name="see-also"></a>参照  
 [演算子](operators.md)   
 [データベース メールを使用する SQL Server エージェント メールを構成します。](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)   
 [データベース メール](../../relational-databases/database-mail/database-mail.md)  
  
  
