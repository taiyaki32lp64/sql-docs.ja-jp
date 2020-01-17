---
title: インストール ウィザードのヘルプ | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: b32ad209651c30f810f239b0c14689be497c4378
ms.sourcegitcommit: 8d01698e779a536093dd637e84c52f3ff0066a2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2019
ms.locfileid: "69609295"
---
# <a name="installation-wizard-help"></a>インストール ウィザードのヘルプ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの構成ページの一部について説明します。

## <a name="instance-configuration-page"></a>[インスタンスの構成] ページ

**インストール ウィザードの** [インスタンスの構成] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ページを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既定のインスタンスまたは名前付きインスタンスのどちらを作成するのかを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがまだインストールされていない場合は、名前付きインスタンスを指定しない限り、既定のインスタンスが作成されます。  
  
各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、照合順序などのオプションに固有の設定を持つ異なるサービス セットから構成されます。 ディレクトリ構造、レジストリ構造、およびサービス名には、すべて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中に作成されるインスタンス名および特定のインスタンス ID が反映されます。  
  
インスタンスには、既定のインスタンスと名前付きインスタンスがあります。 既定のインスタンス名は MSSQLSERVER です。 既定の名前では、接続時にクライアントでインスタンス名を指定する必要はありません。 名前付きインスタンスは、ユーザーがセットアップ中に指定します。 先に既定のインスタンスをインストールしなくても、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を名前付きインスタンスとしてインストールできます。 既定のインスタンスにできるのは、バージョンにかかわらず、一度に 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールだけです。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep では、 **[インスタンスの構成]** ページで準備済みインスタンスを完了するときにインスタンス名を指定できます。 コンピューター上に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既存のインスタンスがない場合は、完了しようとしている準備済みインスタンスを既存のインスタンスとして構成できます。  
  
### <a name="multiple-instances"></a>複数インスタンス
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、1 台のサーバー (1 つのプロセッサ) 上に複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスをインストールできます。ただし、既定のインスタンスにできるのはそのうち 1 つだけです。 その他のインスタンスはすべて、名前付きインスタンスにする必要があります。 コンピューターは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスを同時に実行でき、それぞれ他のインスタンスとは関係なく動作します。  
  
 詳しくは、「[SQL Server の最大容量仕様](../maximum-capacity-specifications-for-sql-server.md)」をご覧ください。  
  
### <a name="options"></a>オプション

**フェールオーバー クラスター インスタンス のみ**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのネットワーク名を指定します。 この名前は、ネットワーク上のフェールオーバー クラスター インスタンスを識別します。  
  
**既定のインスタンスまたは名前付きインスタンスの決定**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスと名前付きインスタンスのどちらをインストールするか決定する場合は、次の事項を考慮してください。  
  
* データベース サーバー上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の単独のインスタンスをインストールする場合は、そのインスタンスは既定のインスタンスであることが必要です。  
  
* 同じコンピューターで複数のインスタンスの使用を計画している場合は、名前付きインスタンスを使用します。 1 台のサーバーでは、既定のインスタンスを 1 つしかホストできません。  
* [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] をインストールするアプリケーションでは、名前付きインスタンスとしてインストールする必要があります。 これにより、複数のアプリケーションが同じコンピューターにインストールされたときの競合が最小限になります。
  
**既定のインスタンス**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスをインストールするには、このオプションを選択します。 1 台のコンピューターでホストできる既定のインスタンスは 1 つだけです。その他すべては名前付きインスタンスにする必要があります。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスをインストールしている場合は、その同じコンピューターに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のインスタンスを追加できます。  
  
**名前付きインスタンス**: 新しい名前付きインスタンスを作成するには、このオプションを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに名前を付けるときは、次の情報に注意してください。  
  
* インスタンス名では大文字と小文字が区別されません。  
  
* インスタンス名の先頭または末尾にアンダースコア (_) を使用することはできません。  
  
* インスタンス名には、"Default" などの予約されたキーワードを含めることはできません。 予約されたキーワードをインスタンス名に使用すると、セットアップ エラーが発生します。 詳細については、「[予約済みキーワード &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)」を参照してください。  
  
* インスタンス名として MSSQLSERVER を指定すると、既定のインスタンスが作成されます。  
  
* [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] は、常に "[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]" の名前付きインスタンスとしてインストールされます。 この機能ロール用に別のインスタンス名を指定することはできません。  
  
* インスタンス名は最大 16 文字まで指定できます。  
  
* インスタンス名の先頭は文字にする必要があります。 使用できる文字は、Unicode 規格 2.0 で定義されている文字です。 これらの文字には、ラテン文字 a から z と A から Z、および各国言語の文字が含まれます。  
  
* 2 文字目以降では、Unicode 規格 2.0 で定義されている文字、Basic Latin またはその他言語の 10 進数、ドル記号 ($)、アンダースコア (_) を使用できます。  
  
