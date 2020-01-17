---
title: SQL Server のプロパティ ([起動時のパラメーター] タブ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 16942624-5374-446c-8de4-ee6ed34d6e94
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ab3d9e9e4178b1ee2e10e5be63f0ea9252fd4a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62679166"
---
# <a name="sql-server-properties-startup-parameters-tab"></a>[SQL Server のプロパティ] ダイアログ ボックス ([起動時のパラメーター] タブ)
  このダイアログ ボックスを使用すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の起動時のパラメーターを追加または削除できます。 起動時のパラメーターは [!INCLUDE[ssDE](../../includes/ssde-md.md)] のパフォーマンスに大きな影響を及ぼします。 起動時のパラメーターを追加または変更する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのスタートアップ オプションの使用」を参照してください。  
  
## <a name="options"></a>および  
 **[起動時のパラメーターの指定]**  
 パラメーターを追加するには、パラメーターを入力し、 **[追加]** をクリックします。  
  
 必要なパラメーターのいずれかを変更するには、 **[既存のパラメーター]** ボックスのパラメーターを選択し、 **[起動時のパラメーターの指定]** ボックスの値を変更して、 **[更新]** をクリックします。  
  
 **[既存のパラメーター]**  
 パラメーターを削除するには、パラメーターを選択し、 **[削除]** をクリックします。  
  
## <a name="parameter-format"></a>パラメーターの形式  
 パラメーターの間に区切り記号を入力しないでください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーによって自動的に区切り記号が追加されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーによって、次のパラメーターの要件が適用されます。  
  
-   先頭および末尾のスペースは、すべての起動時のパラメーターから削除します。  
  
-   すべての起動時のパラメーターの先頭文字は - (ダッシュ) で、2 番目の値は文字です。  
  
## <a name="required-parameters"></a>必要なパラメーター  
 以下のパラメーターが必要です。 これらは変更できますが、削除できません。  
  
-   -d は、 **master.mdf** ファイル (master データベースのデータ ファイル) のパスです。  
  
-   -l は、 **master.ldf** ファイル (master データベースのログ ファイル) のパスです。  
  
-   -e は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログ ファイルのパスです。  
  
> [!CAUTION]  
>  ファイル パス パラメーターが正しくない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は起動しません。  
  
 master データベースを移動する方法の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「システム データベースの移動」を参照してください。  
  
## <a name="optional-parameters"></a>省略可能なパラメーター  
 サポートされている、すべての起動時のパラメーターについては、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのスタートアップ オプションの使用」で説明されています。 起動時のパラメーターの -T*trace#* は、指定された有効なトレース フラグ ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trace# *) を使用して*のインスタンスを起動することを指定します。 トレース フラグを使用してサーバーが起動すると、標準的な動作とは異なります。 トレース フラグの詳細については、[!INCLUDE[tsql](../../includes/tsql-md.md)]オンライン ブックの「トレース フラグ ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )」を参照してください。  
  
> [!CAUTION]  
>  ドキュメントに未記載の起動時のパラメーターとトレース フラグについては、インターネット上で追加の説明を読むことができます。 ドキュメントに未記載の起動時のパラメーターとトレース フラグは、一般的ではない問題の解決またはテストに必要な特定の条件の適用のために作成されます。 ドキュメントに未記載の起動時のパラメーターを使用すると、予期しない結果になる場合があります。 マイクロソフト カスタマー サポート サービスから指示されない限り、ドキュメントに未記載のパラメーターを使用しないでください。  
  
 以下に、一般的な省略可能なパラメーターを示します。  
  
|パラメーター|簡単な説明|  
|---------------|-----------------------|  
|-M|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスをシングル ユーザー モードで起動します。|  
|-T1204|デッドロックに関係しているロックのリソースと種類、および影響を受けている現在のコマンドを返します。|  
|-T1224|ロック数に基づいてロックのエスカレーションを無効にします。|  
|-T3608|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、master データベース以外のすべてのデータベースを自動的に開始および復旧しないようにします。|  
|-T7806|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]で専用管理者接続 (DAC) を有効にします。|  
  
> [!CAUTION]  
>  省略可能なパラメーターの中には、サーバーの動作を変更し、パフォーマンスに影響を与えるものもあります。  
  
## <a name="permissions"></a>Permissions  
 このページは、レジストリの関連エントリを変更できるユーザーのみが使用できます。 該当するユーザーは次のとおりです。  
  
-   ローカル管理者グループのメンバー。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって使用されるドメイン アカウント ( [!INCLUDE[ssDE](../../includes/ssde-md.md)] がドメイン アカウントで実行されるように構成されている場合)。  
  
## <a name="books-online-references"></a>オンライン ブックの参照  
 詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]起動時のパラメーターを参照してください"する方法。サーバーのスタートアップ オプションの構成 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager)"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
  
