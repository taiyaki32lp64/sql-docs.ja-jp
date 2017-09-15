---
title: "メンテナンス プラン ([レポートとログ記録] ページ) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bc79574632edb6fa550c81d66c95616a452ddf38
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="maintenance-plan-reporting-and-logging-page"></a>メンテナンス プラン ([レポートとログ記録] ページ)
  **[レポートとログ記録]** ダイアログ ボックスを使用して、メンテナンス プランを実行したときに生成されるレポートとログを構成できます。  
  
## <a name="options"></a>オプション  
 **[テキスト ファイルのレポートを生成する]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でテキスト ファイル レポートを生成するかどうかを指定します。  
  
 **[新しいファイルの作成]**  
 メンテナンス プランの各実行に対して新しいレポート ファイルを作成します。 既定では、このメンテナンス プランが含まれている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをホストするコンピューターにおいて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中に既定のログ フォルダーとして確立されたフォルダー内にレポート ファイルが記述されます。 別のフォルダーを指定するには、フォルダーの完全なパスを **[フォルダー]** テキスト ボックスに入力するか、参照ボタン (**[...]**) をクリックして目的のフォルダーを指定します。  
  
 **[ファイルに追加]**  
 各プラン実行から、 **[ファイル名]** ボックスで指定したファイルにレポートを追加します。 参照ボタンをクリックし、ダイアログ ボックスの一覧からファイルを選択することもできます。  
  
 **[電子メール受信者にレポートを送信する]**  
 メンテナンス プラン実行の結果を電子メールで転送します。 このオプションは、データベース メールが有効で適切に構成されている場合にのみ利用可能です。  
  
 **[エージェント オペレーター]**  
 電子メールの受信者となるエージェント オペレーターを一覧から選択します。 このオプションは、メールが有効で適切に構成されている場合のみ使用できます。  
  
 **[拡張情報をログに記録する]**  
 追加情報をログに含めます。 このオプションを指定することにより、格納されるメンテナンス プラン履歴のサイズが大きくなります。  
  
 **[リモート サーバーにログを記録する]**  
 メンテナンス プランの履歴をリモート サーバーに記録します。  
  
 **接続**  
 リモート サーバーにログを記録するときの接続情報を指定します。  
  
 **新規**  
 **[接続プロパティ]** ダイアログ ボックスを表示します。 リモート サーバーにログを記録するための新しい接続情報を構成する場合に使用します。  
  
## <a name="see-also"></a>参照  
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [データベース メール](../../relational-databases/database-mail/database-mail.md)  
  
  