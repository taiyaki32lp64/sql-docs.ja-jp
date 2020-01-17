---
title: サーバーの構成 - 照合順序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 521129056d4513af2f86fb7b70b26621cb881b80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092289"
---
# <a name="server-configuration---collation"></a>サーバーの構成 - 照合順序
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの [サーバーの構成 - 照合順序] ページでは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で並べ替えに使用される照合順序の設定を変更できます。 インストールされている別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、または別のコンピューターと照合順序設定を一致させるにはこのオプションを選択します。  
  
## <a name="options"></a>および  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のカスタマイズ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の 2 つのグループを提供します。Windows 照合順序と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]照合順序。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に異なる照合順序の設定を指定できます。また、両方に同じ照合順序を指定することもできます。  
  
 既定では、英語 (米国) システム ロケールには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序が選択されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の他言語バージョンの既定の照合順序は、使用しているコンピューターの Windows システム ロケール設定によって決まります。  
  
 既定の設定は、このインストール済み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序の設定を別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスで使用される照合順序の設定に一致させる必要がある場合、または別のコンピューターの Windows システム ロケールに一致させる必要がある場合にのみ、変更するようにします。  
  
 **注:** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は Windows 照合順序のみを使用します。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインストールを予定する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のセットアップ時に Windows 照合順序を選択して、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] と [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]で一貫した結果が得られるようにしてください。  
  
 詳細については、「 [セットアップでの照合順序の設定](https://go.microsoft.com/fwlink/?LinkId=190977)」を参照してください。  
  
## <a name="best-practices"></a>ベスト プラクティス  
 Windows システム ロケールと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップで使用される既定の照合順序との対応表については、「 [セットアップでの照合順序の設定](https://go.microsoft.com/fwlink/?LinkId=190977)」を参照してください。  
  
 可能であれば、組織で単一の照合順序を使用してください。 そうすれば、データベース、列、式、または識別子ごとに照合順序を明示的に指定する必要はなくなります。 複数の照合順序とコード ページ設定を操作する必要がある場合は、照合順序の優先順位の規則を考慮してクエリを作成します。 詳細については、オンライン ブックの「[照合順序の優先順位 &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序を選択する場合は、次の推奨設定を考慮してください。  
  
-   バイナリ コード ポイント順が使用できる場合は、バイナリ 2 照合順序を選択します。  
  
-   データ型間の比較で一貫性を保つには、Windows 照合順序を選択します。  
  
-   言語の並べ替えのサポートを向上させるには、新しい 100 レベルの照合順序を使用します。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
-   アップグレード済みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスにデータベースを移行する場合は、データベースの既存の照合順序と一致する照合順序を選択します。  
  
  
