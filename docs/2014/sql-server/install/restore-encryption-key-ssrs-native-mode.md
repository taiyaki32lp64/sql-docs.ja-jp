---
title: 暗号化キー (SSRS ネイティブ モード) の復元 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9e85f9c17a28ba5c416bcab4853af9bdd823611f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220088"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>暗号化キーを復元する (SSRS ネイティブ モード)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバー データベースに格納されている機密データをセキュリティで保護するのに暗号化キーを使用します。 暗号化されたデータに継続してアクセスできるようにするには、サービス アカウントの変更のために後で暗号化キーを復元する必要がある場合に備えて、または計画的な移行の一環として、暗号化キーのバックアップを作成することが重要です。 このトピックは、使用する方法の概要、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager のキーを復元します。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
 キーを復元するには、パスワードで保護されたファイルにキーのバックアップ コピーを保存しておく必要があります。 キーの復元時には、レポート サーバーによって、既存のキーがパスワードで保護されたファイル内のキーに置き換えられます。 ファイル内のキーは、データの暗号化および暗号化解除に使用されるキーと同一である必要があります。  
  
 有効なキーを復元したかどうかを確認するには、レポート マネージャーを使用してサブスクリプションを表示するか、保存されている資格情報を使用するデータ ソースが含まれているレポートを表示します。 サブスクリプション定義ページを開こうとしたときに "レポート サーバーでは暗号化されたデータにアクセスできません" というエラーが表示された場合や、保存されている資格情報をレポート データ ソースに対して使用していたレポートを開く際に、資格情報を入力するように求められた場合は、復元したキーが無効です。  
  
 データの暗号化に使用されたキーとは異なる無効なキーを復元すると、レポート サーバー データベースに現在格納されているデータの暗号化は解除できません。 無効なキーを復元した場合は、正しいキーのバックアップ コピーが使用可能であれば、このコピーをすぐに復元してください。 データの暗号化に使用されたキーのバックアップ コピーがない場合は、すべての暗号化されたデータを削除する必要があります。 をクリックして、**削除**のボタンでは、[暗号化キー](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)この手順を実行するページ。 暗号化されたコンテンツを削除したら、すべてのサブスクリプションを手動で更新し、レポートに定義されているすべての保存された資格情報とレポート サーバー上のデータ ドリブン サブスクリプションを再指定する必要があります。  
  
## <a name="restore-encryption-key-dialog"></a>[暗号化キーの復元] ダイアログ ボックス  
 検索する場所について、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager を参照してください[Reporting Services 構成マネージャー&#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)します。  
  
 暗号化キーの復元 ダイアログ ボックスを開くには、次のようにクリックします。**暗号化キー**のナビゲーション ウィンドウで、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager、およびクリック**復元**します。 このダイアログ ボックスは、サービス アカウント ページを使用してサービス アカウントを更新するときにも表示されます、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager。 詳細については、次のトピックを参照してください。  
  
## <a name="options"></a>および  
 **ファイルの場所**  
 対称キーのコピーを含むパスワードで保護されたファイルを選択します。 既定のファイル拡張子は .snk です。  
  
 **Password**  
 ファイルのロックを解除するパスワードを入力します。 パスワードを知っているユーザーのみがキーを復元できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 強力なパスワード ポリシーを適用します。 パスワードは 8 文字以上で、大文字と小文字、英数字、および 1 つ以上の記号文字の組み合わせにする必要があります。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services 構成マネージャーの F1 ヘルプ トピック&#40;SSRS ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services の暗号化キーのバックアップと復元](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [暗号化キーの削除と再作成  &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [暗号化キー &#40;SSRS ネイティブ モード&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