* 埋め込み型スペースなどの特殊文字は、インスタンス名に使用できません。 円記号 (\\)、コンマ (,)、コロン (:)、セミコロン (;)、単一引用符 (')、アンパサンド (&)、ハイフン (-)、およびアット マーク (@) も使用できません。  
  
  現在の Windows コード ページで有効な文字だけを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名に使用できます。 サポートされていない Unicode 文字を使用すると、セットアップ エラーが発生します。  
  
**検出されたインスタンスと機能**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行中のコンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとコンポーネントが一覧表示されます。  
  
**インスタンス ID**: 既定では、インスタンス名がインスタンス ID として使用されます。 この ID は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 既定のインスタンスの場合も名前付きインスタンスの場合も、同じ動作が発生します。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、**Instance ID** フィールドで指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep では、 **[インスタンスの構成]** ページに表示されるインスタンス ID は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep プロセスのイメージの準備手順で指定したインスタンス ID です。 イメージの完了手順では別のインスタンス ID を指定できません。

> [!NOTE]  
>  アンダースコア (_) で始まるインスタンス ID や、シャープ記号 (#) またはドル記号 ($) を含むインスタンス ID はサポートされません。  
  
ディレクトリ、ファイルの場所、およびインスタンス ID の名前付けの詳細については、「[SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](file-locations-for-default-and-named-instances-of-sql-server.md)」を参照してください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンスを構成するすべてのコンポーネントは 1 つの単位として管理されます。 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack とアップグレードが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの各コンポーネントに適用されます。  
  
同じインスタンス名を持つすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、次の条件を満たす必要があります。  
  
* 同じバージョン
* 同じエディション
* 同じ言語設定
* 同じクラスター状態
* 同じオペレーティング システム  
  
> [!NOTE]  
> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] はクラスターに対応していません。  

## <a name="analysis-services-configuration---account-provisioning-page"></a>[Analysis Services の構成] - [アカウントの準備] ページ
  
このページを使用すると、サーバー モードを設定し、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] への無制限アクセスを必要とするユーザーまたはサービスに管理権限を付与することができます。 セットアップでは、ローカル Windows グループ BUILTIN\Administrators が、インストールするインスタンスの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバー管理者ロールに自動的に追加されません。 サーバー管理者ロールにローカルの Administrators グループを追加する場合は、そのグループを明示的に指定する必要があります。  
  
