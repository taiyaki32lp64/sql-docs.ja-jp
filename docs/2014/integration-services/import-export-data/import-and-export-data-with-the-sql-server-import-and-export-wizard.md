---
title: SQL Server インポートおよびエクスポート ウィザード |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f3ce90e2670357d0842b0a6ac7838f396465bab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768167"
---
# <a name="sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザード
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インポートおよびエクスポート ウィザードを作成する最も簡単な方法を提供する[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]先のソースからデータをコピーするパッケージ。  
  
> [!NOTE]  
>  64 ビット コンピューターには、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって 64 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード (DTSWizard.exe) がインストールされます。 ただし、Access や Excel など、一部のデータ ソースは、32 ビット プロバイダーでしか使用できません。 これらのデータ ソースを操作するには、32 ビット版のウィザードをインストールして実行することが必要になる場合があります。 32 ビット版のウィザードをインストールするには、セットアップ中に [クライアント ツール] または [[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]] を選択します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードは、[スタート] メニュー、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、またはコマンド プロンプトから起動できます。 詳細については、次を参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] マネージド データ プロバイダーやネイティブ OLE DB プロバイダーを使用できる任意のデータ ソースとの間でデータをコピーできます。 使用できるプロバイダーの一覧には、次のデータ ソースが含まれます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   フラット ファイル  
  
-   Microsoft Office Access  
  
-   Microsoft Office Excel  
  
 ウィザードの一部の機能は、ウィザードを起動する環境に応じて動作が異なります。  
  
-   開始する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インポートおよびエクスポート ウィザードで[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を選択して、パッケージをすぐに実行する、**をすぐに実行**チェック ボックスをオンします。 既定では、このチェック ボックスがオンになり、パッケージはすぐに実行されます。  
  
     パッケージを保存するかどうかを決定できます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]またはファイル システムにします。 パッケージを保存するように選択した場合は、パッケージの保護レベルを指定する必要もあります。 パッケージの保護レベルの詳細については、次を参照してください。[パッケージ内の機密データのアクセス制御](../security/access-control-for-sensitive-data-in-packages.md)します。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでパッケージを作成してデータをコピーした後、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーを使用して保存したパッケージを開き、タスク、変換、イベント ドリブン ロジックを追加することでパッケージを変更できます。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]、ウィザードによって作成されたパッケージを保存するオプションは使用できません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] プロジェクトから起動する場合、ウィザードを完了する手順としてパッケージを実行することはできません。 代わりに、ウィザードを起動した [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトにパッケージが追加されます。 その後、パッケージを実行するか、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーを使用してタスク、変換、イベント ドリブン手法を追加することにより、パッケージを拡張できます。  
  
 詳細については、次を参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
## <a name="permissions-required-by-the-import-and-export-wizard"></a>インポートおよびエクスポート ウィザードに必要な権限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを正常に完了するには、少なくとも次の権限が必要です。  
  
-   コピー元およびコピー先のデータベースまたはファイル共有に接続する権限。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、サーバーおよびデータベースへのログイン権限が必要です。  
  
-   コピー元のデータベースまたはファイルからデータを読み取る権限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、コピー元のテーブルおよびビューに対する SELECT 権限が必要です。  
  
-   コピー先のデータベースまたはファイルにデータを書き込む権限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、コピー先のテーブルに対する INSERT 権限が必要です。  
  
-   コピー先データベース、テーブル、またはファイルを新しく作成する場合、データベース、テーブル、またはファイルを新しく作成するための十分な権限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、CREATE DATABASE 権限または CREATE TABLE 権限が必要です。  
  
-   Msdb データベースまたはファイル システムに書き込むための十分なアクセス許可と、ウィザードによって作成されたパッケージを保存する場合は。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、Msdb データベースに対する INSERT 権限が必要です。  
  
## <a name="mapping-data-types-in-the-import-and-export-wizard"></a>インポートおよびエクスポート ウィザードのデータ型マッピング  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードには、最小限の変換機能が用意されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでは、列の名前、データ型、およびデータ型プロパティを新しい変換先テーブルおよびファイルに設定できる点を除き、列レベルの変換がサポートされません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] から提供されるマッピング ファイルを使用して、あるデータベース バージョンやシステムから、別のデータベース バージョンやシステムにデータ型をマップします。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から Oracle にマップできます。 既定では、XML 形式のマッピング ファイルは、C:\Program Files\Microsoft SQL Server\100\DTS\MappingFiles にインストールされます。 既定と異なるデータ型間でのマッピングが必要であれば、マッピングの設定を変更して、ウィザードにより実行されるマッピングに適用することができます。 たとえば、する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar**データ型を DB2 にマップする**グラフィック**、DB2 ではなく、データ型**VARGRAPHIC**データ型からデータを転送するときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を変更するには、DB2、 **nchar** SqlClientToIBMDB2.xml マッピング ファイルを使用でマッピング**グラフィック**の代わりに**VARGRAPHIC します。**  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、一般的に使用される変換元と変換先の多数の組み合わせ間でのマッピングが含まれています。さらに新しいマッピング ファイルを Mapping Files ディレクトリに追加して、新たな変換元と変換先をサポートすることもできます。 新しいマッピング ファイルは、公開されている XSD スキーマおよび変換元と変換先の一意の組み合わせ間でのマッピングに準拠する必要があります。  
  
> [!NOTE]  
>  既存のマッピング ファイルを編集するか、新しいマッピング ファイルをフォルダーに追加する場合、新しいファイルか更新したファイルを構成するために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードまたは [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を終了してから再度開く必要があります。  
  
## <a name="external-resources"></a>外部リソース  
  
-   ビデオ、 [Excel (SQL Server ビデオ) への SQL Server データのエクスポート](https://go.microsoft.com/fwlink/?LinkID=200975)、technet.microsoft.com  
  
-   CodePlex サンプル「[へのエクスポート ODBC からフラット ファイルを使用して、ウィザードのチュートリアル。レッスン パッケージ](https://go.microsoft.com/fwlink/?LinkId=217657)、msftisprodsamples.codeplex.com  
  
  
