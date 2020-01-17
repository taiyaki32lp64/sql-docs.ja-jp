---
title: メンテナンス プラン ([レポートとログ記録] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2905877f907e932be058a07ba3a9fbbd892e7ae6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115696"
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>メンテナンス プラン ([レポートとログ記録] ページ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[レポートとログ記録]** ダイアログ ボックスを使用して、メンテナンス プランを実行したときに生成されるレポートとログを構成できます。  
  
## <a name="options"></a>オプション  
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
  
 **[接続]**  
 リモート サーバーにログを記録するときの接続情報を指定します。  
  
 **[新規作成]**  
 **[接続プロパティ]** ダイアログ ボックスを表示します。 リモート サーバーにログを記録するための新しい接続情報を構成する場合に使用します。  
  
## <a name="see-also"></a>参照  
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [データベース メール](../../relational-databases/database-mail/database-mail.md)  
  
  
