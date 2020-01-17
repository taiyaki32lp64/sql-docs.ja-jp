---
title: パッケージ開発のトラブルシューティング ツール | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 41dd248c-dab3-4318-b8ba-789a42d5c00c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38c5c4daa65542dd8da14fa5c51a1b964a271fff
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296503"
---
# <a name="troubleshooting-tools-for-package-development"></a>パッケージ開発のトラブルシューティング ツール

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でパッケージを開発する際にトラブルシューティングを実行できる機能とツールが用意されています。  
  
## <a name="troubleshooting-design-time-validation-issues"></a>デザイン時検証問題のトラブルシューティング  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の現在のリリースでは、パッケージが開かれるときに、システムは、すべてのデータ フロー コンポーネントを検証する前にすべての接続を検証し、低速または使用不能の接続を、オフラインで動作するように設定します。 これにより、パッケージのデータ フローを検証するときの遅延を減らすことができます。  
  
 パッケージを開いた後でも、 **[接続マネージャー]** 領域の接続マネージャーを右クリックして **[オフライン作業]** をクリックすることにより、接続をオフにできます。 これにより SSIS デザイナーの動作を速くできます。  
  
 オフラインで動作するように設定された接続は、次のいずれかを行うまでオフラインのままになります。  
  
-   SSIS デザイナーの **[接続マネージャー]** 領域で接続マネージャーを右クリックして **[接続のテスト]** をクリックすることにより、接続をテストします。  
  
     たとえば、パッケージが開かれるとき、オフラインで動作するように接続が初期設定されます。 接続文字列を変更して問題を解決し、 **[接続のテスト]** をクリックして接続をテストします。  
  
-   パッケージを開き直すか、またはパッケージが含まれているプロジェクトを開き直します。 パッケージ内のすべての接続に対して検証が再び実行されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、検証エラーを回避するための以下の追加機能が備わっています。  
  
-   **データ ソースが使用できないときは、オフラインで動作するようにすべてのパッケージとすべての接続を設定します**。 **[SSIS]** メニューの **[オフライン作業]** を有効にできます。 **DelayValidation** プロパティとは異なり、 **[オフライン作業]** オプションはパッケージを開く前でも使用できます。 また、 **[オフライン作業]** を有効にしてデザイナーでの操作を高速化し、パッケージを検証するときだけこのオプションを無効にすることもできます。  
  
-   **実行時まで無効なパッケージ要素の DelayValidation プロパティを構成する**。 デザイン時には構成が有効でないパッケージ要素の **DelayValidation** を **True** に設定すると、検証エラーが発生するのを防ぐことができます。 たとえば、SQL 実行タスクが実行時に作成するまで存在しないテーブルを、データ フロー タスクで使用する場合があります。 **DelayValidation** プロパティはパッケージ ベル、またはパッケージに含まれている個別のタスクやコンテナーのレベルで有効にできます。 実行時に同じ検証エラーが発生するのを防ぐため、パッケージを配置するときは、同一パッケージ内の要素についてこのプロパティを **True** に設定しておく必要があります。  
  
     **DelayValidation** プロパティはデータ フロー タスク上で設定できますが、個別のデータ フロー コンポーネントでは設定できません。 個別のデータ フロー コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> プロパティを **false**。 ただし、このプロパティの値が **false**の場合、コンポーネントは外部データ ソースのメタデータに変更が加えられても認識しません。  
  
 検証の発生時に、パッケージによって使用されるデータベース オブジェクトがロックされている場合、検証プロセスが応答しなくなる可能性があります。 このような状況では、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーも応答しなくなります。 検証を再開するには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内の関連するセッションを閉じます。 また、このセクションで説明した設定を使用することによって、この問題を回避することもできます。  
  
## <a name="troubleshooting-control-flow"></a>制御フローのトラブルシューティング  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージの開発時にパッケージの制御フローのトラブルシューティングを行うため、次の機能とツールが用意されています。  
  
-   **タスク、コンテナー、およびパッケージにブレークポイントを設定する**。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに用意されているグラフィカルなツールを使用して、ブレークポイントを設定できます。 ブレークポイントは、パッケージ レベル、またはパッケージに含まれている個々のタスクとコンテナーのレベルで有効にできます。 タスクやコンテナーの中には、ブレークポイントの設定時にブレークの条件を追加設定するものがあります。 たとえば、For ループ コンテナーでは、ループの反復処理を開始するたびに実行を中断するブレーク条件を有効にできます。  
  
-   **デバッグ ウィンドウを使用する**。 ブレークポイントが設定されたパッケージを実行すると、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のデバッグ ウィンドウから、変数の値および状態メッセージにアクセスできるようになります。  
  
-   **[進行状況] タブでの情報のレビュー**。[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]内のパッケージを実行するときに、制御フローに関する追加情報が表示されます。 [進行状況] タブにはタスクとコンテナーが実行順に表示され、パッケージ自体を含め、タスクやコンテナーごとに開始時刻、終了時刻、警告、エラー メッセージが表示されます。  
  
 これらの機能の詳細については、「 [制御フローのデバッグ](../../integration-services/troubleshooting/debugging-control-flow.md)」を参照してください。  
  
