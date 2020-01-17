---
title: データベース エンジン サービスのスタートアップ オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 29984a52d711ef02c3c3b640ef8d59323806c2bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812284"
---
# <a name="database-engine-service-startup-options"></a>データベース エンジン サービスのスタートアップ オプション
  スタートアップ オプションは、起動時に必要な特定のファイルの場所およびサーバー全体の状態を指定します。 通常は、スタートアップ オプションを指定する必要はありません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のトラブルシューティングを行う場合や、特殊な問題が発生し、スタートアップ オプションの使用を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カスタマー サポートから指示された場合のみ指定します。  
  
> [!WARNING]  
>  スタートアップ オプションを不適切に使用すると、サーバー パフォーマンスの低下を招くことや、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が起動しなくなることがあります。  
  
## <a name="about-startup-options"></a>スタートアップ オプションについて  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールすると、セットアップが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のレジストリに既定のスタートアップ オプションを書き込みます。 これらのスタートアップ オプションを使用して、代替の master データベース ファイル、master データベース ログ ファイル、またはエラー ログ ファイルを指定することができます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が必要なファイルを見つけることができない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は起動しません。  
  
 スタートアップ オプションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して設定できます。 詳しくは、「[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](scm-services-configure-server-startup-options.md)」を参照してください。  
  
## <a name="list-of-startup-options"></a>スタートアップ オプションの一覧  
  
|既定のスタートアップ オプション|説明|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|master データベース ファイルの完全修飾パス (通常は、C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\master.mdf)。 このオプションを省略すると、レジストリ内にあるパラメーターが使用されます。|  
|**-e**  *error_log_path*|エラー ログ ファイルの完全修飾パス (通常は、C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG) です。 このオプションを省略すると、レジストリ内にあるパラメーターが使用されます。|  
|**-l**  *master_log_path*|master データベース ログ ファイルの完全修飾パス (通常は、C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf)。 このオプションを指定しない場合は、レジストリ内にあるパラメーターが使用されます。|  
  
