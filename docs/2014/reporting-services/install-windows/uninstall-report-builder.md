---
title: レポート ビルダー (レポート ビルダー) のスタンドアロン バージョンのアンインストール |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eeb260942f378eb1e93751fc118f82e67a13d45b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108658"
---
# <a name="uninstall-the-stand-alone-version-of-report-builder-report-builder"></a>スタンドアロン バージョンのレポート ビルダーのアンインストール (レポート ビルダー)
  スタンドアロン バージョンのレポート ビルダーは、コントロール パネルまたはコマンド ラインからアンインストールできます。 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] バージョンのレポート ビルダーをアンインストールするには、[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] をアンインストールする必要があります。  
  
 レポート ビルダーをコマンド ラインからアンインストールする場合に使用する構文は、/i オプションの代わりに /x オプションを使用する以外はレポート ビルダーをインストールする場合と同じです。 /quiet オプションやその他の標準のオプションも使用できます。 レポート ビルダーの Windows インストーラー パッケージ (ReportBuilder3_x86.msi) を削除してしまった場合は、コマンド ラインを使用してレポート ビルダーをアンインストールするのは容易ではありません。 GUID を使用してレポート ビルダーを削除する方法の詳細については、MSDN ライブラリの msiexec プログラムのドキュメントを参照してください。  
  
 レポート ビルダーで使用しているフォルダーにカスタム ファイルが含まれている場合は、レポート ビルダーを削除しても、それらのフォルダーとファイルは削除されません。 レポート ビルダーのファイルのみが削除されます。  
  
### <a name="to-uninstall-report-builder-from-the-control-panel"></a>レポート ビルダーをコントロール パネルからアンインストールするには  
  
1.  **[スタート]** ボタンをクリックし、 **[コントロール パネル]** をクリックします。  
  
2.  コントロール パネルで、 **[プログラムと機能]** をクリックします。  
  
3.  **[名前]** の一覧で、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] レポート ビルダーを見つけてクリックします。  
  
4.  **[アンインストール]** をクリックします。  
  
5.  レポート ビルダーをアンインストールするかどうかを確認するメッセージが表示された場合は、 **[はい]** をクリックします。  
  
### <a name="to-uninstall-report-builder-from-the-command-line"></a>レポート ビルダーをコマンド ラインからアンインストールするには  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
2.  **オープン**テキスト ボックスに「 `cmd.`  
  
3.  コマンド プロンプト ウィンドウで、ReportBuilder3_x86.msi が格納されているフォルダーに移動します。  
  
4.  コマンド ラインに次のように入力します。  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 ログ記録を使用できる場合は、次のようなコマンド ラインを使用します。  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
1.  **Enter**キーを押します。  
  
## <a name="see-also"></a>参照  
 [インストール、アンインストール、およびレポート ビルダーのサポート](../install-uninstall-and-report-builder-support.md)   
 [レポート ビルダーのスタンドアロン バージョンをインストール&#40;レポート ビルダー&#41;](install-report-builder.md)  
  
  
