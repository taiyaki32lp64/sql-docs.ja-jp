---
title: 暗号化キーの復元 (SSRS ネイティブモード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 111e44275922149949cd7e252e112d95cef65076
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952029"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>暗号化キーを復元する (SSRS ネイティブ モード)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、暗号化キーを使用して、レポート サーバー データベースに格納されている機密データのセキュリティを保護します。 暗号化されたデータに継続してアクセスできるようにするには、サービス アカウントの変更のために後で暗号化キーを復元する必要がある場合に備えて、または計画的な移行の一環として、暗号化キーのバックアップを作成することが重要です。 このトピックでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用してキーを復元する方法の概要を示します。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
 キーを復元するには、パスワードで保護されたファイルにキーのバックアップ コピーを保存しておく必要があります。 キーの復元時には、レポート サーバーによって、既存のキーがパスワードで保護されたファイル内のキーに置き換えられます。 ファイル内のキーは、データの暗号化および暗号化解除に使用されるキーと同一である必要があります。  
  
 有効なキーを復元したかどうかを確認するには、レポート マネージャーを使用してサブスクリプションを表示するか、保存されている資格情報を使用するデータ ソースが含まれているレポートを表示します。 サブスクリプション定義ページを開こうとしたときに "レポート サーバーでは暗号化されたデータにアクセスできません" というエラーが表示された場合や、保存されている資格情報をレポート データ ソースに対して使用していたレポートを開く際に、資格情報を入力するように求められた場合は、復元したキーが無効です。  
  
 データの暗号化に使用されたキーとは異なる無効なキーを復元すると、レポート サーバー データベースに現在格納されているデータの暗号化は解除できません。 無効なキーを復元した場合は、正しいキーのバックアップ コピーが使用可能であれば、このコピーをすぐに復元してください。 データの暗号化に使用されたキーのバックアップ コピーがない場合は、すべての暗号化されたデータを削除する必要があります。 削除するには、 **[暗号化キー]** ページの [[削除]](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md) ボタンをクリックします。 暗号化されたコンテンツを削除したら、すべてのサブスクリプションを手動で更新し、レポートに定義されているすべての保存された資格情報とレポート サーバー上のデータ ドリブン サブスクリプションを再指定する必要があります。  
  
## <a name="restore-encryption-key-dialog"></a>[暗号化キーの復元] ダイアログ ボックス  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager の場所の詳細については、 [「 &#40;ネイティブモード&#41;の Reporting Services Configuration Manager](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
 [暗号化キーの復元] ダイアログ ボックスを開くには、 **構成マネージャーのナビゲーション ウィンドウの** [暗号化キー] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をクリックし、 **[復元]** をクリックします。 このダイアログ ボックスは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーの [サービス アカウント] ページを使用してサービス アカウントを更新した場合にも表示されます。 詳細については、次のトピックを参照してください。  
  
## <a name="options"></a>および  
 **ファイルの場所**  
 対称キーのコピーを含むパスワードで保護されたファイルを選択します。 既定のファイル拡張子は .snk です。  
  
 **パスワード**  
 ファイルのロックを解除するパスワードを入力します。 パスワードを知っているユーザーのみがキーを復元できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、強力なパスワード ポリシーが適用されます。 パスワードは 8 文字以上で、大文字と小文字、英数字、および 1 つ以上の記号文字の組み合わせにする必要があります。  
  
## <a name="see-also"></a>参照  
 [Reporting Services Configuration Manager の F1 ヘルプ&#40;トピック SSRS ネイティブ&#41;モード](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services の暗号化キーのバックアップと復元](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [暗号化キーの削除と再作成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [暗号化キー &#40;SSRS ネイティブモード&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
