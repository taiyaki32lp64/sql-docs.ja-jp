---
title: sys.dm_clr_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 331969c2baa8ec67e0cd7c0ebf8cdd894878f397
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266061"
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の共通言語ランタイム (CLR) 統合に関係するプロパティごとに 1 行のデータを返します。このプロパティには、ホストされる CLR のバージョンや状態などが含まれます。 実行して、ホストされる CLR が初期化されて、 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)、 [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)、または[DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md)ステートメント、または任意の CLR ルーチン、型、またはトリガーを実行しています。 **Sys.dm_clr_properties**ビューは、サーバー上でユーザー CLR コードの実行が有効になっているかどうかを指定していません。 使用してユーザー CLR コードの実行が有効になっている、 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)ストアド プロシージャを[clr を有効になっている](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)オプションを 1 に設定します。  
  
 **Sys.dm_clr_properties**ビューが含まれています、**名前**と**値**列。 このビューの各行は、ホストされる CLR のプロパティに関する詳細を説明します。 このビューを使用して、ホストされる CLR に関する情報 (CLR のインストール ディレクトリ、CLR のバージョン、ホストされる CLR の現在の状態など) を収集します。 このビューでは、サーバー コンピューターにインストールされている CLR の問題のための CLR 統合コードが動作していないかどうかを判断できます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|プロパティの名前。|  
|**value**|**nvarchar(128)**|プロパティの値。|  
  
## <a name="properties"></a>Properties  
 **ディレクトリ**プロパティは、.NET Framework がインストールされているサーバー上のディレクトリを示します。 サーバー コンピューター上の .NET Framework の複数のインストールがあるし、このプロパティの値は、インストールを識別します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用しています。  
  
 **バージョン**プロパティは、.NET Framework のバージョンを示すし、サーバーで CLR をホストします。  
  
 **Sys.dm_clr_properties**動的マネージ ビューでの 6 つの異なる値を返すことができます、**状態**の状態を反映するには、プロパティ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR をホストします。 これらは次のとおりです。  
  
-   Mscoree is not loaded. (mscoree が読み込まれていない。)  
  
-   Mscoree is loaded. (mscoree が読み込まれている。)  
  
-   Mscoree で CLR のバージョンをロックします。  
  
-   CLR が初期化されます。  
  
-   CLR の初期化が完全に失敗しました。  
  
-   CLR が停止しました。  
  
 **Mscoree が読み込まれていない**と**Mscoree が読み込まれる**状態、サーバー起動時における、ホストされる CLR の初期化の進行状況を表示および確認することはありません。  
  
 **Mscoree で Locked CLR version**状態が表示され、ホストされる CLR が使用されていないと、そのため、これがまだ初期化されていません。 ホストされる CLR が初期化される DDL ステートメントを初めて (など[CREATE ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) またはマネージ データベース オブジェクトが実行されます。  
  
 **CLR が初期化される**状態では、ホストされる CLR が正常に初期化されたことを示します。 ユーザー CLR コードの実行が有効になっているかどうかは見られませんことに注意してください。 有効になっており、しを使用して無効になっている場合はユーザー CLR コードの実行は最初、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)ストアド プロシージャは、状態値がありますが**CLR が初期化される**します。  
  
 **CLR の初期化が完全に失敗した**状態では、CLR をホストしていることを示します初期化に失敗しました。 これは多くの場合メモリ不足が原因ですが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と CLR の間でホスティングのハンドシェイクが失敗していることも考えられます。 このようなケースでは、エラー メッセージ 6512 または 6513 がスローされます。  
  
 **CLR が停止状態**にのみ返さ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]シャット ダウン処理中です。  
  
## <a name="remarks"></a>コメント  
 プロパティと値のこのビューは、将来のバージョンで変更可能性があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR 統合機能の強化のためです。  
  
## <a name="permissions"></a>アクセス許可  
  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="examples"></a>使用例  
 次の例では、ホストされる CLR に関する情報を取得します。  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [共通言語ランタイム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
