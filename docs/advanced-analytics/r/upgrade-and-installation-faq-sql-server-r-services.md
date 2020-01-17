---
title: アップグレードとインストールに関する FAQ
description: SQL Server での機械学習機能のインストールに関してよく寄せられる質問に回答します。
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6357f98627842ab790b494cf1b4a1f9b2110ec9c
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727348"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server Machine Learning または Microsoft R Server のアップグレードとインストールに関する FAQ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このトピックでは、SQL Server での機械学習機能のインストールに関してよく寄せられる質問に回答します。 また、アップグレードに関してよく寄せられる質問についても説明します。

+ 一部の問題は、リリース前のバージョンからのアップグレードでのみ発生します。 そのため、これらのメモを読む前に、まずバージョンとエディションを識別することをお勧めします。 バージョン情報を取得するには、SQL Server Management Studio からクエリで `@@VERSION` を実行します。
+ 最新のリリースまたはサービス リリースにできるだけ早くアップグレードし、最近のリリースで修正された問題を解決してください。

**適用対象:** SQL Server 2016 R Services、SQL Server Machine Learning Services (データベース内)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>以前のバージョンの SQL Server 2016 の要件と制限 

インストールする SQL Server のビルドによっては、次の制限事項が適用される場合があります。

- 以前のバージョンの SQL Server 2016 R Services では、作業ディレクトリを含むドライブに 8dot3 表記が必要でした。 リリース前のバージョンをインストールした場合は、SQL Server 2016 Service Pack 1 にアップグレードすると、この問題を解決する必要があります。 この要件は、SP1 以降のリリースには適用されません。

- SQL Server 2016 でフェールオーバー クラスターに [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] をインストールすることはできません。 ただし、SQL Server 2019 では、フェールオーバーのサポートが提供されます。 詳細については、「[新機能](../what-s-new-in-sql-server-machine-learning-services.md)」を参照してください。

- Azure VM では場合によって、追加的な構成が必要になることがあります。 たとえば、リモート アクセスをサポートするために、ファイアウォールの例外を作成する必要がある場合があります。

- 別のバージョンの R とのサイドバイサイドのインストール、または Revolution Analytics からの他のリリースはサポートされていません。

- セットアップを開始する前に、ウイルス スキャンを無効にします。 セットアップが完了したら、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] が使用するフォルダーのウイルス スキャンを中断することをお勧めします。 可能であれば、[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] ツリー全体でスキャンを中断します。

 - Windows Core にインストールされた SQL Server のインスタンスへの Microsoft R Server のインストール。 SQL Server 2016 の RTM バージョンでは、Windows Server Core エディションのインスタンスに Microsoft R Server を追加するときに問題が発生することがわかっていました。 この問題は修正されています。 この問題が発生する場合は、[KB3164398](https://support.microsoft.com/kb/3164398) に記載の修正プログラムを適用して、Windows Server Core の既存のインスタンスに R 機能を追加してください。 詳細については、 [「Can't install Microsoft R Server Standalone on a Windows Server Core operating system」](https://support.microsoft.com/kb/3168691)(Windows Server Core オペレーティング システムに Microsoft R Server (スタンドアロン) をインストールすることはできません) を参照してください。


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>ローカライズされた SQL Server 2016 のための機械学習コンポーネントのオフライン インストール

SQL Server 2016 の初期リリース バージョンでは、インターネットに接続しないオフライン セットアップ中にロケール固有の .cab ファイルをインストールできませんでした。 この問題は、後のリリースで修正されましたが、正しい言語をインストールできないというメッセージがインストーラーから返された場合は、ファイル名を編集してセットアップを続行することができます。

+ インストーラー ファイルを手動で編集して、正しい言語がインストールされていることを確認します。 たとえば、日本語バージョンの SQL Server をインストールする場合は、ファイル名を SRS_8.0.3.0_**1033**.cab から SRS_8.0.3.0_**1041**.cab に変更します。
+ 機械学習コンポーネントに使用される言語識別子は、インストールされる SQL Server セットアップ言語と同じにする必要があります。同じになっていない場合、セットアップを完了できません。

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>リリース前のバージョン: サポート ポリシー、アップグレード、および既知の問題

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] のリリース前のバージョンの新規インストールは、現在サポートされていません。 リリース前のバージョンを使用している場合は、できるだけ早くアップグレードしてください。

ここでは、特定のアップグレード シナリオについて、詳細な手順を説明します。

### <a name="how-to-upgrade-sql-server"></a>SQL Server をアップグレードする方法

セットアップ ウィザードを再実行して、SQL Server のバージョンをアップグレードできます。