[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールする場合は、[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] ファームでの [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] サーバーの配置に責任を負う SharePoint ファーム管理者またはサービス管理者に管理権限を付与してください。  
  
### <a name="options"></a>オプション

**[サーバー モード]** : サーバー モードでは、サーバーに配置できる [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの種類を指定します。 セットアップ中に指定したサーバー モードを後で変更することはできません。 各モードは互いに排他的です。そのため、従来のオンライン分析処理 (OLAP) ソリューションとテーブル モデル ソリューションの両方をサポートする場合は、それぞれ異なるモードで構成した 2 つの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスが必要になります。  
  
**[管理者の指定]** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのサーバー管理者を少なくとも 1 人指定する必要があります。 指定したユーザーまたはグループは、インストールする [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのサーバー管理者ロールのメンバーになります。 これらのメンバーは、ソフトウェアをインストールするコンピューターと同じドメインの Windows ドメイン ユーザー アカウントを持つ必要があります。  
  
> [!NOTE]  
> ユーザー アカウント制御 (UAC) は Windows セキュリティ機能であり、管理操作または管理アプリケーションの承認を管理者が実行前に明示的に行う必要があります。 UAC は既定でオンになっているため、高度な特権を必要とする特定の操作について許可するよう求めるメッセージが表示されます。 UAC を構成して既定の動作を変更することも、特定のプログラム用に UAC をカスタマイズすることもできます。 UAC および UAC 構成の詳細については、「[User Account Control Step by Step Guide (Windows ユーザー アカウント制御手順ガイド)](https://go.microsoft.com/fwlink/?linkid=196350)」と「[User Account Control (ユーザー アクセス制御)](https://go.microsoft.com/fwlink/?linkid=196351)」 (Wikipedia) を参照してください。  
  
### <a name="see-also"></a>参照
  
* [サービス アカウントの構成 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services)
* [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

## <a name="analysis-services-configuration---data-directories-page"></a>[Analysis Services の構成] - [データ ディレクトリ] ページ

次の表にある既定のディレクトリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ中にユーザーが構成できます。 これらのファイルへのアクセス許可は、ローカル管理者と、セットアップ中に作成およびプロビジョニングされる SQLServerMSASUser$\<インスタンス> セキュリティ グループのメンバーに付与されます。  
  
### <a name="uielement-list"></a>UIElement の一覧  
  
|[説明]|既定のディレクトリ|推奨事項|  
|-----------------|-----------------------|---------------------|  
|**データ ルート ディレクトリ**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data\ |\Program files\Microsoft SQL Server\ フォルダーが権限の制限により保護されていることを確認してください。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のパフォーマンスは、多くの構成で、データ ディレクトリが配置されているストレージのパフォーマンスに依存します。 このディレクトリは、システムに割り当てられている中でパフォーマンスが最も高いストレージに配置してください。 フェールオーバー クラスターのインストールの場合は、データ ディレクトリが共有ディスク上に配置されるようにしてください。|  
|**ログ ファイル ディレクトリ**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log\ |このディレクトリは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ログ ファイルのディレクトリであり、FlightRecorder ログを含んでいます。 フライト レコーダーの時間を増加する場合、ログ ディレクトリに十分な容量があることを確認してください。|  
|**Temp ディレクトリ**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp\ |Temp ディレクトリは、高パフォーマンスのストレージ サブシステムに配置してください。|  
|**バックアップ ディレクトリ**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup\ |このディレクトリは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のバックアップ ファイルのディレクトリです。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint のインストールでは、このディレクトリには [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] システム サービスによって [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ ファイルもキャッシュされます。<br /><br /> データの損失を防ぐために適切な権限を設定し、バックアップ ディレクトリに書き込むための適切な権限が [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のユーザー グループに付与されるようにしてください。 マップされたドライブをバックアップ ディレクトリに使用することはサポートされていません。|  
  
### <a name="considerations"></a>考慮事項  
  
* [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスでは、SharePoint ファームに配置されるときに、アプリケーション ファイル、データ ファイル、およびコンテンツ データベースのプロパティとサービス アプリケーション データベースのプロパティが格納されます。  
  
* 既存のインストールに機能を追加する場合、前にインストールした機能の場所は変更できません。また、新しい機能のインストール場所を指定することもできません。  

* SQL Server のフォルダーおよびファイルの種類を除外するように、ウイルス対策アプリケーションやスパイウェア対策アプリケーションなどのスキャン ソフトウェアを構成することが必要な場合があります。 詳細については、「[SQL Server を実行しているコンピューター上で実行するウイルス対策ソフトウェア](https://support.microsoft.com/kb/309422)」のサポート記事を参照してください。
  
* 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のインスタンスのディレクトリと共有しないでください。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内の [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンポーネントと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントは、別のディレクトリにインストールしてください。  
  
* 次の状況では、プログラム ファイルとデータ ファイルをインストールすることができません。  
  
  * リムーバブル ディスク ドライブ  
  * 圧縮を使用したファイル システム  
  * システム ファイルが配置されているディレクトリ  
  
### <a name="see-also"></a>参照

ディレクトリ、ファイルの場所、およびインスタンス ID の名前付けの詳細については、「[SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](file-locations-for-default-and-named-instances-of-sql-server.md)」を参照してください。  
  
### <a name="analysis-services-configuration---data-directories-page"></a>[Analysis Services の構成] - [データ ディレクトリ] ページ

次の表にある既定のディレクトリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ中にユーザーが構成できます。 これらのファイルへのアクセス許可は、ローカル管理者と、セットアップ中に作成およびプロビジョニングされる SQLServerMSASUser$\<インスタンス> セキュリティ グループのメンバーに付与されます。  
  
#### <a name="uielement-list"></a>UIElement の一覧
  
|[説明]|既定のディレクトリ|推奨事項|  
|-----------------|-----------------------|---------------------|  
|**データ ルート ディレクトリ** |\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data |\Program files\Microsoft SQL Server\ フォルダーが権限の制限により保護されていることを確認してください。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のパフォーマンスは、多くの構成で、データ ディレクトリが配置されているストレージのパフォーマンスに依存します。 このディレクトリは、システムに割り当てられている中でパフォーマンスが最も高いストレージに配置してください。 フェールオーバー クラスターのインストールの場合は、データ ディレクトリが共有ディスク上に配置されるようにしてください。|  
|**ログ ファイル ディレクトリ**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log |このディレクトリは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ログ ファイルのディレクトリであり、FlightRecorder ログを含んでいます。 フライト レコーダーの時間を増加する場合、ログ ディレクトリに十分な容量があることを確認してください。|  
|**Temp ディレクトリ**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp |Temp ディレクトリは、高パフォーマンスのストレージ サブシステムに配置してください。|  
|**バックアップ ディレクトリ**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup |このディレクトリは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のバックアップ ファイルのディレクトリです。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint のインストールでは、ここは [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] システム サービスによって [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ ファイルがキャッシュされる場所でもあります。<br /><br /> データの損失を防ぐために適切な権限を設定し、バックアップ ディレクトリに書き込むための適切な権限が [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービスのユーザー グループに付与されるようにしてください。 マップされたドライブをバックアップ ディレクトリに使用することはサポートされていません。|  
  
#### <a name="considerations"></a>考慮事項
  
* [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスでは、SharePoint ファームに配置されるときに、アプリケーション ファイル、データ ファイル、およびコンテンツ データベースのプロパティとサービス アプリケーション データベースのプロパティが格納されます。  
  
* 既存のインストールに機能を追加する場合、前にインストールした機能の場所は変更できません。また、新しい機能のインストール場所を指定することもできません。  

* SQL Server のフォルダーおよびファイルの種類を除外するように、ウイルス対策アプリケーションやスパイウェア対策アプリケーションなどのスキャン ソフトウェアを構成することが必要な場合があります。 詳細については、[Antivirus software on computers running SQL Server (SQL Server を実行するコンピューター上のウイルス対策ソフトウェア)](https://support.microsoft.com/kb/309422) に関する記事をご覧ください。
  
* 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のインスタンスのディレクトリと共有しないでください。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内の [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンポーネントと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントは、別のディレクトリにインストールしてください。  
  
* 次の状況では、プログラム ファイルとデータ ファイルをインストールすることができません。  
  
  * リムーバブル ディスク ドライブ  
  * 圧縮を使用したファイル システム  
  * システム ファイルが配置されているディレクトリ  
  
#### <a name="see-also"></a>参照

* ディレクトリ、ファイルの場所、およびインスタンス ID の名前付けの詳細については、「[SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](file-locations-for-default-and-named-instances-of-sql-server.md)」を参照してください。  
* [ファイル サーバーの共有アクセス許可と NTFS アクセス許可](https://docs.microsoft.com/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)

## <a name="serverconfig"></a> [データベース エンジンの構成] - [サーバー構成] ページ

このページは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ モードを設定し、Windows ユーザーまたはグループを [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] の管理者として追加するために使用します。  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の実行に関する注意点

以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のログインとして BUILTIN\Administrators グループが準備され、ローカル Administrators グループのメンバーは、管理者資格情報を使用してログインできました。 しかし、引き上げられたアクセス許可を使用するのはベスト プラクティスではありません。

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、BUILTIN\Administrators グループはログインとして準備されていません。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の新しいインスタンスのインストール時に、管理ユーザーごとに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを作成し、そのログインを **sysadmin** 固定サーバー ロールに追加する必要があります。 レプリケーション エージェント ジョブをなどの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行する Windows アカウントに対しても同じようにします。  
  
### <a name="options"></a>オプション

**[セキュリティ モード]** : インストール用に **Windows 認証**または**混合モード認証**を選択します。  
  
**[Windows Principal Provisioning]\(Windows プリンシパルのプロビジョニング\)** : 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Windows の BUILTIN\Administrators ローカル グループが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** サーバー ロールに配置されました。これにより、Windows 管理者に対し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへのアクセスが実質的に許可されました。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、BUILTIN\Administrators グループは **sysadmin** サーバー ロールで提供されません。 代わりに、セットアップ時に新規インストール用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者を明示的に用意する必要があります。  
  
> [!IMPORTANT]  
> セットアップ時に新規インストール用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者を明示的に用意する必要があります。 セットアップは、この手順を完了するまで続行できません。
  
**[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者の指定]** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの Windows プリンシパルを少なくとも 1 つ指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップを実行しているアカウントを追加するには、 **[現在のユーザーの追加]** ボタンを選択します。 システム管理者の一覧に対してアカウントを追加または削除するには、 **[追加]** または **[削除]** を選択し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスについて管理者特権を持っているユーザー、グループ、またはコンピューターの一覧を編集します。  
  
一覧の編集が完了したら、 **[OK]** を選択し、構成ダイアログ ボックスで管理者の一覧を確認します。 一覧が完成したら、 **[次へ]** を選択します。  
  
**混合モード認証**を選択した場合は、あらかじめ登録された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者 (**sa**) アカウントのログイン資格情報を入力する必要があります。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
**[Windows 認証モード]** : Windows ユーザー アカウントでユーザーが接続すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではオペレーティング システムの Windows プリンシパル トークンを使用してアカウント名とパスワードが検証されます。 Windows 認証は、既定の認証モードであり、混合モード認証よりはるかに安全性に優れています。 Windows 認証では、Kerberos セキュリティ プロトコルを使用し、強力なパスワードに対して複雑な検証を行うという点で、パスワード ポリシーが強化されています。また、アカウント ロックアウトの機能が提供され、パスワード有効期限にも対応しています。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  

> [!IMPORTANT]  
> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]**sa** パスワードを空白のままにしたり、推測されやすいパスワードを設定したりしないでください。  
  
**[混合モード] (Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証)** : Windows 認証または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用してユーザー接続を許可します。 Windows ユーザー アカウントで接続するユーザーは、Windows によって検証される信頼関係接続を使用することができます。  
  
混合モード認証を選択する必要があり、レガシ アプリケーションに対応するために SQL ログインを使用する必要もある場合は、必ずすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントに強力なパスワードを設定してください。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証は旧バージョンとの互換性を維持するためだけに提供されます。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
**[パスワードの入力]** : システム管理者 (**sa**) ログインを入力および確認します。 パスワードは侵入者に対する防御の最前線であるため、システムのセキュリティにとって強力なパスワードを設定することは不可欠です。 **sa** パスワードを空白のままにしないでください。また、推測しやすいパスワードを設定しないでください。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パスワードは、文字、記号、数字の組み合わせを含む 1 ～ 128 文字で指定できます。 混合モード認証を選択する場合、インストール ウィザードの次のページに進む前に、強力な **sa** パスワードを入力する必要があります。  
  
#### <a name="strong-password-guidelines"></a>強力なパスワードのガイドライン
  
強力なパスワードとは、他人によってたやすく推測されず、コンピューター プログラムを使用して簡単にはハッキングされないパスワードです。 強力なパスワードでは、次のような禁止された条件または用語を使用することはできません。  
  
* 空白または NULL 条件
* "Password"
* "Admin"
* "Administrator"
* "sa"
* "sysadmin"

強力なパスワードには、インストール コンピューターに関連付けられた次のような用語を指定できません。  
  
* 現在、コンピューターにログインしているユーザーの名前
* コンピューター名  
  
強力なパスワードは、長さ 9 文字以上で、以下の 4 つの条件のうち 3 つ以上を満たしている必要があります。  
  
* 大文字を含んでいる。
* 小文字を含んでいる。  
* 数字を含んでいる。
* #、%、^ など、英数字以外の文字を含んでいる。  
  
このページで入力するパスワードは、強力なパスワード ポリシーの要件を満たす必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用したオートメーションを使用している場合、必ず強力なパスワード ポリシーの要件を満たすパスワードを指定してください。  
  
### <a name="see-also"></a>参照

Windows 認証と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のどちらを選択するかについて詳しくは、「[認証モードの選択](../../relational-databases/security/choose-an-authentication-mode.md)」を参照してください。  

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] を実行するアカウントの選択の詳細については、「[Windows サービス アカウントとアクセス許可の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」をご覧ください。

## <a name ="datadir"></a> [データベース エンジンの構成] - [データ ディレクトリ] ページ

このページを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]のプログラムおよびデータ ファイルのインストール場所を指定します。 インストールの種類により、サポートされるストレージにはローカル ディスク、共有ストレージ、または SMB ファイル サーバーが含まれる場合があります。  
  
SMB ファイル共有をディレクトリとして指定するには、サポートされている UNC パスを手動で入力する必要があります。 SMB ファイル共有を参照して指定することはできません。 SMB ファイル共有のサポートされる UNC パス形式の例を次に示します。

`\\<ServerName>\<ShareName>\...`

### <a name="standalone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンス
  
次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスでの、サポートされているストレージの種類と、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中に構成できる既定のディレクトリの一覧です。  
  
### <a name="uielement-list"></a>UIElement の一覧
  
|[説明]|サポートされているストレージの種類|既定のディレクトリ|推奨事項|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**データ ルート ディレクトリ**|ローカル ディスク、SMB ファイル サーバー、共有ストレージ* |\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリのアクセス制御リスト (ACL) が構成され、構成の一部として継承が無効になります。|  
|**ユーザー データベース ディレクトリ**|ローカル ディスク、SMB ファイル サーバー、共有ストレージ*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data |ユーザー データ ディレクトリのベスト プラクティスは、ワークロードとパフォーマンスの要件によって異なります。|  
|**ユーザー データベース ログ ディレクトリ**|ローカル ディスク、SMB ファイル サーバー、共有ストレージ*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|ログ ディレクトリに十分な領域があることを確認してください。|  
|**バックアップ ディレクトリ**|ローカル ディスク、SMB ファイル サーバー、共有ストレージ*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup|データの損失を防ぐために適切な権限を設定して、バックアップ ディレクトリに書き込むための適切な権限が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのユーザー アカウントにあることを確認してください。 マップされたドライブをバックアップ ディレクトリに使用することはサポートされていません。|  
  
\* 共有ディスクがサポートされていますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスに対して使用することはお勧めしません。  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンス

次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンスでの、サポートされているストレージの種類と、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中に構成できる既定のディレクトリの一覧です。  
  
|[説明]|サポートされているストレージの種類|既定のディレクトリ|推奨事項|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**データ ルート ディレクトリ**|共有ストレージ、SMB ファイル サーバー|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> **ヒント**: **[クラスター ディスクの選択]** ページで**共有ディスク**を選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しない場合、このフィールドの既定値は空白になります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリの ACL が構成され、構成の一部として継承が無効になります。|  
|**ユーザー データベース ディレクトリ**|共有ストレージ、SMB ファイル サーバー|\<Drive:>Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> **ヒント**: **[クラスター ディスクの選択]** ページで**共有ディスク**を選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しない場合、このフィールドの既定値は空白になります。|ユーザー データ ディレクトリのベスト プラクティスは、ワークロードとパフォーマンスの要件によって異なります。|  
|**ユーザー データベース ログ ディレクトリ**|共有ストレージ、SMB ファイル サーバー|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> **ヒント**: **[クラスター ディスクの選択]** ページで**共有ディスク**を選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しない場合、このフィールドの既定値は空白になります。|ログ ディレクトリに十分な領域があることを確認してください。|  
|**バックアップ ディレクトリ**|ローカル ディスク、共有ストレージ、SMB ファイル サーバー|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup<br /><br /> **ヒント**: **[クラスター ディスクの選択]** ページで**共有ディスク**を選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しない場合、このフィールドの既定値は空白になります。|データの損失を防ぐために適切な権限を設定して、バックアップ ディレクトリに書き込むための適切な権限が SQL Server サービスのユーザー アカウントにあることを確認してください。 マップされたドライブをバックアップ ディレクトリに使用することはサポートされていません。|  
  
### <a name="security-considerations"></a>セキュリティに関する考慮事項
  
セットアップにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリの ACL が構成され、構成の一部として継承が無効になります。  
  
次の推奨事項は SMB ファイル サーバーに当てはまります。  
  
* SMB ファイル サーバーを使用する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントはドメイン アカウントである必要があります。  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに使用するアカウントには、データ ディレクトリとして使用する SMB ファイル共有フォルダーに対するフル コントロールの NTFS 権限が必要です。  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに使用するアカウントには、SMB ファイル サーバーに対する SeSecurityPrivilege 特権を付与する必要があります。 この特権を付与するには、ファイル サーバーで [ローカル セキュリティ ポリシー] コンソールを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査とセキュリティ ログの管理 **ポリシーに** セットアップ アカウントを追加します。 この設定は、[ローカル セキュリティ ポリシー] コンソールの **[ローカル ポリシー]** の **[ユーザー権利の割り当て]** セクションにあります。

### <a name="considerations"></a>考慮事項
  
* 既存のインストールに機能を追加する場合、前にインストールした機能の場所は変更できません。また、新しい機能のインストール場所を指定することもできません。  
  
* 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリを、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他のインスタンスのディレクトリと共有しないでください。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内の [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンポーネントと [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントは、別のディレクトリにインストールしてください。  
  
* 次の状況では、プログラム ファイルとデータ ファイルをインストールすることができません。  
  
  * リムーバブル ディスク ドライブ
  * 圧縮を使用したファイル システム
  * システム ファイルが配置されているディレクトリ
  * フェールオーバー クラスター インスタンス上のマップされたネットワーク ドライブ  
  
## <a name="a-nametempdba-database-engine-configuration---tempdb-page"></a><a name="tempdb"><a/> [データベース エンジンの構成] - [TempDB] ページ

このページを利用し、**tempdb** のデータとログ ファイルの場所、サイズ、拡張設定、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]のファイル数を指定します。 インストールの種類により、サポートされるストレージにはローカル ディスク、共有ストレージ、または SMB ファイル サーバーが含まれる場合があります。  
  
SMB ファイル共有をディレクトリとして指定するには、サポートされている UNC パスを手動で入力する必要があります。 SMB ファイル共有を参照して指定することはできません。 SMB ファイル共有のサポートされる UNC パス形式の例を次に示します。

`\\<ServerName>\<ShareName>\....`
  
### <a name="data-and-log-directories-for-a-standalone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスのデータとログのディレクトリ

次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスでの、サポートされているストレージの種類と、セットアップ中に構成できる既定のディレクトリの一覧です。  
  
|[説明]|サポートされているストレージの種類|既定のディレクトリ|推奨事項|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**データ ディレクトリ**|ローカル ディスク、SMB ファイル サーバー、共有ストレージ* |\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリの ACL が構成され、構成の一部として継承が無効になります。<br /><br /> **tempdb** ディレクトリのベスト プラクティスは、ワークロードとパフォーマンスの要件によって異なります。 データ ファイルを複数のボリュームに分散させるには、複数のフォルダーまたはドライブを指定します。|  
|**ログ ディレクトリ**|ローカル ディスク、SMB ファイル サーバー、共有ストレージ*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|ログ ディレクトリに十分な領域があることを確認してください。|  
  
\* 共有ディスクがサポートされていますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスに対して使用することはお勧めしません。  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンスのデータとログのディレクトリ

次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンスでの、サポートされているストレージの種類と、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中に構成できる既定のディレクトリの一覧です。  
  
|[説明]|サポートされているストレージの種類|既定のディレクトリ|推奨事項|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**tempdb データ ディレクトリ**|ローカル ディスク、共有ストレージ、SMB ファイル サーバー|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\Data<br /><br /> **ヒント**: **[クラスター ディスクの選択]** ページで**共有ディスク**を選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しない場合、このフィールドの既定値は空白になります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリの ACL が構成され、構成の一部として継承が無効になります。<br /><br /> 指定のディレクトリ (複数のファイルが指定される場合、ディレクトリも複数になります) はすべてのクラスター ノードで有効にします。 フェールオーバー中に、**tempdb** のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、SQL Server リソースはオンラインへの移行に失敗します。|  
|**tempdb ログ ディレクトリ**|ローカル ディスク、共有ストレージ、SMB ファイル サーバー|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> **ヒント**: **[クラスター ディスクの選択]** ページで**共有ディスク**を選択した場合、既定値は最初の共有ディスクになります。 **[クラスター ディスクの選択]** ページで何も選択しない場合、このフィールドの既定値は空白になります。|ユーザー データ ディレクトリのベスト プラクティスは、ワークロードとパフォーマンスの要件によって異なります。<br /><br /> 指定したディレクトリがすべてのクラスター ノードで有効であることを確認してください。 フェールオーバー中に、**tempdb** のディレクトリがフェールオーバーのターゲット ノード上で利用できない場合、SQL Server リソースはオンラインへの移行に失敗します。<br /><br /> ログ ディレクトリに十分な領域があることを確認してください。|  
  
### <a name="uielement-list"></a>UIElement の一覧

作業負荷と要件に合わせて **tempdb** の設定を構成します。 次の設定は、 **tempdb** データ ファイルに適用されます。  
  
* **ファイル数** は **tempdb**のデータ ファイルの合計数です。 既定値は 8 とセットアップ時に検出された論理コア数の小さいほうになります。 一般的なルールとして、論理プロセッサの数が 8 以下の場合、論理プロセッサと同じ数のデータ ファイルを使用します。 論理プロセッサの数が 8 より大きい場合、8 つのデータ ファイルを使用します。 競合が発生する場合は、競合が許容できるレベルに低下するまでデータ ファイルの数を 4 の倍数分ずつ増やすか(最大で、論理プロセッサの数まで)、ワークロードまたはコードを変更します。
  
* **初回サイズ (MB)** は各 **tempdb** データ ファイルの初回サイズです (メガバイト単位)。 既定値は 8 MB です (または、[!INCLUDE[ssexpress](../../includes/ssexpress_md.md)] の場合は 4 MB)。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] では、最大初期ファイル サイズ 262,144 MB (256 GB) が導入されます。 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] の最大初期ファイル サイズは 1024 MB です。 すべての **tempdb** データ ファイルの初回サイズは同じです。 **tempdb** は SQL Server が起動するか、フェールオーバーするたびに再作成されるため、通常の作業のワークロードに必要なサイズに近いサイズを指定します。 起動時にさらに効率的に **tempdb** を作成するには、[データベースのファイルの瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)を有効にします。  
  
* **合計初回サイズ (MB)** は、すべての **tempdb** データ ファイルを合計したものです。  
  
* **自動拡張 (MB)** はメガバイト単位で表した領域です。各 **tempdb** データ ファイルの領域が枯渇すると、このサイズ分だけ自動的に拡張されます。 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 以降では、すべてのデータ ファイルがこの設定で指定された量だけ同時に拡張されます。  
  
* **自動拡張の合計 (MB)** は各自動拡張イベントを合計したものです。  
* **データ ディレクトリ** には、**tempdb** データ ファイルを維持しているすべてのディレクトリが表示されます。 ディレクトリが複数存在するとき、データ ファイルはラウンド ロビン方式でディレクトリに置かれます。 たとえば、3 つのディレクトリを作成し、8 つのデータ ファイルを指定する場合、データ ファイル 1、4、7 が最初のディレクトリに作成されます。 データ ファイル 2、5、8 が 2 番目のディレクトリに作成されます。 データ ファイル 3 と 6 が 3 番目のディレクトリに入ります。  
  
* ディレクトリを追加するには、 **[追加…]** を選択します。  
  
* ディレクトリを削除するには、ディレクトリを選択し、 **[削除]** を選択します。  
  
**[Tempdb ログ ファイル]** はログ ファイルの名前です。 このファイルは自動的に作成されます。 次の設定は、 **tempdb** ログ ファイルにのみ適用されます。  
  
* **初回サイズ (MB)** は **tempdb** ログ ファイルの初回サイズです。 既定値は 8 MB です (または、[!INCLUDE[ssexpress](../../includes/ssexpress_md.md)] の場合は 4 MB)。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] では、最大初期ファイル サイズ 262,144 MB (256 GB) が導入されます。 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] の最大初期ファイル サイズは 1024 MB です。 **tempdb** は SQL Server が起動するか、フェールオーバーするたびに再作成されるため、通常の作業のワークロードに必要なサイズに近いサイズを指定します。 起動時にさらに効率的に **tempdb** を作成するには、[データベースのファイルの瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)を有効にします。  
  
  > [!NOTE]
  > **Tempdb** では、最小ログ記録が利用されます。 **tempdb** ログ ファイルはバックアップできません。 SQL Server が起動するたびに、あるいはクラスター インスタンスのフェールオーバー時に再作成されます。

* **自動拡張 (MB)** は **tempdb** ログの拡張単位であり、メガバイト単位で指定されます。  既定値の 64 MB で、初期化中、最適な数の仮想ログ ファイルが作成されます。  

  > [!NOTE]
  > **Tempdb** ログ ファイルでは、データベースのファイルの瞬時初期化は利用されません。
  
* **ログ ディレクトリ** は、 **tempdb** ログ ファイルが作成されるディレクトリです。 **tempdb** ログ ディレクトリは 1 つだけ存在します。  
  
### <a name="security-considerations"></a>セキュリティに関する考慮事項
  
セットアップにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディレクトリの ACL が構成され、構成の一部として継承が無効になります。  

次の推奨事項は SMB ファイル サーバーに当てはまります。  
  
* SMB ファイル サーバーを使用する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントはドメイン アカウントである必要があります。  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに使用するアカウントには、データ ディレクトリとして使用する SMB ファイル共有フォルダーに対する**フル コントロール**の NTFS 権限が必要です。  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに使用するアカウントには、SMB ファイル サーバーに対する SeSecurityPrivilege 特権を付与する必要があります。 この特権を付与するには、ファイル サーバーで [ローカル セキュリティ ポリシー] コンソールを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査とセキュリティ ログの管理 **ポリシーに** セットアップ アカウントを追加します。 この設定は、[ローカル セキュリティ ポリシー] コンソールの **[ローカル ポリシー]** の **[ユーザー権利の割り当て]** セクションにあります。  
  
> [!NOTE]
> 既定以外のインストール ディレクトリを指定する場合は、個々のインストール フォルダーがこの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して一意であることを確認します。 このダイアログ ボックスのディレクトリは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のインスタンスのディレクトリと共有できません。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンス内の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、別のディレクトリにインストールする必要もあります。
  
### <a name="see-also"></a>参照

* [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)
* [ファイル サーバーの共有アクセス許可と NTFS アクセス許可](https://docs.microsoft.com/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)  

<!--
The MaxDOP setting applies only to SQL Server 2019 and later.
-->

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="a-namemaxdopa-database-engine-configuration---maxdop-page"></a><a name="maxdop"><a/> [データベース エンジンの構成] - [MAXDOP] ページ

**並列処理の最大限度 (MaxDOP)** により、1 つのステートメントで使用できるプロセッサの最大数が決まります。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、インストール時にこのオプションを構成する機能が導入されています。 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] では、また、サーバー用の推奨される MaxDOP 設定が、コア数に基づいて自動的に検出されます。  

セットアップ中にこのページをスキップした場合、MaxDOP の既定値は、以前のバージョン (0) に対する [!INCLUDE[ssde_md](../../includes/ssde_md.md)] の既定値ではなく、このページに表示される推奨値になります。 また、このページでこの設定を手動で構成し、インストール後にこの設定を変更することができます。 

### <a name="uielement-list"></a>UIElement の一覧

* **[並列処理の最大限度] (MaxDOP)** は、1 つのステートメントの並列実行中に使用するプロセッサの最大数の値です。 既定値は、「[max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)」の並列処理の最大限度ガイドラインと一致します。

## <a name="a-namememorya-database-engine-configuration---memory-page"></a><a name="memory"><a/> [データベース エンジンの構成] - [メモリ] ページ

**[最小サーバー メモリ]** では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] でバッファー プールとその他のキャッシュに使用されるメモリの下限が決まります。 既定値は 0 で、推奨値も 0 です。 **最小サーバー メモリ**の効果について詳しくは、「[メモリ管理アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md#effects-of-min-and-max-server-memory)」をご覧ください。

**[最大サーバー メモリ]** では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] でバッファー プールとその他のキャッシュに使用されるメモリの上限が決まります。 既定値は 2,147,483,647 メガバイト (MB) であり、計算された推奨値は、「[サーバー メモリの構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)」の、既存のシステム メモリに基づくスタンドアロン [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対するメモリ構成ガイドラインと一致します。 **最大サーバー メモリ**の効果について詳しくは、「[メモリ管理アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md#effects-of-min-and-max-server-memory)」をご覧ください。

セットアップの間にこのページをスキップした場合に使用される既定の**最大サーバー メモリ**の値は、[!INCLUDE[ssde_md](../../includes/ssde_md.md)] の既定値 (2,147,483,647 メガバイト) です。 **[推奨]** ラジオ ボタンを選択すると、このページでこれらの設定を手動で構成でき、インストール後にこれらの設定を変更できます。 詳細については、 [サーバー メモリ構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)の設定を参照してください。

### <a name="uielement-list"></a>UIElement の一覧
  
**Default**:このラジオ ボタンは既定で選択されており、**最小サーバー メモリ**と**最大サーバー メモリ**の設定は [!INCLUDE[ssde_md](../../includes/ssde_md.md)] の既定値に設定されます。 

**[推奨]** : 計算された推奨値を受け入れる場合、または計算された値をユーザー構成値に変更する場合は、このラジオ ボタンを選択する必要があります。  
  
**[最小サーバー メモリ (MB)]** : 計算された推奨値からユーザー構成値に変更する場合は、**最小サーバー メモリ**の値を入力します。  
  
**[最大サーバー メモリ (MB)]** : 計算された推奨値からユーザー構成値に変更する場合は、**最大サーバー メモリ**の値を入力します。  

**[SQL Server データベース エンジン用に推奨されているメモリ構成を受け入れるには、ここをクリックします]** : このサーバーで計算された推奨メモリ構成を受け入れるには、このチェック ボックスをオンにします。 **[推奨]** ラジオ ボタンを選択した場合、このチェック ボックスをオンにしないとセットアップを続行できません。

::: moniker-end

## <a name="database-engine-configuration---filestream-page"></a>[データベース エンジンの構成] - [FILESTREAM] ページ

このページを使用すると、このインストールの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に対して FILESTREAM を有効にすることができます。 FILESTREAM では、**varbinary(max)** BLOB (バイナリ ラージ オブジェクト) データをファイル システム内のファイルとして格納することにより、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] と NTFS ファイル システムが統合されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、FILESTREAM データの挿入、更新、クエリ、検索、およびバックアップを行うことができます。 Microsoft Win32 ファイル システム インターフェイスによるデータへのストリーミング アクセスが可能になります。 
  
### <a name="uielement-list"></a>UIElement の一覧
  
**[Transact-SQL アクセスに対して FILESTREAM を有効にする]** : [!INCLUDE[tsql](../../includes/tsql-md.md)] アクセスに対して FILESTREAM を有効にする場合にオンにします。 他のオプションを使用するには、先にこのチェック ボックスをオンにする必要があります。  
  
**[ファイル I/O ストリーム アクセスに対して FILESTREAM を有効にする]** : FILESTREAM の Win32 ストリーム アクセスを有効にする場合にオンにします。  
  
**[Windows 共有名]** : FILESTREAM データを格納する Windows 共有の名前を入力します。  
  
**[リモート クライアントに FILESTREAM データへのストリーム アクセスを許可する]** : リモート クライアントにこのサーバー上の FILESTREAM データへのアクセスを許可するには、このチェック ボックスをオンにします。  
  
### <a name="see-also"></a>参照

* [FILESTREAM の有効化と構成](../../relational-databases/blob/enable-and-configure-filestream.md)
* [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

## <a name="database-engine-configuration---user-instance-page"></a>[データベース エンジンの構成] - [ユーザー インスタンス] ページ

**[ユーザー インスタンス]** ページは次の目的に使用します。

* 管理者アクセス許可を持たないユーザー用に [!INCLUDE[ssDE](../../includes/ssde-md.md)] の別のインスタンスを生成します。
* ユーザーを管理者ロールに追加します。  
  
### <a name="options"></a>オプション
  
**[ユーザー インスタンスを有効にする]** : 既定値はオンです。 ユーザー インスタンスを有効にする機能を無効にするには、チェック ボックスをオフにします。  
  
ユーザー インスタンスは子インスタンスまたはクライアント インスタンスとも呼ばれ、ユーザーに代わって親インスタンス ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] などのサービスを実行するプライマリ インスタンス) によって作成される [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]のインスタンスです。 ユーザー インスタンスは、そのユーザーのセキュリティ コンテキストでのユーザーのプロセスとして実行します。 親インスタンスやコンピューター上で実行するその他のユーザー インスタンスとは分離されます。 ユーザー インスタンス機能は "通常のユーザーとして実行" (Run As Normal User: RANU) とも呼ばれます。  
  
> [!NOTE]  
> セットアップ中に **sysadmin** 固定サーバー ロールのメンバーとして準備されたログインは、テンプレート データベース内の管理者として準備されます。 削除されない限り、これらはユーザー インスタンス上の **sysadmin** 固定サーバー ロールのメンバーです。  
  
**[Add user to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Administrator role]\(SQL Server 管理者ロールにユーザーを追加する\)** : 既定値はオフです。 現在のセットアップ ユーザーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者ロールに追加するには、このチェック ボックスをオンにします。  
  
[!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] ユーザーのうち、BUILTIN\Administrators のメンバーは、[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] への接続時に **sysadmin** 固定サーバー ロールに自動的に追加されません。 サーバーレベルの管理者ロールに明示的に追加されている [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] ユーザーのみが、[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] を管理できます。 Built-In\Users グループのメンバーは、[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] インスタンスに接続できますが、データベース タスクを行うアクセス許可は制限されます。 このため、[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 特権を以前のリリースの Windows の BUILTIN\Administrators および Built-In\Users から継承しているユーザーには、[!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] で実行している [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] のインスタンスにおいて、管理特権を明示的に付与する必要があります。  
  
インストール プログラムの終了後にユーザー ロールを変更するには、[SQL Server Management Studio](../../relational-databases/security/authentication-access/join-a-role.md) または [Transact-SQL](../../t-sql/statements/alter-role-transact-sql.md) を使用します。
