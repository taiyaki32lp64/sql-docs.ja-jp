---
title: Integration Services の開発者向けのドキュメント | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9fdcc10cd21714681578489fd1c71db607226086
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284394"
---
# <a name="integration-services-developer-documentation"></a>Integration Services の開発者向けのドキュメント

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、完全に再記述されたオブジェクト モデルが含まれています。それは、多数の機能で強化されています。この結果、パッケージのプログラミングや拡張作業は、より簡単に、柔軟に、また強力に行えるようになりました。 開発者は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージのほとんどすべての側面を拡張およびプログラミングできます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の開発者として、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のプログラミングでは、次の 2 つの基本的な方法を採用できます。  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナー内で使用可能になるコンポーネントを記述してパッケージを拡張し、パッケージにカスタム機能を提供できます。  
  
-   開発者独自のアプリケーションから、プログラムでパッケージを作成、構成、および実行することができます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で組み込みコンポーネントが要件を満たしていない場合は、独自の拡張機能をコーディングすることによって [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の機能を拡張できます。 この方法をとる場合、以下のように 2 つの選択肢があります。  
  
-   単一のパッケージで臨時に使用する場合は、スクリプト タスクでコードを記述してカスタム タスクを作成するか、またはスクリプト コンポーネントでコードを記述してカスタム データ フロー コンポーネントを作成し、変換元、変換、あるいは変換先として設定することができます。 これらの強力なラッパーによってインフラストラクチャ コードが自動的に記述されるため、開発者はカスタム機能の開発に集中できます。ただし、他の場所で簡単に再利用することはできません。  
  
-   複数のパッケージで使用する場合は、接続マネージャー、タスク、列挙子、ログ プロバイダー、およびデータ フロー コンポーネントなどの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のカスタム拡張機能を作成できます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のマネージド オブジェクト モデルには、基になる基本クラスが含まれており、従来よりもカスタム拡張機能の開発が簡単になっています。  
  
 パッケージを動的に作成する場合、または開発環境以外で [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを管理および実行する場合は、プログラムでパッケージを操作できます。 既存のパッケージを読み込み、変更し、実行できます。または、まったく新しいパッケージをプログラムで作成および実行することもできます。 この場合、次に示すような一連の方法があります。  
  
-   既存のパッケージを読み込んで、変更せずに実行します。  
  
-   既存のパッケージを読み込み、再構成 (異なるデータ ソースの指定など) してから実行します。  
  
-   新しいパッケージを作成し、コンポーネントを追加および構成後、オブジェクト単位やプロパティ単位で変更し、保存してから実行します。  
  
 ここでは、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のプログラミングに対するこれらの方法について説明し、例を示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Integration Services プログラミングの概要](../integration-services/integration-services-programming-overview.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 開発での制御フローおよびデータ フローの役割について説明します。  
  
 [同期変換と非同期変換について](../integration-services/understanding-synchronous-and-asynchronous-transformations.md)  
 同期出力と非同期出力の重要な相違点、およびデータ フローでこれらの出力を使用するコンポーネントについて説明します。  
  
 [プログラムによる接続マネージャーの操作](../integration-services/working-with-connection-managers-programmatically.md)  
 マネージド コードで使用できる接続マネージャーと、コードが **AcquireConnection** メソッドを呼び出した場合に接続マネージャーが返す値の一覧を表示します。  
  
 [スクリプトによるパッケージの拡張](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 スクリプト タスクを使用した制御フローの拡張方法、またはスクリプト コンポーネントを使用したデータ フローの拡張方法について説明します。  
  
 [カスタム オブジェクトを使用したパッケージの拡張](../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 複数のパッケージで使用するプログラム カスタム タスク、データ フロー コンポーネント、およびその他のパッケージ オブジェクトを作成する方法について説明します。  
  
 [プログラムによるパッケージの作成](../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージをプログラムで作成、構成、および保存する方法について説明します。  
  
 [プログラムによるパッケージの実行と管理](../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージをプログラムで列挙、実行、および管理する方法について説明します。  
  
## <a name="reference"></a>リファレンス  
 [Integration Services のエラーとメッセージのリファレンス](../integration-services/integration-services-error-and-message-reference.md)  
 定義済みの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] エラー コードと、そのシンボル名および説明の一覧を示します。  
  
## <a name="related-sections"></a>関連項目  
 [パッケージ開発のトラブルシューティング ツール](../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
 開発時にパッケージのトラブルシューティングを行うために [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] に用意されている機能とツールについて説明します。  
  
## <a name="external-resources"></a>外部リソース  
  
-   www.codeplex.com/MSFTISProdSamples の CodePlex サンプル「[Integration Services 製品サンプル](https://go.microsoft.com/fwlink/?LinkID=131204)」  
  
## <a name="see-also"></a>参照  
 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
  
  
