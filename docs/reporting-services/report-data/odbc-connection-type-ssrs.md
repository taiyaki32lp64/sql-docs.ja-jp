---
title: ODBC の接続の種類 (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 24163866-f37a-4c38-982e-c3d79bf64d4c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 11e1f8b080d76dce34b621e79e28a0771431f61c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593975"
---
# <a name="odbc-connection-type-ssrs"></a>ODBC の接続の種類 (SSRS)
  ODBC データ プロバイダーのデータを含めるには、種類が ODBC のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ODBC データ処理拡張機能に基づいています。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、「 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。  
  
##  <a name="Connection"></a> 接続文字列  
 ODBC データ処理拡張機能の接続文字列は、使用する ODBC ドライバーに依存します。 一般的な接続文字列は、ドライバーでサポートされる名前と値のペアで構成されます。 たとえば、次の接続文字列は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の ODBC ドライバーおよび AdventureWorks データベースを指定しています。  
  
```  
Driver={SQL Server Native Client 10.0};Server=server;Database=AdventureWorks;Trusted_Connection=yes;  
```  
  
  
##  <a name="Credentials"></a> [資格情報]  
 クエリの実行、ローカルでのレポートのプレビュー、およびレポート サーバーからのレポートのプレビューには、資格情報が必要です。  
  
 レポートをパブリッシュした後、レポートをレポート サーバーで実行するときに、データを取得するための権限が有効な状態になるように、データ ソースの資格情報を変更する必要が生じる場合があります。  
  
 パスワードを要求したり、接続文字列にパスワードを含めるように ODBC データ ソースを構成し、ユーザーが句読点などの特殊文字を使用してパスワードを入力した場合、基になるデータ ソースのドライバーによってはその特殊文字を検証することができません。 レポートを処理する際に、この問題によって、"パスワードが無効です" というメッセージが表示される場合があります。 パスワードを変更できない場合は、データベース管理者と協力して、適切な資格情報をシステム ODBC データ ソース名 (DSN) の一部としてレポート サーバーに格納することができます。 詳細については、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントの「OdbcConnection.ConnectionString」を参照してください。  
  
> [!NOTE]  
>  パスワードなどのログイン情報を接続文字列に追加しないことをお勧めします。 レポート ビルダーでは、 **[データ ソース]** ダイアログ ボックスに、資格情報の入力に使用できるタブが別に用意されています。  
  
 詳細については、「[データ接続、データソース、および&#40;接続文字列レポートビルダー&#41;と SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 」または「[レポートデータソースに関する資格情報と接続情報の指定](specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
  
##  <a name="Remarks"></a> 解説  
 ODBC は初期のデータ アクセス テクノロジで、その発展形が OLEDB です。 ODBC でサポートされるのはリレーショナル データ ソースだけです。 ODBC データ プロバイダーは *ドライバー*と呼ばれます。 ODBC ドライバーはマイクロソフトとサード パーティ ベンダーによって提供されます。 たとえば、Microsoft Office では、Office ファイル形式に接続する ODBC ドライバーがインストールされます。  
  
 ODBC 接続文字列を作成するには、ODBC ドライバーがインストールされている必要があり、マシン DSN またはシステム DSN を作成しておく必要があります。 目的のデータを正常に取得するには、ドライバーでサポートされるクエリ構文を使用する必要があります。 パラメーターのサポートはドライバーによって異なります。 詳細については、選択するドライバーに応じたトピック (「[SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)」など) を参照してください。  
  
###### <a name="platform-and-version-information"></a>プラットフォームおよびバージョン情報  
 特定の ODBC データプロバイダーの詳細については、「 [ &#40;Reporting Services SSRS&#41;でサポートされるデータソース](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)」を参照してください。
  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 データ接続、データ ソース、およびデータセットを操作する手順について説明します。  
  
 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 関連項目  
 次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義し、カスタマイズし、使用する方法が説明されています。  
  
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
 レポートのデータへのアクセスの概要について説明します。  
  
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 データ接続とデータ ソースについて説明します。  
  
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 埋め込みデータセットと共有データセットについて説明します。  
  
 [データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 クエリによって生成されるデータセット フィールド コレクションについて説明します。  
  
 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。 各データ拡張機能のプラットフォームおよびバージョン サポートに関する詳細な情報です。  
  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
