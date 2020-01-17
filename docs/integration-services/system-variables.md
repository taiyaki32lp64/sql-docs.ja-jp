---
title: システム変数 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], variables
- tasks [Integration Services], variables
- system variables [Integration Services]
- event handlers [Integration Services], variables
- variables [Integration Services], system
ms.assetid: efecd0d4-1489-4eba-a8fe-275d647058b8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c0b29d0e74d25739b72e712080d2f379ae3be437
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296724"
---
# <a name="system-variables"></a>システム変数

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、実行中のパッケージとそのオブジェクトに関する情報を格納する、システム変数のセットが用意されています。 これらの変数は、式およびプロパティ式の内部で使用でき、パッケージ、コンテナー、タスク、およびイベント ハンドラーをカスタマイズできます。  
  
 すべての変数 (システム変数とユーザー定義変数) を SQL 実行タスクが使用するパラメーター バインドで使用して、パラメーターに変数をマップできます。  
  
## <a name="system-variables-for-packages"></a>パッケージ用システム変数  
 次の表では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] がパッケージ用に提供するシステム変数について説明します。  
  
|システム変数|データ型|[説明]|  
|---------------------|---------------|-----------------|  
|**CancelEvent**|Int32|タスクがシグナルを送信して実行を停止する必要があることを示す、Windows イベント オブジェクトへのハンドルです。|  
|**ContainerStartTime**|DateTime|コンテナーの開始時刻です。|  
|**CreationDate**|DateTime|パッケージが作成された日付です。|  
|**CreatorComputerName**|String|パッケージが作成されたコンピューターです。|  
|**CreatorName**|String|パッケージの構築者の名前です。|  
|**ExecutionInstanceGUID**|String|実行中のパッケージのインスタンスの一意識別子です。|  
|**FailedConfigurations**|String|失敗したパッケージ構成の名前。|  
|**IgnoreConfigurationsOnLoad**|Boolean|パッケージを読み込むときにパッケージ構成を無視するかどうかを示します。|  
|**InteractiveMode**|Boolean|パッケージが対話モードで実行されているかどうかを示します。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでパッケージを実行中の場合、このプロパティは **True**に設定されます。 **DTExec** コマンド プロンプト ユーティリティを使用してパッケージを実行中の場合、プロパティは **False**に設定されます。|  
|**LocaleId**|Int32|パッケージで使用するロケールです。|  
|**MachineName**|String|パッケージが実行されているコンピューターの名前です。|  
|**OfflineMode**|Boolean|パッケージがオフライン モードかどうかを示します。 オフライン モードでは、データ ソースへの接続は取得されません。|  
|**PackageID**|String|パッケージの一意識別子です。|  
|**PackageName**|String|パッケージの名前です。|  
|**StartTime**|DateTime|パッケージの実行を開始した時刻です。|  
|**ServerExecutionID**|Int64|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーで実行されるパッケージの実行 ID です。<br /><br /> 既定値はゼロです。 この値が変更されるのは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーで ISServerExec によってパッケージが実行される場合のみです。 子パッケージがある場合は、この値が親パッケージから子パッケージに渡されます。|  
|**UserName**|String|パッケージを開始したユーザーのアカウントです。 ユーザー名は、ドメイン名によって修飾されます。|  
|**VersionBuild**|Int32|パッケージのバージョンです。|  
|**VersionComment**|String|パッケージ バージョンについてのコメント。|  
|**VersionGUID**|String|バージョンの一意識別子です。|  
|**VersionMajor**|Int32|パッケージのメジャー バージョン。|  
|**VersionMinor**|Int32|パッケージのマイナー バージョン。|  
  
## <a name="system-variables-for-containers"></a>コンテナー用システム変数  
 次の表では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] が、For ループ コンテナー、Foreach ループ コンテナー、およびシーケンス コンテナー用に提供するシステム変数について説明します。  
  
|システム変数|データ型|[説明]|コンテナー|  
|---------------------|---------------|-----------------|---------------|  
|**LocaleId**|Int32|コンテナーが使用するロケールです。|For ループ コンテナー<br /><br /> Foreach ループ コンテナー<br /><br /> シーケンス コンテナー|  
  
## <a name="system-variables-for-tasks"></a>タスク用システム変数  
 次の表では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] がタスク用に提供するシステム変数について説明します。  
  
|システム変数|データ型|[説明]|  
|---------------------|---------------|-----------------|  
|**CreationName**|String|タスクの名前です。|  
|**LocaleId**|Int32|タスクが使用するロケールです。|  
|**TaskID**|String|タスク インスタンスの一意識別子です。|  
|**TaskName**|String|タスク インスタンスの名前です。|  
|**TaskTransactionOption**|Int32|タスクが使用するトランザクションのオプションです。|  
  
