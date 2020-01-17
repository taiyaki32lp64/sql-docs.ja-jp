---
title: dtutil ユーティリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- verifying packages
- checking packages
- moving packages
- packages [Integration Services], command line options
- command prompt [Integration Services]
- SQL Server Integration Services packages, command line options
- copying packages
- existence testing [Integration Services]
- Integration Services packages, command line options
- SSIS packages, command line options
- deleting packages
- dtutil utility
- removing packages
- relocating packages
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19f179ae869a175ea6238ba4ade9e5f87d663e08
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297797"
---
# <a name="dtutil-utility"></a>Encrypt

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **dtutil** コマンド プロンプト ユーティリティは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージの管理に使用します。 このユーティリティを使用して、パッケージのコピー、移動、削除を行ったり、パッケージの存在を確認することができます。 これらの操作は [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ上で実行できます。このパッケージは、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベース、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストア、およびファイル システムの 3 つの場所のいずれかに格納されます。 このユーティリティが **msdb**に格納されているパッケージにアクセスする場合、コマンド プロンプトでユーザー名とパスワードが必要となる場合があります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用する場合、コマンド プロンプトではユーザー名とパスワードの両方が必要です。 ユーザー名を入力しない場合、 **dtutil** は Windows 認証を使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にログオンしようとします。 パッケージのストレージ型は **SQL**、 **FILE**、および **DTS** オプションで指定します。  
  
 **dtutil** コマンド プロンプト ユーティリティでは、コマンド ファイルの使用およびリダイレクションはサポートされていません。  
  
 **dtutil** コマンド プロンプト ユーティリティには、次の機能が含まれます。  
  
-   コマンド プロンプトの解説。これによってコマンド プロンプトのアクションを自己文書化し、理解しやすくします。  
  
-   上書きの保護。パッケージをコピーまたは移動する場合、既存のパッケージを上書きする前に確認メッセージが表示されます。  
  
-   コンソール ヘルプ。 **dtutil**のコマンド オプションに関する情報が提供されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のインスタンスに接続している場合、dtutil によって実行される操作の多くは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]で確認しながら実行することもできます。 詳細については、「[パッケージの管理 &#40;SSIS サービス&#41;](../integration-services/service/package-management-ssis-service.md)」を参照してください。  
  
 オプションを入力する順序は任意です。 パイプ (|) 文字は **OR** 演算子を表し、利用可能な値を示すために使用されます。 **OR** パイプで区切られたオプションのうちの 1 つを使用する必要があります。  
  
 すべてのオプションは、スラッシュ (/) またはマイナス記号 (-) で始まる必要があります。 ただし、オプションのテキストとスラッシュ (/) またはマイナス記号 (-) の間に空白を入れないでください。空白を入れると、コマンドの実行が失敗します。  
  
 引数は、引用符で囲むか、空白を含まない文字列を指定する必要があります。  
  
 引用符で囲まれた文字列内に二重引用符がある場合は、単一引用符がエスケープされていることを表します。  
  
 パスワードを除いて、オプションおよび引数では大文字と小文字が区別されません。  
  
 **64 ビット コンピューターでのインストールに関する注意点**  
  
 64 ビット コンピューターには、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によって 64 ビット版の **dtexec** ユーティリティ (dtexec.exe) および **dtutil** ユーティリティ (dtutil.exe) がインストールされます。 32 ビット版のこれらの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ツールをインストールするには、セットアップ中に [クライアント ツール] または [ [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ] を選択する必要があります。  
  
 既定では、64 ビットと 32 ビットの両方のバージョンの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コマンド プロンプト ユーティリティがインストールされている 64 ビット コンピューターでは、コマンド プロンプトで 32 ビット バージョンが実行されます。 これは、PATH 環境変数で、32 ビット バージョンのディレクトリ パスが 64 ビット バージョンのディレクトリ パスより前に配置されているためです (通常、32 ビットのディレクトリ パスは *\<ドライブ>* :\Program Files(x86)\Microsoft SQL Server\130\DTS\Binn で、64 ビットのディレクトリ パスは *\<ドライブ>* :\Program Files\Microsoft SQL Server\130\DTS\Binn です。)  
  
> [!NOTE]  
>  SQL Server エージェントを使用してユーティリティを実行する場合は、SQL Server エージェントによって 64 ビット バージョンのユーティリティが自動的に使用されます。 SQL Server エージェントでは、PATH 環境変数ではなくレジストリを使用してユーティリティの適切な実行可能ファイルが特定されます。  
  
 コマンド プロンプトで 64 ビット バージョンのユーティリティが実行されるようにするには、次のいずれかの操作を実行します。  
  
-   コマンド プロンプト ウィンドウを開いて、64 ビット バージョンのユーティリティが格納されたディレクトリ *(\<ドライブ>* :\Program Files\Microsoft SQL Server\130\DTS\Binn) に移動し、その場所からユーティリティを実行します。  
  
-   コマンド プロンプトで、64 ビット バージョンのユーティリティの完全なパス ( *\<ドライブ>* :\Program Files\Microsoft SQL Server\130\DTS\Binn) を入力してユーティリティを実行します。  
  
-   PATH 環境変数で、64 ビットのパス ( *\<ドライブ>* :\Program Files\Microsoft SQL Server\130\DTS\Binn) を 32 ビットのパス ( *\<ドライブ>* :\ Program Files(x86)\Microsoft SQL Server\130\DTS\Binn) より前に配置してパスの順序を永続的に変更します。  
  
## <a name="syntax"></a>構文  
  
```dos
dtutil /option [value] [/option [value]]...  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|オプション|[説明]|  
|------------|-----------------|  
|/?|コマンド プロンプト オプションを表示します。|  
|/C[opy] *location;destinationPathandPackageName*|[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージに対するコピー操作を指定します。 このパラメーターを使用するには、先に **/FI**、 **SQ**、または **/DT** オプションを使用してパッケージの場所を指定する必要があります。 次に、コピー先の場所とコピー先のパッケージ名を指定します。 *destinationPathandPackageName* 引数には、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージのコピー先を指定します。 コピー先の *location* が **SQL**の場合は、 *DestUser*、 *DestPassword* 、および *DestServer* 引数もコマンドで指定する必要があります。<br /><br /> **Copy** 操作でコピー先に既存のパッケージが見つかった場合、 **dtutil** によって、パッケージの上書きを確認するプロンプトが表示されます。 パッケージを上書きする場合は **Y** 、プログラムを終了する場合は **N** と応答します。 コマンドに *Quiet* 引数が含まれている場合は、プロンプトは表示されず、既存のパッケージはすべて上書きされます。|  
|/Dec[rypt] *password*|(省略可)。 パスワードが暗号化されているパッケージを読み込むときに使用する暗号化解除用パスワードを設定します。|  
|/Del[ete]|*SQL*、 *DTS* 、または *FILE* オプションによって指定されたパッケージを削除します。 **dtutil** がパッケージを削除できない場合、プログラムは終了します。|  
|/DestP[assword] *password*|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用している [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに接続するために SQL オプションで使用されるパスワードを指定します。 コマンド ラインで *DESTPASSWORD* オプションを指定せずに *DTSUSER* を指定すると、エラーが生成されます。<br /><br /> 注: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]。|  
|/DestS[erver] *server_instance*|保存先が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]となる操作で使用されるサーバー名を指定します。 これは、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージの保存時に、ローカル以外のサーバーまたは既定以外のサーバーを識別するために使用されます。 コマンド ラインで *と関連する操作を指定せずに* DESTSERVER [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を指定すると、エラーになります。 このオプションとの組み合わせが適しているのは、 *SIGN SQL*、 *COPY SQL*、または *MOVE SQL* オプションなどの操作を行うコマンドです。<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス名は、円記号とインスタンス名をサーバー名に追加することによって指定します。|  
|/DestU[ser] *username*|*認証を使用する*インスタンスへ接続するために、 *SIGN SQL*オプション、 *COPY SQL* オプション、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] MOVE SQL [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オプションで使用するユーザー名を指定します。 コマンド ラインで *DESTUSER* オプション、 *SIGN SQL*オプション、または *COPY SQL*オプションを指定せずに *MOVE SQL* を指定すると、エラーになります。|  
|/Dump *process ID*|(省略可) 指定したプロセス ( **dtexec** ユーティリティまたは **dtsDebugHost.exe** プロセス) を一時停止し、デバッグ ダンプ ファイル (.mdmp および .tmp) を作成します。<br /><br /> 注: **/Dump** オプションを使用するには、Debug Programs ユーザー権限 (SeDebugPrivilege) が割り当てられている必要があります。<br /><br /> 一時停止するプロセスの *process ID* を見つけるには、Windows タスク マネージャーを使用します。<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の既定では、デバッグ ダンプ ファイルは *\<ドライブ>* :\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps フォルダーに格納されます。<br /><br /> **dtexec** ユーティリティおよび **dtsDebugHost.exe** プロセスの詳細については、「 [dtexec Utility](../integration-services/packages/dtexec-utility.md) 」および「 [Building, Deploying, and Debugging Custom Objects](../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)」を参照してください。<br /><br /> デバッグ ダンプ ファイルの詳細については、「 [Generating Dump Files for Package Execution](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)」を参照してください。<br /><br /> 注:デバッグ ダンプ ファイルには機密情報が含まれている場合があります。 アクセス制御リスト (ACL) を使用してファイルへのアクセスを制限するか、アクセスが制限されたフォルダーにファイルをコピーしてください。|  
|/DT[S] *filespec*|実行される [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージが [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアに存在することを指定します。 *filespec* 引数には、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアのルートから始まるフォルダー パスを指定する必要があります。 既定では、構成ファイル内のルート フォルダーの名前は "MSDB" と "File System" です。 空白を含むパスは、二重引用符で囲む必要があります。<br /><br /> DT[S] オプションが、次のオプションのいずれかと同じコマンド ライン上に指定された場合、DTEXEC_DTEXECERROR が返されます。<br /><br /> **FILE**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/En[crypt] *{SQL &#124; FILE}; Path;ProtectionLevel[;password]*|(省略可)。 読み込まれたパッケージを指定された保護レベルおよびパスワードで暗号化し、それを *Path*で指定された場所に保存します。 パスワードが必要かどうかは、 *ProtectionLevel* で判断されます。<br /><br /> *SQL* - Path には保存先となるパッケージ名を指定します。<br /><br /> *FILE* - Path にはパッケージの完全修飾パスとファイル名を指定します。<br /><br /> *DTS* - このオプションは現在サポートされていません。<br /><br /> *ProtectionLevel* オプション:<br /><br /> Level 0:重要な情報を切り離します。<br /><br /> Level 1: ローカル ユーザーの資格情報を使用して重要な情報を暗号化します。<br /><br /> Level 2: 必要なパスワードを使用して重要な情報を暗号化します。<br /><br /> Level 3: 必要なパスワードを使用してパッケージを暗号化します。<br /><br /> Level 4: ローカル ユーザーの資格情報を使用してパッケージを暗号化します。<br /><br /> Level 5: パッケージは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ストレージの暗号化を使用します。|  
|/Ex[ists]|(省略可)。 パッケージが存在するかどうかを判断するために使用されます。 **dtutil** は、 *SQL*オプション、 *DTS* オプション、または *FILE* オプションのいずれかによって指定されたパッケージを検索します。 **dtutil** が指定されたパッケージを見つけることができない場合、DTEXEC_DTEXECERROR が返されます。|  
|/FC[reate] {*SQL* &#124; *DTS*};*ParentFolderPath;NewFolderName*|(省略可)。 *NewFolderName*で指定された名前で新しいフォルダーを作成します。 新しいフォルダーの場所は、 *ParentFolderPath*によって指定されます。|  
|/FDe[lete] {*SQL* &#124; *DTS*}[;*ParentFolderPath;FolderName]*|(省略可)。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] FolderName [!INCLUDE[ssIS](../includes/ssis-md.md)] で指定された名前のフォルダーを *または*から削除します。 削除するフォルダーの場所は、 *ParentFolderPath*で指定されます。|  
|/FDi[rectory] {*SQL* &#124; *DTS*};*FolderPath[;S]*|(省略可)。 [!INCLUDE[ssIS](../includes/ssis-md.md)] または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上にあるフォルダーの内容 (フォルダーとパッケージの両方) を一覧表示します。 省略可能な *FolderPath* パラメーターには、内容を表示するフォルダーを指定します。 *S* パラメーターは、 *FolderPath*で指定されたフォルダーのサブフォルダーの内容を表示する場合に指定します。|  
|/FE[xists ] {*SQL* &#124; *DTS*};*FolderPath*|(省略可)。 指定されたフォルダーが [!INCLUDE[ssIS](../includes/ssis-md.md)] 上または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上にあるかどうかを確認します。 *FolderPath* パラメーターは、確認するフォルダーのパスおよび名前です。|  
|/Fi[le] *filespec*|このオプションは、実行される [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージがファイル システムに存在することを指定します。 *filespec* の値は、汎用名前付け規則 (UNC) パスまたはローカル パスのどちらかで指定できます。<br /><br /> *File* オプションが、次のオプションのいずれかと同じコマンド ライン上に指定された場合、DTEXEC_DTEXECERROR が返されます。<br /><br /> **DTS**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/FR[ename] {*SQL* &#124; *DTS*} [;*ParentFolderPath; OldFolderName;NewFolderName]*|(省略可)。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 上または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上にあるフォルダーの名前を変更します。 *ParentFolderPath* は、名前を変更するフォルダーの場所です。 *OldFolderName* はフォルダーの現在の名前で、 *NewFolderName* はそのフォルダーに付ける新しい名前です。|  
|/H[elp] *option*|**dtutil** の各オプションとその使用方法を詳細に説明するヘルプ テキストを表示します。 このオプションの引数は省略可能です。 引数が含まれている場合、ヘルプ テキストには、指定されたオプションに関する詳細情報が表示されます。 次の例では、すべてのオプションに関するヘルプが表示されます。<br /><br /> `dtutil /H`<br /><br /> 次の 2 つの例では、 */H* オプションを使用して、特定のオプション (この例では */Q [uiet]* オプション) に関する詳細なヘルプが表示されます。<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|パッケージの新しい GUID を作成し、パッケージの ID プロパティを更新します。 パッケージをコピーするときに、パッケージ ID が同じままだと、両方のパッケージが同じ GUID でログ ファイルに表示されることになります。 この操作では、新しくコピーされたパッケージ用に新しい GUID が作成され、元のパッケージと区別されます。|  
|/M[ove] {*SQL* &#124; *File* &#124; *DTS*}; *pathandname*|[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージに対する移動操作を指定します。 このパラメーターを使用するには、先に **/FI**、 **/SQ**、または **/DT** オプションを使用してパッケージの場所を指定し、 次に **Move** 操作を指定します。 この操作には、2 つの引数をセミコロンで区切って指定する必要があります。<br /><br /> 移動先の引数には、 *SQL*、 *FILE*、または *DTS*を指定できます。 *SQL* の移動先には、 *DESTUSER*オプション、 *DESTPASSWORD*オプション、および *DESTSERVER* オプションを含めることができます。<br /><br /> *pathandname* 引数には、パッケージの場所を指定します。*SQL* ではパッケージのパスおよびパッケージ名、*FILE* では UNC またはローカル パス、*DTS* では [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ ストアのルートを基準とした相対的な場所をそれぞれ使用します。 移動先が *FILE* または *DTS*の場合、パスの引数にはファイル名を含めません。 代わりに、指定された場所にあるパッケージ名をファイル名として使用します。<br /><br /> <br /><br /> **MOVE** 操作で移動先に既存のパッケージが見つかった場合、 **dtutil** によって、パッケージの上書きを確認するプロンプトが表示されます。 パッケージを上書きする場合は **Y** 、プログラムを終了する場合は **N** と応答します。 コマンドに *QUIET* オプションが含まれている場合は、プロンプトは表示されず、既存のパッケージはすべて上書きされます。|  
|/Q[uiet]|**COPY**オプション、 **MOVE**オプション、または **SIGN** オプションを含むコマンドの実行時に示される確認プロンプトが表示されないようにします。 この確認プロンプトは、指定されたパッケージと同じ名前のパッケージが対象となるコンピューターに既に存在する場合や、指定されたパッケージが既に署名されている場合に表示されます。|  
|/R[emark] *text*|コメントをコマンド ラインに追加します。 コメントの引数は省略可能です。 コメント テキストが空白を含む場合、テキストを引用符で囲む必要があります。 1 行のコマンド ラインに複数の REM オプションを含めることができます。|  
|/Si[gn] {*SQL* &#124; *File* &#124; *DTS*}; *path*; *hash*|[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージに署名します。 この操作には、移動先、パス、およびハッシュの 3 つの引数をセミコロンで区切って指定する必要があります。<br /><br /> 移動先の引数には、 *SQL*、 *FILE*、または *DTS*を指定できます。 SQL の移動先には、 *DESTUSER*オプション、 *DESTPASSWORD* オプション、および *DESTSERVER* オプションを含めることができます。<br /><br /> path 引数には、操作の対象となるパッケージの場所を指定します。<br /><br /> hash 引数には、さまざまな長さの 16 進数文字列で表される認証識別子を指定します。<br /><br /> 詳細については、「 [デジタル署名を使用してパッケージのソースを特定する](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)」を参照してください。<br /><br /> <br /><br /> **\*\* 重要 \*\*** パッケージの署名を確認するように構成した場合、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によって確認されるのは、デジタル署名が存在するかどうか、有効かどうか、および信頼関係のある発行元の署名であるかどうかのみです。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、パッケージが変更されたかどうかは確認 *されません* 。|  
|/SourceP[assword] *password*|*認証を使用する* インスタンスのデータベースに格納されている *パッケージを取得できるように、* SQL [!INCLUDE[ssIS](../includes/ssis-md.md)] オプションおよび [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SOURCEUSER [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オプションで使用されるパスワードを指定します。 コマンド ラインで *SOURCEUSER* オプションを指定せずに **SOURCEPASSWORD** を指定すると、エラーになります。<br /><br /> 注: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] *server_instance*|**に格納されている** パッケージを取得できるように、 [!INCLUDE[ssIS](../includes/ssis-md.md)] SQL [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]オプションで使用されるサーバー名を指定します。 コマンド ラインで *SQL* オプション、 *SQL*, *SQL* *SQL*, or *MOVE* *SQL* option.<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンス名は、円記号とインスタンス名をサーバー名に追加することによって指定します。|  
|/SourceU[ser] *username*|*認証を使用する* に格納されている [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージを取得できるように、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SOURCESERVER [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オプションで使用されるユーザー名を指定します。 コマンド ラインで *SOURCEUSER* オプション、 *SIGN SQL*オプション、または *COPY SQL*オプションを指定せずに *MOVE SQL* を指定すると、エラーになります。<br /><br /> 注: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] *package_path*|[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージの場所を指定します。 このオプションは、パッケージが **msdb** データベースに格納されることを示します。 *package_path* 引数には、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージのパスと名前を指定します。 フォルダー名の最後には円記号を入力します。<br /><br /> *SQL* オプションが、次のオプションのいずれかと同じコマンド ライン上に指定された場合、DTEXEC_DTEXECERROR が返されます。<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> *SQL* オプションは、オプションを使用しないか、次のオプションのいずれか 1 つを使用します。<br /><br /> *SOURCEUSER*<br /><br /> *SOURCEPASSWORD*<br /><br /> *SOURCESERVER*<br /><br /> <br /><br /> *SOURCEUSERNAME* が含まれていない場合、パッケージへのアクセスに Windows 認証が使用されます。 *SOURCEPASSWORD* は *SOURCEUSER* が存在する場合のみ使用できます。 *SOURCEPASSWORD* が含まれていない場合、空白のパスワードが使用されます。<br /><br /> **\*\* 重要 \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## <a name="dtutil-exit-codes"></a>dtutil 終了コード  
 構文エラーの検出、不適切な引数の使用、オプションの無効な組み合わせの指定などがあった場合、**dtutil** は警告を表示して終了コードを設定します。 それ以外の場合は、"操作は正常に完了しました" というメッセージが表示されます。次の表は、終了時に **dtutil** ユーティリティが設定できる値を示しています。  
  
|[値]|Description|  
|-----------|-----------------|  
|0|ユーティリティが正常に実行されました。|  
|1|ユーティリティが失敗しました。|  
|4|ユーティリティは要求されたパッケージを見つけることができません。|  
|5|ユーティリティは要求されたパッケージを読み込むことができません。|  
|6|コマンド ラインに構文エラーまたはセマンティック エラーのいずれかが含まれているため、ユーティリティはコマンド ラインを解決できません。|  
  
## <a name="remarks"></a>Remarks  
 **dtutil**でコマンド ファイルやリダイレクトを使用することはできません。  
  
 コマンド ライン内でのオプションの順序は重要ではありません。  
  
## <a name="examples"></a>使用例  
 次の例では、コマンド ラインの使用に関する一般的なシナリオについて説明します。  
  
### <a name="copy-examples"></a>コピーの例  
 Windows 認証を使用する **のローカル インスタンス上に** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースがあり、このデータベースに格納されているパッケージを SSIS パッケージ ストアにコピーするには、次の構文を使用します。  
  
```dos
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 パッケージをファイル システム上の場所から別の場所にコピーし、そのコピーに別の名前を付けるには、次の構文を使用します。  
  
```dos
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 ローカル ファイル システム上のパッケージを、別のコンピューター上でホストされている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスにコピーするには、次の構文を使用します。  
  
```dos
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 */DestU[ser]* オプションと */DestP[assword]* オプションが使用されていないため、Windows 認証の使用が想定されています。  
  
 コピー後にパッケージ用の新しい ID を作成するには、次の構文を使用します。  
  
```dos
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 特定のフォルダーにあるすべてのパッケージの新しい ID を作成するには、次の構文を使用します。  
  
```dos
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 コマンド プロンプトでコマンドを入力するときは、パーセント記号を 1 つ (%) 使用します。 バッチ ファイル内でコマンドを使用するときは、パーセント記号を 2 つ (%%) 使用します。  
  
### <a name="delete-examples"></a>削除の例  
 Windows 認証を使用する **のインスタンス上に** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースがあり、このデータベースに格納されているパッケージを削除するには、次の構文を使用します。  
  
```dos
dtutil /SQL delPackage /DELETE  
```  
  
 **認証を使用する** のインスタンス上に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースがあり、このデータベースに格納されているパッケージを削除するには、次の構文を使用します。  
  
```dos
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  パッケージを名前付きサーバーから削除するには、 **SOURCESERVER** オプションおよびそのオプションの引数を含めます。 *SQL* を使用する場合にのみサーバーを指定できます。  
  
 SSIS パッケージ ストアに格納されているパッケージを削除するには、次の構文を使用します。  
  
```dos
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 ファイル システムに格納されているパッケージを削除するには、次の構文を使用します。  
  
```dos
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### <a name="exists-examples"></a>存在確認の例  
 Windows 認証を使用する **のローカル インスタンス上に** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースがあり、このデータベースにパッケージが存在するかどうかを判断するには、次の構文を使用します。  
  
```dos
dtutil /SQL srcPackage /EXISTS  
```  
  
 **認証を使用する** のローカル インスタンス上に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースがあり、このデータベースにパッケージが存在するかどうかを判断するには、次の構文を使用します。  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  パッケージが名前付きサーバーに存在するかどうかを判断するには、 **SOURCESERVER** オプションおよびその引数を含めます。 サーバーを指定できるのは、SQL オプションを使用した場合のみです。  
  
 パッケージがローカルのパッケージ ストアに存在するかどうかを判断するには、次の構文を使用します。  
  
```dos
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 パッケージがローカルのファイル システムに存在するかどうかを判断するには、次の構文を使用します。  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### <a name="move-examples"></a>移動の例  
 SSIS パッケージ ストアに格納されているパッケージを、Windows 認証を使用する **のローカル インスタンス上の** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースに移動するには、次の構文を使用します。  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 **認証を使用する** のローカル インスタンス上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースに格納されているパッケージを、 **認証を使用する** の別のローカル インスタンス上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースに移動するには、次の構文を使用します。  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  ある名前付きサーバーから別の名前付きサーバーにパッケージを移動するには、 **SOURCES** オプションと **DESTS** オプション、および関連する引数を含めます。 *SQL* を使用する場合にのみサーバーを指定できます。  
  
 SSIS パッケージ ストアに格納されているパッケージを移動するには、次の構文を使用します。  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 ファイル システムに格納されているパッケージを移動するには、次の構文を使用します。  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### <a name="sign-examples"></a>署名の例  
 Windows 認証を使用する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のローカル インスタンス上に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースがあり、このデータベースに格納されているパッケージに署名するには、次の構文を使用します。  
  
```dos
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 証明書に関する情報を確認するには、 **CertMgr**を使用します。 ハッシュ コードを確認するには、 **CertMgr** ユーティリティで証明書を選択し、 **[表示]** をクリックしてプロパティを表示します。 **[詳細]** タブで、証明書に関する詳細な情報を確認できます。 **Thumbprint** プロパティはハッシュ値として使用されます。このとき、スペースは削除されます。  
  
> [!NOTE]  
>  上の例で使用しているハッシュは実際のハッシュではありません。  
  
 詳細については、「 [Signing and Checking Code with Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)」(Authenticode を使用したコードの署名と検証) の「CertMgr」を参照してください。  
  
### <a name="encrypt-examples"></a>暗号化の例  
 次の例では、完全パッケージ暗号化とパスワードを使用してファイルベースの PackageToEncrypt.dtsx を暗号化し、ファイルベースの EncryptedPackage.dts として保存します。 暗号化に使用されるパスワードは、 *EncPswd*です。  
  
```dos
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## <a name="see-also"></a>参照  
[Integration Services (SSIS) パッケージの実行](../integration-services/packages/run-integration-services-ssis-packages.md)  
  
  
