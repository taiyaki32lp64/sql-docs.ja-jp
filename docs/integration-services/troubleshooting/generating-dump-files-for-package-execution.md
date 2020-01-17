---
title: パッケージ実行用のダンプ ファイルを生成する | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 89e0fd965cdd2faeb522d35e892ec8f0fe79bb9e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295112"
---
# <a name="generating-dump-files-for-package-execution"></a>パッケージ実行用のダンプ ファイルを生成する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、パッケージの実行に関する情報を提供するデバッグ ダンプ ファイルを作成できます。 このファイル内の情報は、パッケージの実行に関する問題のトラブルシューティングに役立ちます。  
  
> **注:** デバッグ ダンプ ファイルには機密情報が含まれている場合があります。 機密情報を保護するには、アクセス制御リスト (ACL) を使用してこのファイルへのアクセスを制限するか、アクセスが制限されたフォルダーにファイルをコピーすることができます。 たとえば、デバッグ ファイルを [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート サービスに送信する前には、機密性の高い情報をすべて削除することをお勧めします。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーにプロジェクトを配置すると、そのプロジェクトに含まれているパッケージの実行に関する情報を提供するダンプ ファイルを作成できます。 ISServerExec.exe プロセスが終了すると、ダンプ ファイルが作成されます。 **[パッケージの実行]** ダイアログ ボックスの **[エラー時にダンプする]** オプションを選択することにより、パッケージの実行中にエラーが発生したらダンプ ファイルが作成されるように指定できます。 また、次のストアド プロシージャを使用することもできます。  
  
-   [catalog.set_execution_parameter_value (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
     パッケージの実行中にエラーまたはイベントが発生したとき、および特定のイベントが発生したときにダンプ ファイルが作成されるように構成する場合に、このストアド プロシージャを呼び出します。  
  
-   [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
  
     実行中のパッケージを一時停止してダンプ ファイルを作成する場合に、このストアド プロシージャを呼び出します。  
  
 パッケージ配置モデルを使用する場合は、 **dtexec** ユーティリティまたは **dtutil** ユーティリティを使用して、コマンド ラインでデバッグ ダンプ オプションを指定することによって、デバッグ ダンプ ファイルを作成します。 詳細については、「[dtexec ユーティリティ](../../integration-services/packages/dtexec-utility.md)」と「[dtutil ユーティリティ](../../integration-services/dtutil-utility.md)」を参照してください。 パッケージ配置モデルの詳細については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](https://msdn.microsoft.com/library/hh213290.aspx)」と「[レガシー パッケージの配置 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)」を参照してください。   
  
## <a name="debug-dump-file-format"></a>デバッグ ダンプ ファイルの形式  
 デバッグ ダンプ オプションを指定した場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって作成されるデバッグ ダンプ ファイルを次に示します。  
  
-   .mdmp デバッグ ダンプ ファイル。 これはバイナリ ファイルです。  
  
-   .tmp デバッグ ダンプ ファイル。 これはテキスト形式のファイルです。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の既定では、これらのファイルは *\<ドライブ>:* \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps フォルダーに格納されます。  
  
 次の表では、.tmp ファイル内の特定のセクションのみについて説明します。 .tmp ファイルには、次の表に記載されていないデータが他にも含まれています。  
  
|情報の種類|[説明]|例|  
|-------------------------|-----------------|-------------|  
|環境|オペレーティング システムのバージョン、メモリの使用量のデータ、プロセス ID、およびプロセス イメージ名。 環境情報は .tmp ファイルの先頭にあります。|# SSIS Textual Dump taken at 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Image Name [C:\Program Files\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Running on 2 amd64 processors under WOW64<br /><br /> # Memory:58% in use. Physical:845M/2044M  Paging:2404M/4095M (avail/total)|  
|ダイナミック リンク ライブラリ (DLL) のパスとバージョン|パッケージの処理中にシステムによって読み込まれる各 DLL のパスとバージョン番号。|# Loaded Module: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Loaded Module:C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Loaded Module:C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|最新のメッセージ|システムで発行された最新のメッセージ。 各メッセージの時刻、種類、説明、およびスレッド ID が含まれます。|[M:1]   Ring buffer entry:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( \@ 0282F1A8 )<br /><br /> [E:3]         Time Stamp:2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         Thread ID:2368           (ThreadID)<br /><br /> [E:3]         Event Name:OnError                        (EventName)<br /><br /> [E:3]         Source Name:              (SourceName)<br /><br /> [E:3]         Source ID:                      (SourceID)<br /><br /> [E:3]         Execution ID:               (ExecutionGUID)<br /><br /> [E:3]         Data Code: -1073446879              (DataCode)<br /><br /> [E:3]         Description:コンポーネントが見つからないか、登録されていないか、アップグレードできないか、コンポーネントに必要なインターフェイスが見つかりません。 このコンポーネントの連絡先情報は "" です。|  
  
## <a name="related-information"></a>関連情報  
 [[パッケージの実行] ダイアログ ボックス](../../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
  
