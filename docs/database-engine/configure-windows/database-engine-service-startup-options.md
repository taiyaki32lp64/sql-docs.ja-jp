---
title: データベース エンジン サービスのスタートアップ オプション | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], startup option
- overriding default startup options
- minimal configuration mode [SQL Server], startup option
- default startup options
- temporarily override default startup options [SQL Server]
- startup options [SQL Server]
- starting SQL Server, options
- single-user mode [SQL Server], startup parameter
- overriding default startup parameters
- minimal configuration mode [SQL Server], startup parameter
- default startup parameters
- temporarily override default startup parameters [SQL Server]
- startup parameters [SQL Server]
- starting SQL Server, parameters
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4518428d6dd583e5d9fe2a4da06f052b8b75da70
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252868"
---
# <a name="database-engine-service-startup-options"></a>データベース エンジン サービスのスタートアップ オプション

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

スタートアップ オプションは、起動時に必要な特定のファイルの場所およびサーバー全体の状態を指定します。 通常は、スタートアップ オプションを指定する必要はありません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のトラブルシューティングを行う場合や、特殊な問題が発生し、スタートアップ オプションの使用を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カスタマー サポートから指示された場合のみ指定します。  
  
> [!WARNING]  
>  スタートアップ オプションを不適切に使用すると、サーバー パフォーマンスの低下を招くことや、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が起動しなくなることがあります。  
>
>  スタートアップに関する将来の問題を防ぐため、Linux 上の SQL Server は "mssql" ユーザーで起動してください。 例: `sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]` 
  
## <a name="about-startup-options"></a>スタートアップ オプションについて  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールすると、セットアップが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のレジストリに既定のスタートアップ オプションを書き込みます。 これらのスタートアップ オプションを使用して、代替の master データベース ファイル、master データベース ログ ファイル、またはエラー ログ ファイルを指定することができます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が必要なファイルを見つけることができない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は起動しません。  
  
 スタートアップ オプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して設定できます。 詳しくは、「[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)」を参照してください。  
  
## <a name="list-of-startup-options"></a>スタートアップ オプションの一覧  
### <a name="default-startup-options"></a>既定のスタートアップ オプション  

|オプション|[説明]|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|master データベース ファイルの完全修飾パス (通常は、C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\master.mdf)。 このオプションを省略すると、レジストリ内にあるパラメーターが使用されます。|  
|**-e**  *error_log_path*|エラー ログ ファイルの完全修飾パス (通常は、C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG) です。 このオプションを省略すると、レジストリ内にあるパラメーターが使用されます。|  
|**-l**  *master_log_path*|master データベース ログ ファイルの完全修飾パス (通常は、C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf)。 このオプションを指定しない場合は、レジストリ内にあるパラメーターが使用されます。|  
  
### <a name="other-startup-options"></a>他のスタートアップ オプション   