+ [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)
+ [インストール ウィザードを使用して SQL Server をアップグレードする](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

バインドと呼ばれるプロセスを使用して、機械学習コンポーネントだけをアップグレードすることができます。 
+ [SqlBindR を使用して機械学習コンポーネントをアップグレードする](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>リリース前のバージョンからのインプレース アップグレードのサポート終了

SQL Server 2016 のリリース前バージョンからのアップグレードはサポートされなくなりました。 これには SQL Server 2016 CTP3、CTP 3.1、CTP 3.2、RC0、または RC1 が含まれます。

SQL Server 2016 のリリース前バージョンでは、次のバージョンがインストールされています。

| Version | ビルド         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

使用しているバージョンが不明な場合は、SQL Server Management Studio のクエリで `@@VERSION` を実行します。

一般的に、アップグレードのプロセスは次のとおりです。

1. スクリプトとデータをバックアップします。
2. リリース前バージョンをアンインストールします。
3. リリース バージョンをインストールします。

SQL Server がリリース前のバージョンの場合、機械学習コンポーネントのアンインストールが複雑で、特殊なスクリプトの実行が必要になる場合があります。 ご購入元に問い合わせてください。

###  <a name="bkmk_Uninstall"></a> 以前のバージョンの Microsoft R Server からアップグレードする前にアンインストールする

Microsoft R Server のプレリリース版がインストールされている場合は、それをアンインストールしてから新しいバージョンにアップグレードする必要があります。

1.  **[コントロール パネル]** を開き、 **[プログラムの追加と削除]** をクリックし、 `Microsoft SQL Server 2016 <version number>`を選択します。

2.  コンポーネントに対する **[追加]** 、 **[修復]** 、または **[削除]** オプションを含むダイアログ ボックスが表示されたら、 **[削除]** を選択します。
  
3.  **[機能の選択]** ページの **[共有機能]** で **[R Server (スタンドアロン)]** を選択します。 **[次へ]** をクリックし、 **[完了]** をクリックして、選択したコンポーネントのみをアンインストールします。

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services と Microsoft R Server (スタンドアロン) のサイドバイサイド エラー 

以前のバージョンの SQL Server 2016 では、Microsoft R Server (スタンドアロン) と R Services (データベース内) の両方を同時にインストールすると、セットアップが失敗し、「アクセスが拒否されました」というメッセージが表示されることがありました。 この問題は、SQL Server 2016 の Service Pack 1 で修正されました。

このエラーが発生した場合に、これらの機能をアップグレードする必要がある場合は、SP1 を使用して SQL Server 2016 のスリップストリーム インストールを実行してください。 この問題を解決するには 2 つの方法があり、どちらもアンインストールと再インストールが必要です。

1. R Services (データベース内) をアンインストールし、SQLRUserGroup のユーザー アカウントが削除されていることを確認します。

2. サーバーを再起動し、Microsoft R Server (スタンドアロン) を再インストールします。

3. Microsoft SQL Server のセットアップをもう一度実行し、今度は **[既存の Microsoft SQL Server に機能を追加]** を選択します。

4. インスタンスを選択し、 **[R Services (データベース内)]** オプションを選択して追加します。

このプロシージャで問題を解決できない場合は、次の回避策を試してください。

1. セットアップ中に、R Services (データベース内) と Microsoft R Server (スタンドアロン) を同時にアンインストールします。

2. ローカル ユーザー アカウント (SQLRUserGroup) を削除します。

3. サーバーを再起動します。

4. SQL Server セットアップを実行し、R Services (データベース内) 機能のみを追加します。 **Microsoft R Server (スタンドアロン)** は選択しないでください。

一般に、R Services (データベース内) と Microsoft R Server (スタンドアロン) の両方を同じコンピューターにインストールしないことをお勧めします。 ただし、サーバーに十分な容量があることを前提として、Microsoft R Server のスタンドアロンが開発ツールとして役に立つ場合があります。 もう1つの可能なシナリオでは、Microsoft R Server の運用化機能を使用する必要がありますが、データ移動せずに SQL Server のデータにアクセスしなければならなりません。

## <a name="incompatible-version-of-r-client-and-r-server"></a>R Client および R Server の互換性のないバージョン

Microsoft R Client をインストールし、それを使用してリモートの SQL Server コンピューティング コンテキストで R を実行すると、次のようなエラーが表示されることがあります。

*Microsoft R Server バージョン 8.0.3 と互換性のない、Microsoft R Client のバージョン 9.0.0 をコンピューター上で実行しています。互換性のあるバージョンをダウンロードしてインストールしてください。*

SQL Server 2016 では、SQL Server R Services で実行されていた R と、Microsoft R Client のライブラリがまったく同じバージョンである必要がありました。 この要件は、以降のバージョンでは削除されています。 ただし、常に最新バージョンの機械学習コンポーネントにバージョン変更し、すべての Service Pack をインストールすることをお勧めします。 

以前のバージョンの Microsoft R Server があり、Microsoft R Client 9.0.0 との互換性を確保する必要がある場合は、この[サポート記事](https://support.microsoft.com/kb/3210262)に記載されている更新プログラムをインストールしてください。


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>インストールに失敗し "Revolution Enterprise 製品は一度に 1 つしかインストールできません" というエラーが表示される

このエラーは、以前の Revolution Analytics 製品またはプレリリース版の SQL Server R Services がインストールされている場合に発生する可能性があります。 以前のバージョンが存在する場合は、そのアンインストールを行ってから、Microsoft R Server の新しいバージョンをインストールしてください。 他のバージョンの Revolution Enterprise ツールとのサイド バイ サイド インストールはサポートされていません。

ただし、サイド バイ サイド インストールは、R Server (スタンドアロン) を [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] または SQL Server 2016 と共に使用する場合はサポートされます。

## <a name="registry-cleanup-to-uninstall-older-components"></a>古いコンポーネントをアンインストールするレジストリのクリーンアップ

以前のバージョンの削除時に問題が発生する場合は、レジストリを編集して関連するキーを削除することが必要な場合があります。

> [!IMPORTANT]
> この問題は、プレリリース版の Microsoft R Server または CTP バージョンの SQL Server 2016 R Services がインストールされている場合にのみ発生します。
  
1. Windows レジストリを開き、 `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`キーを見つけます。
2. 次のエントリのいずれかが存在し、キーに値 `sEstimatedSize2`のみが含まれる場合は、該当するエントリを削除します。
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2 の場合)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1 の場合)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0 の場合)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0 の場合)

## <a name="see-also"></a>参照

 [SQL Server Machine Learning Services (データベース内)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (スタンドアロン)](../r/r-server-standalone.md)
