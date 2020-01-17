---
title: メンテナンス プラン ([レポートとログ記録] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 623507b4d9e52da376d4c83e4ee5c4d51b15dc39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186265"
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>メンテナンス プラン ([レポートとログ記録] ページ)
  **[レポートとログ記録]** ダイアログ ボックスを使用して、メンテナンス プランを実行したときに生成されるレポートとログを構成できます。  
  
## <a name="options"></a>および  
 **[テキスト ファイルのレポートを生成する]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でテキスト ファイル レポートを生成するかどうかを指定します。  
  
 **[新しいファイルの作成]**  
 メンテナンス プランの各実行に対して新しいレポート ファイルを作成します。 既定では、このメンテナンス プランが含まれている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをホストするコンピューターにおいて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中に既定のログ フォルダーとして確立されたフォルダー内にレポート ファイルが記述されます。 別のフォルダーを指定するには、フォルダーの完全なパスを **[フォルダー]** テキスト ボックスに入力するか、参照ボタン ( **[...]** ) をクリックして目的のフォルダーを指定します。  
  
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
  
 **Connection**  
 リモート サーバーにログを記録するときの接続情報を指定します。  
  
 **[新規作成]**  
 **[接続プロパティ]** ダイアログ ボックスを表示します。 リモート サーバーにログを記録するための新しい接続情報を構成する場合に使用します。  
  
## <a name="see-also"></a>関連項目  
 [メンテナンス プラン](maintenance-plans.md)   
 [データベース メール](../database-mail/database-mail.md)  
  
  
