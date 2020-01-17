---
title: データ ソースのプロパティ ダイアログ ボックスで、資格情報 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.credentials.f1
- "10100"
ms.assetid: 14c3eeb6-d37b-4fda-967b-43afcdb48119
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ed5b58aa9a4fe81a55e602fb61f673bf10059ee7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109458"
---
# <a name="data-source-properties-dialog-box-credentials"></a>[資格情報] ([データ ソースのプロパティ] ダイアログ ボックス)
  **[データ ソースのプロパティ]** ダイアログ ボックスの **[資格情報]** を選択すると、レポート内のデータ ソースに接続するための資格情報を表示および変更できます。 指定した資格情報は、データ ソースへのアクセス、およびレポート プレビュー用のデータのコピーのキャッシュに使用されます。 プレビュー データのキャッシュの方法の詳細については、「 [レポートのプレビュー](reports/previewing-reports.md)」を参照してください。 資格情報の詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
## <a name="options"></a>および  
 **Windows 認証 (統合セキュリティ) を使用します。**  
 Windows 認証を使用します。  
  
 **このユーザー名とパスワードを使用して、**  
 特定のユーザー名とパスワードを指定します。 共有データ ソースの場合、レポート サーバー プロジェクトをターゲット サーバーにパブリッシュするときに、データベース用の保存された資格情報としてユーザー名とパスワードが保存されます。 ユーザー名とパスワードを Windows 資格情報として使用する場合は、ターゲット サーバーにパブリッシュされた共有データ ソースのプロパティを編集できます。 詳細については、「[共有データ ソースを作成、削除、または変更する &#40;レポート マネージャー&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)」を参照してください。  
  
 **ユーザー名**  
 データ ソースへのログインに使用するユーザー名を入力します。  
  
 **Password**  
 データ ソースへのログインに使用するパスワードを入力します。  
  
 **資格情報のプロンプト**  
 レポートの実行時に資格情報の入力を要求します。  
  
 **プロンプト文字列を入力します。**  
 データ ソースのログイン資格情報を指定するようユーザーに指示する文を入力します。  
  
 **資格情報なし**  
 データ ソースの資格情報を指定しません。 このオプションは、データ ソースで資格情報が不要な場合、または他の方法で資格情報を渡している場合にのみ機能します。  
  
## <a name="see-also"></a>参照  
 [データ ソースのプロパティダイアログ ボックスの [全般]](../../2014/reporting-services/data-source-properties-dialog-box-general.md)   
 [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Reporting Services でのデータ接続、データ ソース、および接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
