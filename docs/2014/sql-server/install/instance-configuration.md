---
title: インスタンスの構成 |Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 66329d4c25a23a6b3dbc3570723bab8aecfa3d4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68190965"
---
# <a name="instance-configuration"></a>インスタンスの構成
  **インストール ウィザードの** [インスタンスの構成] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ページを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既定のインスタンスまたは名前付きインスタンスのどちらを作成するのかを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがまだインストールされていない場合は、名前付きインスタンスを指定しない限り、既定のインスタンスが作成されます。  
  
 各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、照合順序などのオプションに固有の設定を持つ異なるサービス セットから構成されます。 ディレクトリ構造、レジストリ構造、およびサービス名には、すべて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ中に作成されるインスタンス名および特定のインスタンス ID が反映されます。  
  
 インスタンスには、既定のインスタンスと名前付きインスタンスがあります。 既定のインスタンス名は MSSQLSERVER です。 接続時に、クライアントでインスタンス名を指定する必要はありません。 名前付きインスタンスは、ユーザーがセットアップ中に指定します。 先に既定のインスタンスをインストールしなくても、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を名前付きインスタンスとしてインストールできます。 既定のインスタンスにできるのは、バージョンにかかわらず、一度に 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールだけです。  
  
 **警告!** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep では、 **[インスタンスの構成]** ページで準備済みインスタンスを完了するときにインスタンス名を指定できます。 コンピューター上に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既存のインスタンスがない場合は、完了しようとしている準備済みインスタンスを既存のインスタンスとして構成するように選択できます。  
  
## <a name="multiple-instances"></a>複数のインスタンス  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、1 台のサーバー (1 つのプロセッサ) 上に複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスをインストールできます。ただし、既定のインスタンスにできるのはそのうち 1 つだけです。 その他のインスタンスはすべて、名前付きインスタンスにする必要があります。 コンピューターは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスを同時に実行でき、それぞれ他のインスタンスとは関係なく動作します。  
  
 詳しくは、「 [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md)」をご覧ください。  
  
## <a name="options"></a>および  
 フェールオーバー クラスター インスタンスのみ - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのネットワーク名を指定します。 この名前は、ネットワーク上のフェールオーバー クラスター インスタンスを識別します。  
  
 既定のインスタンスまたは名前付きインスタンス - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスと名前付きインスタンスのどちらをインストールするか決定する場合は、次の事項を考慮してください。  
  
-   データベース サーバー上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の単独のインスタンスをインストールする場合は、そのインスタンスは既定のインスタンスであることが必要です。  
  
-   同じコンピューターで複数のインスタンスの使用を計画している場合は、名前付きインスタンスを使用します。 1 台のサーバーでは、既定のインスタンスを 1 つしかホストできません。  
  
-   [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] をインストールするアプリケーションでは、名前付きインスタンスとしてインストールする必要があります。 これにより、複数のアプリケーションが同じコンピューターにインストールされた場合に競合が発生する可能性が軽減されます。  
  
 **[既定のインスタンス]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスをインストールするには、このオプションを選択します。 1 台のコンピューターでホストできる既定のインスタンスは 1 つだけです。その他すべては名前付きインスタンスにする必要があります。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスをインストールしている場合は、その同じコンピューターに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のインスタンスを追加できます。  
  
 **[名前付きインスタンス]**  
 新しい名前付きインスタンスを作成するには、このオプションを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに名前を付ける際は、次の点に注意してください。  
  
-   インスタンス名では大文字と小文字が区別されません。  
  
-   インスタンス名の先頭または末尾にアンダースコア (_) を使用することはできません。  
  
-   インスタンス名には、"Default" などの予約されたキーワードを含めることはできません。 予約されたキーワードをインスタンス名に使用すると、セットアップ エラーが発生します。 詳細については、「[予約済みキーワード &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)」を参照してください。  
  
-   インスタンス名として MSSQLServer を指定すると、既定のインスタンスが作成されます。  
  
-   [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] は、常に 'PowerPivot' の名前付きインスタンスとしてインストールされます。 この機能ロール用に別のインスタンス名を指定できます。  
  
-   インスタンス名は最大 16 文字まで指定できます。  
  
-   インスタンス名の先頭は文字にする必要があります。 使用できる文字は、Unicode 規格 2.0 で定義されている文字です。 これには、ラテン文字 a ～ z と A ～ Z、および各国言語の文字が含まれます。  
  
-   2 文字目以降では、Unicode 規格 2.0 で定義されている文字、Basic Latin またはその他言語の 10 進数、ドル記号 ($)、アンダースコア (_) を使用できます。  
  
-   埋め込み型スペースなどの特殊文字は、インスタンス名に使用できません。 円記号 (\\)、コンマ (,)、コロン (:)、セミコロン (;)、単一引用符 (')、アンパサンド (&)、ハイフン (-)、およびアット マーク (@) も使用できません。  
  
-   **現在の Windows コード ページで有効な文字のみで使用できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス名。サポートされていない Unicode 文字を使用すると、セットアップ エラーが発生します。**  
  
 **検出されたインスタンスと機能**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行中のコンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとコンポーネントが一覧表示されます。  
  
 **[インスタンス ID]** : 既定では、インスタンス名がインスタンス ID として使用されます。 これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのインストール ディレクトリとレジストリ キーを識別するために使用されます。 これは、既定のインスタンスの場合も名前付きインスタンスの場合も同様です。 既定のインスタンスの場合、インスタンス名とインスタンス ID は、MSSQLSERVER になります。 既定以外のインスタンス ID を使用するには、 **Instance ID** フィールドで指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep では、このページに表示されるインスタンス ID は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep プロセスのイメージの準備手順で指定したインスタンス ID です。 イメージの完了手順では別のインスタンス ID を指定できません。  
  
> [!NOTE]  
>  アンダースコア (_) で始まるインスタンス ID や、シャープ記号 (#) またはドル記号 ($) を含むインスタンス ID はサポートされません。  
  
 ディレクトリ、ファイルの場所、およびインスタンス ID の名前付けの詳細については、「[SQL Server の既定のインスタンスおよび名前付きインスタンスのファイルの場所](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンスを構成するすべてのコンポーネントは 1 つの単位として管理されます。 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack とアップグレードは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの各コンポーネントに適用されます。  
  
 同じインスタンス名を持つすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、次の条件を満たす必要があります。  
  
-   **同じバージョン**  
  
-   **同じエディション**  
  
-   **同じ言語設定**  
  
-   **同じクラスター状態**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] はクラスターに対応していません。  
  
-   **同じオペレーティング システム**  
  
  