|他のスタートアップ オプション|説明|  
|---------------------------|-----------------|  
|**-c**|コマンド プロンプトから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動する場合に、起動時間を短縮します。 通常、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、サービス コントロール マネージャーを呼び出すことにより、サービスとして起動します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、コマンド プロンプトから起動した場合はサービスとして起動しないため、 **-c** を使用してこの手順を省略します。|  
|**-f**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを最小構成で起動します。 設定値によりサーバーが起動できないとき (たとえば使用できるメモリが不足している場合) などに便利です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を最小構成モードで起動すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がシングル ユーザー モードになります。 詳細については、後の **-m** の説明を参照してください。|  
|**-g**  *memory_to_reserve*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ プール外の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス内にメモリ割り当てに使用できる領域として残すメモリ容量を整数 (MB 単位) で指定します。 メモリ プール外のメモリは、拡張プロシージャ .dll ファイル、分散クエリによって参照される OLE DB プロバイダー、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントで参照されるオートメーション オブジェクトなどのアイテムを読み込むために、 [!INCLUDE[tsql](../../includes/tsql-md.md)] によって使用される領域です。 既定値は 256 MB です。<br /><br /> このオプションを使用すると、メモリ割り当てを調整するうえで役に立つ場合がありますが、これは、アプリケーションが使用できる仮想メモリに対してオペレーティング システムが設定する制限値よりも物理メモリが多い場合だけです。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に必要なメモリ容量が通常より多い大容量メモリ構成で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスの仮想アドレス空間全体が使用される場合に効果があります。 このオプションを誤って使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が起動しないことや、実行時エラーが発生することがあります。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに次の警告が記録されない限り、 **-g** パラメーターの既定値を使用してください。<br /><br /> -"仮想失敗バイトを割り当てます。FAIL_VIRTUAL_RESERVE \<size>"<br /><br /> -"仮想失敗バイトを割り当てます。FAIL_VIRTUAL_COMMIT \<size>"<br /><br /> これらのメッセージは、拡張ストアド プロシージャ .dll ファイルやオートメション オブジェクトなどのアイテムの格納領域を確保するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ プールの一部を解放しようとしていることを示している場合があります。 その場合は、 **-g** スイッチによって確保するメモリ量を増やすことを検討してください。<br /><br /> 既定値より小さい値を使用すると、SQL Server Memory Manager によって管理されるメモリ プールおよびスレッド スタックが利用できる容量が増えます。その結果、拡張ストアド プロシージャ、分散クエリ、またはオートメーション オブジェクトを多用しないシステムの、メモリ負荷の高い作業のパフォーマンスが向上することがあります。|  
|**-m**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをシングル ユーザー モードで起動します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをシングル ユーザー モードで起動する場合、接続できるユーザーは 1 ユーザーのみで、CHECKPOINT プロセスは起動されません。 CHECKPOINT は、完了したトランザクションがディスク キャッシュからデータベース デバイスに定期的に書き込まれることを保証する機能です。 一般的に、システム データベースを修復する必要がある問題が発生したときに、このオプションを使用します。sp_configure allow updates オプションが有効になります。 既定では、allow updates は無効になっています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動すると、コンピューターのローカル Administrators グループのメンバーはすべて、固定サーバー ロール sysadmin のメンバーとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続できるようになります。 詳細については、「 [システム管理者がロックアウトされた場合の SQL Server への接続](connect-to-sql-server-when-system-administrators-are-locked-out.md)」を参照してください。シングル ユーザー モードの詳細については、「 [シングル ユーザー モードでの SQL Server の起動](start-sql-server-in-single-user-mode.md)」を参照してください。|  
|**-m「クライアント アプリケーション名」**|**SQLCMD** または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で **-m** オプションを使用すると、接続を特定のクライアント アプリケーションに限定できます。 たとえば、**-m"SQLCMD"** を使用すると、接続が、**SQLCMD** クライアント プログラムとして識別される必要がある単一の接続に限定されます。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動するときに、その唯一の接続を不明なクライアント アプリケーションによって使用されていた場合に使用します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のクエリ エディターを使用して接続するには、 **-m"Microsoft SQL Server Management Studio - Query"** を使用します。<br /><br /> クライアント アプリケーション名では大文字と小文字が区別されます。<br /><br /> **\*\* セキュリティに関する注意 \*\*** このオプションをセキュリティ機能として使用しないでください。 クライアント アプリケーションの名前はクライアント アプリケーションによって接続文字列の一部として指定されるため、本当の名前が指定されるとは限りません。|  
|**-n**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントを記録する際に、Windows アプリケーション ログを使用しません。 **-n** を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動する場合は、 **-e** スタートアップ オプションも使用することをお勧めします。 このオプションを指定しないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のイベントはログに記録されません。|  
|**-s**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の名前付きインスタンスの起動を可能にします。 **-s** パラメーターが設定されていない場合は、既定のインスタンスが起動されます。 **sqlservr.exe**を開始する前に、コマンド プロンプトで、インスタンスの適切な BINN ディレクトリに移動する必要があります。 たとえば、Instance1 がバイナリ用に \mssql$Instance1 を使用する場合、ユーザーは \mssql$Instance1\binn ディレクトリで **sqlservr.exe -s instance1**を起動する必要があります。|  
|**-T**  *trace#*|指定された、有効なトレース フラグ (*trace#*) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動します。 トレース フラグを使用してサーバーが起動すると、標準的な動作とは異なります。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)」を参照してください。<br /><br /> **\*\* 重要 \*\*** **-T** オプションを指定してトレース フラグを指定するときは、大文字の "T" を使用してトレース フラグ番号を渡してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は小文字の "t" を受け付けますが、これは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のサポート エンジニアのみが必要とする他の内部トレース フラグを設定するためのものです。 コントロール パネルの起動ウィンドウで指定されているパラメーターは使用されません。|  
|**-x**|次の監視機能を無効にします。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パフォーマンス モニター カウンター<br /><br /> CPU 時間とキャッシュ ヒット率統計の管理<br /><br /> DBCC SQLPERF コマンドに関する情報の収集<br /><br /> 一部の動的管理ビューに関する情報の収集<br /><br /> 拡張イベントの多数のイベント ポイント<br /><br /> <br /><br /> **\*\* 警告 \*\*** **-x**スタートアップ オプションを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関するパフォーマンスと機能の問題を診断するために使用できる情報が大幅に減少します。|  
|**-E**|ファイル グループ内の各ファイルに割り当てられるエクステントの数を増やします。 このオプションは、インデックス スキャンまたはデータ スキャンを実行するユーザーの数が限られているデータ ウェアハウス アプリケーションで役立つ場合があります。 パフォーマンスに悪影響を及ぼす可能性があるため、他のアプリケーションでは使用しないでください。 このオプションは、32 ビット リリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ではサポートされていません。|  
  
## <a name="using-startup-options-for-troubleshooting"></a>トラブルシューティングでのスタートアップ オプションの使用  
 シングル ユーザー モードや最小構成モードなど、一部のスタートアップ オプションは、主にトラブルシューティングの際に使用されます。 トラブルシューティングのために **-m** オプションや **-f** オプションを使用してサーバーを起動する場合は、sqlservr.exe を手動で起動するときに、コマンド ラインから起動すると最も容易に起動できます。  
  
> [!NOTE]  
>  **net start** を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動する場合、スタートアップ オプションではハイフン (-) の代わりにスラッシュ (/) を使用します。  
  
## <a name="using-startup-options-during-normal-operations"></a>通常の操作でのスタートアップ オプションの使用  
 スタートアップ オプションの一部は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を起動するたびに使用することが考えられます。 このようなオプション (**-g** やトレース フラグを使用した起動など) は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、起動時のパラメーターを構成すると最も容易に設定できます。 これらのツールは、スタートアップ オプションをレジストリ キーとして保存するため、常にこれらのスタートアップ オプションを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動できます。  
  
## <a name="compatibility-support"></a>互換性サポート  
 **-h**  パラメーターは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ではサポートされていません。 このパラメーターは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビットのインスタンスで AWE が有効になっている場合に、ホット アド メモリ メタデータ用の仮想メモリ アドレス空間を確保するために使用されていました。 詳細については、「[SQL Server 2014 で提供が中止された機能](../../getting-started/discontinued-sql-server-features-in-sql-server-2014.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [scan for startup procs サーバー構成オプションの構成](configure-the-scan-for-startup-procs-server-configuration-option.md)  
  
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](start-stop-pause-resume-restart-sql-server-services.md)  
  
## <a name="see-also"></a>参照  
 [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql)   
 [sqlservr アプリケーション](../../tools/sqlservr-application.md)  
  
  