## <a name="system-variables-for-event-handlers"></a>イベント ハンドラー用システム変数  
 次の表では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] がイベント ハンドラー用に提供するシステム変数について説明します。 すべての変数がすべてのイベント ハンドラーで使用できるわけではありません。  
  
|システム変数|データ型|[説明]|イベント ハンドラー|  
|---------------------|---------------|-----------------|-------------------|  
|**キャンセル**|Boolean|エラー、警告、またはクエリのキャンセルが発生したときに、イベント ハンドラーが実行を停止するかどうかを示します。|OnError イベント ハンドラー<br /><br /> OnWarning イベント ハンドラー<br /><br /> OnQueryCancel イベント ハンドラー|  
|**ErrorCode**|Int32|エラー識別子です。|OnError イベント ハンドラー<br /><br /> OnInformation イベント ハンドラー<br /><br /> OnWarning イベント ハンドラー|  
|**ErrorDescription**|String|エラーの説明。|OnError イベント ハンドラー<br /><br /> OnInformation イベント ハンドラー<br /><br /> OnWarning イベント ハンドラー|  
|**ExecutionStatus**|Boolean|現在の実行ステータスです。|OnExecStatusChanged イベント ハンドラー|  
|**ExecutionValue**|DBNull|実行値です。|OnTaskFailed イベント ハンドラー|  
|**LocaleId**|Int32|イベント ハンドラーが使用するロケールです。|すべてのイベント ハンドラー|  
|**PercentComplete**|Int32|完了済みの作業の割合です。|OnProgress イベント ハンドラー|  
|**ProgressCountHigh**|Int32|OnProgress イベントによって処理される操作の総数を示す、64 ビット値の上位部分です。|OnProgress イベント ハンドラー|  
|**ProgressCountLow**|Int32|OnProgress イベントによって処理される操作の総数を示す、64 ビット値の下位部分です。|OnProgress イベント ハンドラー|  
|**ProgressDescription**|String|進行状況の説明です。|OnProgress イベント ハンドラー|  
|**Propagate**|Boolean|イベントが、上位レベルのイベント ハンドラーに反映されるかどうかを示します。<br /><br /> 注:変数 **Propagate** の値は、パッケージの検証中は無視されます。 子パッケージ内で **Propagate** を **False** に設定しても、イベントは親パッケージに反映されます。|すべてのイベント ハンドラー|  
|**SourceDescription**|String|イベントを発生させたイベント ハンドラー内の実行可能ファイルの説明です。|すべてのイベント ハンドラー|  
|**[SourceID]**|String|イベントを発生させたイベント ハンドラー内の実行可能ファイルの一意識別子です。|すべてのイベント ハンドラー|  
|**[SourceName]**|String|イベントを発生させたイベント ハンドラー内の実行可能ファイルの名前です。|すべてのイベント ハンドラー|  
|**VariableDescription**|String|変数の説明です。|OnVariableValueChanged イベント ハンドラー|  
|**VariableID**|String|変数の一意識別子です。|OnVariableValueChanged イベント ハンドラー|  
  
## <a name="system-variables-in-parameter-bindings"></a>パラメーター バインドにおけるシステム変数  
 パッケージの実行時に、システム変数の値をテーブルに保存すると役立つことがよくあります。 たとえば、テーブルを動的に作成し、このテーブルを作成したパッケージ実行インスタンスの GUID をテーブル列に書き込むパッケージなどです。  
  
 システム変数を使用して、SQL 実行タスクが使用する SQL ステートメントのパラメーターにマップする場合、各パラメーター バインドのデータ型を、システム変数のデータ型に設定することが重要です。 このように設定しないと、システム変数の値が誤って解釈されることがあります。 たとえば、 **ExecutionInstanceGUID** システム変数は文字列データ型で、実行中のパッケージのインスタンスの GUID の文字列表現を保持しますが、パラメーター バインドに GUID データ型を使用すると、パッケージのインスタンスの GUID は誤って解釈されます。  
  
 この規則は、ユーザー定義変数にも当てはまります。 ただし、システム変数のデータ型は変更できないため、システム変数を使用する場合はそのデータ型に合わせた調整が必要ですが、ユーザー定義変数にはそれに比べると高い柔軟性があります。 パラメーター バインドで使用するユーザー定義変数は、通常、マップ先パラメーターのデータ型と互換性のあるデータ型で定義します。  
  
## <a name="related-tasks"></a>Related Tasks  
 [クエリ パラメーターを SQL 実行タスクの変数にマップする方法](https://msdn.microsoft.com/library/6a164349-dfcf-4995-80bc-d4e7aee52a83)  
  
  
