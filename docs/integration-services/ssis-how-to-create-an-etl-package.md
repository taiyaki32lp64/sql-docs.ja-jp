---
title: SSIS ETL パッケージを作成する方法 | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9a36d403867699a02adfec0d04c9db4efa803514
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281889"
---
# <a name="ssis-how-to-create-an-etl-package"></a>SSIS ETL パッケージを作成する方法

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



このチュートリアルでは、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用して、簡単な [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを作成する方法を学習します。 作成するパッケージは、フラット ファイルからデータを取得し、そのデータを変換した後で、ファクト テーブルに挿入します。 以降のレッスンでは、このパッケージを拡張して、ループ、パッケージ構成、ログ記録、およびエラー フローについて学習します。  
  
チュートリアルで使用するサンプル データをインストールすると、チュートリアルの各レッスンで作成するパッケージの完了した状態のバージョンもインストールされます。 完了した状態のパッケージを使用すれば、手順をとばし、後のレッスンからチュートリアルを開始することができます。 このチュートリアルでパッケージまたは新しい開発環境を初めて使用する場合は、レッスン 1 から開始することをお勧めします。  

## <a name="what-is-sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS) とは

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) は、データ ウェアハウスの ETL (抽出、変換、読み込み) パッケージなど、パフォーマンスの高いデータ統合ソリューションを構築するためのプラットフォームです。 SSIS には、パッケージをビルドしてデバッグするためのグラフィカルなツールやウィザード、ワークフロー機能 (FTP 操作など) や SQL ステートメントを実行したり電子メール メッセージを送信したりするためのタスク、データの抽出や読み込みに使用するデータの抽出元と抽出先、データをクリーニング、集計、マージ、コピーするための変換、パッケージの実行と保存を管理するための管理データベース (`SSISDB`)、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクト モデルをプログラミングするための API (アプリケーション プログラミング インターフェイス) が用意されています。  

## <a name="what-you-learn"></a>学習する内容  
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の新しいツール、コントロール、機能などに慣れる最良の方法は、実際に使ってみることです。 このチュートリアルでは、[!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用して、ループ、構成、エラー フロー ロジック、およびログの記録を含む簡単な ETL パッケージを作成します。  
  
## <a name="prerequisites"></a>Prerequisites  
このチュートリアルは、データベースの基本的な操作を理解している一方で、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]の新機能にはほとんど触れたことがないユーザーを対象にしています。  

このチュートリアルを実行するには、次のコンポーネントがインストールされている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]の両方で使用できます。 SQL Server と SSIS のインストールについては、「[Integration Services のインストール](install-windows/install-integration-services.md)」をご覧ください。

-   **AdventureWorksDW2012** サンプル データベース。 **AdventureWorksDW2012** データベースをダウンロードするには、[AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)から `AdventureWorksDW2012.bak` をダウンロードし、バックアップを復元します。  

-   **サンプル データ** ファイル。 このサンプル データは、 [!INCLUDE[ssIS](../includes/ssis-md.md)] のレッスン パッケージに含まれています。 サンプル データとレッスン パッケージを ZIP ファイルとしてダウンロードする場合は、[SQL Server Integration Services のチュートリアル ファイル](https://www.microsoft.com/download/details.aspx?id=56827)に関するページを参照してください。

    - Zip ファイル内のファイルのほとんどは、意図しない変更を回避するために読み取り専用になっています。 ファイルに出力を書き込んだり、ファイルを変更したりするには、ファイルのプロパティで読み取り専用属性をオフにする必要がある場合があります。
    - サンプル パッケージでは、データ ファイルがフォルダー `C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Creating a Simple ETL Package` 内にあることが想定されています。 ダウンロードしたファイルを別の場所に解凍する場合は、サンプル パッケージの複数の場所でファイル パスを更新する必要がある場合があります。

## <a name="lessons-in-this-tutorial"></a>このチュートリアルで行うレッスン  
[レッスン 1:SSIS によるプロジェクトと基本パッケージの作成](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
このレッスンでは、簡単な ETL パッケージを作成します。パッケージの内容は、1 つのフラット ファイルからデータを抽出し、参照変換を使用してデータを変換し、最後に結果をファクト テーブルの変換先に読み込ませるというものです。  
  
[レッスン 2:SSIS でのループの追加](../integration-services/lesson-2-adding-looping-with-ssis.md)  
このレッスンでは、レッスン 1 で作成したパッケージを拡張し、新しいループ機能を活用して、複数のフラット ファイルを単一のデータ フロー プロセスに抽出します。  
  
[レッスン 3:SSIS でのログ記録の追加](../integration-services/lesson-3-add-logging-with-ssis.md)  
このレッスンでは、レッスン 2 で作成したパッケージを拡張し、新しいログ機能を活用します。  
  
[レッスン 4:SSIS でエラー フロー リダイレクションを追加する](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
このレッスンでは、レッスン 3 で作成したパッケージを拡張し、新しいエラー出力構成を活用します。  
  
[レッスン 5: パッケージ配置モデルの SSIS パッケージ構成を追加する](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
このレッスンでは、レッスン 4 で作成したパッケージを拡張し、新しいパッケージ構成オプションを活用します。  
  
[レッスン 6:SSIS でプロジェクト配置モデルを持つパラメーターを使用する](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
このレッスンでは、レッスン 5 で作成したパッケージを拡張し、プロジェクト配置モデルで新しいパラメーターを使用します。  
  
  
  
