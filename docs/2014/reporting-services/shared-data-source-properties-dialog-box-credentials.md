---
title: 共有データ ソースのプロパティ ダイアログ ボックスは、資格情報 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shareddatasource.credentials.f1
ms.assetid: c08d1a5f-206b-4d53-ab1a-368b651ee5bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cf21cc35bb41837b65d2a2b3c2c946ffae34864f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101259"
---
# <a name="shared-data-source-properties-dialog-box-credentials"></a>[資格情報] ([共有データ ソース プロパティ] ダイアログ ボックス)
  **[共有データ ソース プロパティ]** ダイアログ ボックスの **[資格情報]** を選択すると、レポート内の共有データ ソースに接続するための資格情報を表示および変更できます。 指定した資格情報は、データ ソースへのアクセス、およびレポート プレビュー用のデータのコピーのキャッシュに使用されます。 プレビュー データのキャッシュの方法の詳細については、「 [レポートのプレビュー](reports/previewing-reports.md)」を参照してください。 資格情報の詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
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
 [データ接続、データ ソース、および Reporting Services の接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [レポート データ ソースに関する資格情報と接続情報を指定する](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [[全般] ([共有データ ソース プロパティ] ダイアログ ボックス)](../../2014/reporting-services/shared-data-source-properties-dialog-box-general.md)  
  
  