|オプション |[説明]|   
|---------------------------|-----------------|  
|**-c**|コマンド プロンプトから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動する場合に、起動時間を短縮します。 通常、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、サービス コントロール マネージャーを呼び出すことにより、サービスとして起動します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、コマンド プロンプトから起動した場合はサービスとして起動しないため、 **-c** を使用してこの手順を省略します。|  
|**-f**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを最小構成で起動します。 設定値によりサーバーが起動できないとき (たとえば使用できるメモリが不足している場合) などに便利です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を最小構成モードで起動すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシングル ユーザー モードになります。 詳細については、後の **-m** の説明を参照してください。|  
|**-kDecimalNumber**| このスタートアップ パラメーターでは、1 秒あたりのチェックポイント I/O の数を制限します。ここで、**DecimalNumber** は MB/秒で表したチェックポイント速度です。  この値を変更すると、バックアップの実行速度に影響したり、回復プロセスをすべて行うことになったりするため、注意して進めてください。 このスタートアップ パラメーターの詳細については、[-k パラメーター](https://support.microsoft.com/help/929240/fix-i-o-requests-that-are-generated-by-the-checkpoint-process-may-caus)を導入した場合のホット フィックスを参照してください。| 
|**-m**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをシングル ユーザー モードで起動します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをシングル ユーザー モードで起動する場合、接続できるユーザーは 1 ユーザーのみで、CHECKPOINT プロセスは起動されません。 CHECKPOINT は、完了したトランザクションがディスク キャッシュからデータベース デバイスに定期的に書き込まれることを保証する機能です。 一般的に、システム データベースを修復する必要がある問題が発生したときに、このオプションを使用します。sp_configure allow updates オプションが有効になります。 既定では、allow updates は無効になっています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動すると、コンピューターのローカル Administrators グループのメンバーはすべて、固定サーバー ロール sysadmin のメンバーとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続できるようになります。 詳細については、「 [システム管理者がロックアウトされた場合の SQL Server への接続](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)」を参照してください。シングル ユーザー モードの詳細については、「 [シングル ユーザー モードでの SQL Server の起動](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)」を参照してください。|  
|**-mClient アプリケーション名**|接続を特定のクライアント アプリケーションに限定します。 たとえば、 `-mSQLCMD`  を使用すると、接続が、SQLCMD クライアント プログラムとして識別される必要がある単一の接続に限定されます。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動するときに、その唯一の接続を不明なクライアント アプリケーションによって使用されていた場合に使用します。 `"Microsoft SQL Server Management Studio - Query"` を使用し、SSMS クエリ エディターと接続します。 SSMS クエリ エディター オプションは、 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 構成マネージャーで構成できません。ツールで拒否されるダッシュ文字が含まれているためです。<br /><br /> クライアント アプリケーション名では大文字と小文字が区別されます。 アプリケーション名にスペースや特殊文字が含まれる場合、二重引用符が必要です。<br /><br />**コマンドラインから起動した場合の例:**<br /><br />`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\sqlservr -s MSSQLSERVER -m"Microsoft SQL Server Management Studio - Query"` <br /><br />`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\sqlservr -s MSSQLSERVER -mSQLCMD` <br /><br /> **セキュリティに関する注意:** このオプションをセキュリティ機能として使用しないでください。 クライアント アプリケーションの名前はクライアント アプリケーションによって接続文字列の一部として指定されるため、本当の名前が指定されるとは限りません。|  
|**-n**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントを記録する際に、Windows アプリケーション ログを使用しません。 **-n** を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動する場合は、 **-e** スタートアップ オプションも使用することをお勧めします。 このオプションを指定しないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベントはログに記録されません。|  
|**-s**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の名前付きインスタンスの起動を可能にします。 **-s** パラメーターが設定されていない場合は、既定のインスタンスが起動されます。 **sqlservr.exe**を開始する前に、コマンド プロンプトで、インスタンスの適切な BINN ディレクトリに移動する必要があります。 たとえば、Instance1 がバイナリ用に `\mssql$Instance1` を使用する場合、ユーザーは `\mssql$Instance1\binn` ディレクトリで **sqlservr.exe -s instance1** を起動する必要があります。|  
|**-T** *trace#*|指定された、有効なトレース フラグ (*trace#* ) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動します。 トレース フラグを使用してサーバーが起動すると、標準的な動作とは異なります。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。<br /><br /> **重要:** **-T** オプションを指定してトレース フラグを指定するときは、大文字の "T" を使用してトレース フラグ番号を渡してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は小文字の "t" を受け付けますが、これは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサポート エンジニアのみが必要とする他の内部トレース フラグを設定するためのものです。 コントロール パネルの起動ウィンドウで指定されているパラメーターは使用されません。|  
|**-x**|次の監視機能を無効にします。<br /> - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パフォーマンス モニター カウンター<br /> - CPU 時間とキャッシュ ヒット率統計の管理<br /> - DBCC SQLPERF コマンドに関する情報の収集<br /> - 一部の動的管理ビューに関する情報の収集<br /> - 拡張イベントの多数のイベント ポイント<br /><br /> **警告:** **-x** スタートアップ オプションを使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関するパフォーマンスや機能の問題を診断するために使用できる情報が大幅に減少されます。|  
|**-E**|ファイル グループ内の各ファイルに割り当てられるエクステントの数を増やします。 このオプションは、インデックス スキャンまたはデータ スキャンを実行するユーザーの数が限られているデータ ウェアハウス アプリケーションで役立つ場合があります。 パフォーマンスに悪影響を及ぼす可能性があるため、他のアプリケーションでは使用しないでください。 このオプションは、32 ビット リリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ではサポートされていません。|  
  
## <a name="using-startup-options-for-troubleshooting"></a>トラブルシューティングでのスタートアップ オプションの使用  
 シングル ユーザー モードや最小構成モードなど、一部のスタートアップ オプションは、主にトラブルシューティングの際に使用されます。 トラブルシューティングのために **-m** オプションや **-f** オプションを使用してサーバーを起動する場合は、sqlservr.exe を手動で起動するときに、コマンド ラインから起動すると最も容易に起動できます。  
  
> [!NOTE]  
>  **net start** を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動する場合、スタートアップ オプションではハイフン (-) の代わりにスラッシュ (/) を使用します。  
  
## <a name="using-startup-options-during-normal-operations"></a>通常の操作でのスタートアップ オプションの使用  
 スタートアップ オプションの一部は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を起動するたびに使用することが考えられます。 このようなオプション (トレース フラグを使用した起動など) は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、起動時のパラメーターを構成すると最も容易に設定できます。 これらのツールは、スタートアップ オプションをレジストリ キーとして保存するため、常にこれらのスタートアップ オプションを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動できます。  
  
## <a name="compatibility-support"></a>互換性サポート  

以前のリリースから削除されたオプションについては、[sqlservr アプリケーション](../../tools/sqlservr-application.md#compatibility-support)のページを参照してください。

## <a name="related-tasks"></a>Related Tasks  
[scan for startup procs サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)  
[データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)
[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)
  
## <a name="see-also"></a>参照  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sqlservr アプリケーション](../../tools/sqlservr-application.md)  
  
  
