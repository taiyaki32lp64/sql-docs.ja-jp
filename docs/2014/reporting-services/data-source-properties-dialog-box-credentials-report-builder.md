---
title: データ ソースのプロパティ ダイアログ ボックスで、資格情報 (レポート ビルダー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5dd4d113c92e0a2d094aa02d49010a5dd477c6ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109459"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>[資格情報] ([データ ソースのプロパティ] ダイアログ ボックス) (レポート ビルダー)
  **[データ ソースのプロパティ]** ダイアログ ボックスの **[資格情報]** を選択すると、レポート内の埋め込みデータ ソースに接続するための資格情報を表示および変更できます。 指定した資格情報は、レポートのプレビュー時、データ ソースにアクセスする際に使用されます。 詳細については、「 [レポート ビルダーでの資格情報の指定](../../2014/reporting-services/specify-credentials-in-report-builder.md)」を参照してください。  
  
## <a name="options"></a>および  
 **Windows 認証 (統合セキュリティ) を使用します。**  
 Windows 認証を使用します。  
  
 **このユーザー名とパスワードを使用して、**  
 特定のユーザー名とパスワードを指定します。 埋め込みデータ ソースの場合、レポート サーバー プロジェクトをターゲット サーバーにパブリッシュするときに、データベース用の保存された資格情報としてユーザー名とパスワードが保存されます。 ユーザー名とパスワードを Windows 資格情報として使用する場合は、ターゲット サーバーにパブリッシュされた共有データ ソースのプロパティを変更できます。 詳細については、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ドキュメントの「[共有データ ソースを作成、削除、または変更する (レポート マネージャー)](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)」を参照してください。  
  
 **ユーザー名**  
 データ ソースへのログオンに使用するユーザー名を入力します。  
  
 **Password**  
 データ ソースへのログオンに使用するパスワードを入力します。  
  
 **資格情報のプロンプト**  
 レポートの実行時に資格情報の入力を要求します。  
  
 **プロンプト文字列を入力します。**  
 データ ソースのログイン資格情報を指定するようユーザーに指示する文を入力します。  
  
 **資格情報なし**  
 データ ソースの資格情報を指定しません。 このオプションは、データ ソースで資格情報が不要な場合、または他の方法で資格情報を渡している場合にのみ機能します。  
  
 同じデータ拡張機能から、レポート サーバーで自動実行アカウントを構成する必要があります。  
  
 詳細については、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)の [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ドキュメントの「[外部データ ソースのデータを追加する (SSRS)](report-data/add-data-from-external-data-sources-ssrs.md)」および「[自動実行アカウントの構成 (SSRS 構成マネージャー)](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」で、対応するデータ ソースの種類に関するトピックを参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [[全般] ([データ ソースのプロパティ] ダイアログ ボックス) &#40;レポート ビルダー&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