## <a name="troubleshooting-data-flow"></a>データ フローのトラブルシューティング  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージの開発時にパッケージのデータ フローのトラブルシューティングを行うため、次の機能とツールが用意されています。  
  
-   **データのサブセットだけを使用してテストする**。 パッケージのデータ フローをデータセットのサンプルだけを使用してトラブルシューティングを行う場合は、比率サンプリング変換または行サンプリング変換を追加して、実行時にインライン データ サンプルを作成できます。 詳細については、「 [比率サンプリング変換](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md) 」と「 [行サンプリング変換](../../integration-services/data-flow/transformations/row-sampling-transformation.md)」を参照してください。  
  
-   **データ ビューアーを使用して、データ フローでのデータの動きを監視する**。 データ ビューアーには、データが変換元から変換を経て変換先へと移動するのに合わせて、データの値が表示されます。 データ ビューアーでは、グリッドにデータを表示できます。 データ ビューアーのデータはクリップボードにコピーして、ファイルや Excel のワークシートに貼り付けることができます。 詳細については、「 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md) でパッケージを開発する際にトラブルシューティングを実行できる機能とツールが用意されています。  
  
-   **エラー出力をサポートするデータ フロー コンポーネントでエラー出力を構成する**。 データ フローの変換元、変換、および変換先の多くで、エラー出力がサポートされています。 データ フロー コンポーネントのエラー出力を構成することによって、エラーが含まれているデータを別の変換先に送ることができます。 たとえば、別のテキスト ファイルに、失敗したデータや切り捨てられたデータをキャプチャできます。 また、データ ビューアーをエラー出力にアタッチしてエラーを引き起こすデータだけを調べることもできます。 デザイン時に、エラー出力でエラーが発生したデータ値をキャプチャできるので、実際のデータを効率的に処理できるパッケージの開発に役立ちます。 他のトラブルシューティング ツールや機能はデザイン時にしか有益ではありませんが、エラー出力は運用環境でも実用的です。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。  
  
-   **処理された行数をキャプチャする**。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでパッケージを実行すると、パスを通過した行数がデータ フロー デザイナーに表示されます。 データがパスを通過する間、この数値は定期的に更新されます。 また、データ フローに行数変換を追加して、最終的な行数を変数に取り込むこともできます。 詳細については、「 [Row Count Transformation](../../integration-services/data-flow/transformations/row-count-transformation.md)」を参照してください。  
  
-   **[進行状況] タブでの情報のレビュー**。[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]内のパッケージを実行するときに、データ フローに関する追加情報が表示されます。 [進行状況] タブには、データ フロー コンポーネントが実行順に表示されます。また、パッケージの各フェーズの進行状況 (パーセント値) や変換先に書き込まれた行数を確認できます。  
  
 これらの機能の詳細については、「 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)」を参照してください。  
  
## <a name="troubleshooting-scripts"></a>トラブルシューティングのスクリプト  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) は、スクリプト タスクおよびスクリプト コンポーネントで使用されるスクリプトを記述する開発環境です。 VSTA には、パッケージの開発時にスクリプトのトラブルシューティングを行えるように、次の機能とツールが用意されています。  
  
-   **スクリプト タスクのスクリプトにブレークポイントを設定する。** VSTA では、スクリプト タスクのスクリプトに対してのみデバッグがサポートされています。 スクリプト タスクに設定したブレークポイントは、パッケージおよびパッケージ内のタスクやコンテナーに設定したブレークポイントと統合されます。したがって、すべてのパッケージ要素をシームレスにデバッグできます。  
  
    > [!NOTE]  
    >  複数のスクリプト タスクを含むパッケージをデバッグする場合、デバッガーは 1 つのスクリプト タスクにあるブレークポイントのみにヒットし、他のスクリプト タスクにあるブレークポイントを無視します。 スクリプト タスクが Foreach ループ コンテナーまたは For ループ コンテナーの一部である場合、デバッガーは、ループの最初の繰り返し後にスクリプト タスクにあるブレークポイントを無視します。  
  
 詳細については、「 [スクリプトのデバッグ](../../integration-services/troubleshooting/debugging-script.md)」を参照してください。 スクリプト コンポーネントをデバッグする方法の推奨事項については、「 [スクリプト コンポーネントのコーディングおよびデバッグ](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)」を参照してください。  
  
## <a name="troubleshooting-errors-without-a-description"></a>説明のないエラーのトラブルシューティング  
 パッケージ開発中、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エラー番号に対応する説明のないエラーが発生した場合は、その説明を「 [Integration Services のエラーおよびメッセージのリファレンス](../../integration-services/integration-services-error-and-message-reference.md)」で確認できます。 現時点では、この一覧にトラブルシューティング情報は含まれていません。  
  
## <a name="see-also"></a>参照  
 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)   
 [データ フロー パフォーマンス機能](../../integration-services/data-flow/data-flow-performance-features.md)  
  
  
