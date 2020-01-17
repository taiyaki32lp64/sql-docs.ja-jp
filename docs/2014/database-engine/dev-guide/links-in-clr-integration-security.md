---
title: CLR 統合のセキュリティへのリンク |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-access links [CLR integration]
- security [CLR integration]
- invocation links [CLR integration]
- gated links [CLR integration]
ms.assetid: 168efd01-d12e-4bdf-a1b3-0b5c76474eaf
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37aa64129658128bd7297f147f317166917e05a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781071"
---
# <a name="links-in-clr-integration-security"></a>CLR 統合のセキュリティのリンク
  ここでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはいずれかのマネージド言語で、[!INCLUDE[tsql](../../includes/tsql-md.md)] 内のユーザー コードが相互に呼び出すしくみを説明します。 このようなオブジェクト間のリレーションシップをリンクと呼びます。  
  
## <a name="invocation-links"></a>呼び出しリンク  
 呼び出しリンクは、オブジェクトを呼び出すユーザーからのコード呼び出し (ストアド プロシージャを呼び出す [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチなど)、または共通言語ランタイム (CLR) ストアド プロシージャや関数からのコード呼び出しのいずれかに対応しています。 呼び出しリンクにより、呼び出し先の `EXECUTE` 権限がチェックされます。  
  
## <a name="table-access-links"></a>テーブル アクセス リンク  
 テーブル アクセス リンクは、テーブル、ビュー、またはテーブル値関数の値の取得や変更に対応します。 テーブル アクセス リンクは、SELECT 権限、INSERT 権限、UPDATE 権限、および DELETE 権限に関してアクセス制御の粒度が細かいという点を除いて、呼び出しリンクと同じです。  
  
## <a name="gated-links"></a>ゲート リンク  
 ゲート リンクは、一度確立されると、実行されている間、オブジェクトのリレーションシップ間で権限がチェックされることはありません。 2 つのオブジェクトの間にゲート リンクがある場合 (たとえば、オブジェクト**x**とオブジェクト**y**)、オブジェクトに対するアクセス許可**y** オブジェクトからアクセスされるその他のオブジェクトと**y**オブジェクトの作成時にのみチェック**x**します。 オブジェクトの作成時に**x**、`REFERENCE`権限がチェックされます**y**の所有者に対して**x**します。 実行時に、(たとえば、オブジェクトを呼び出すユーザー **x**)、に対する権限チェックがない**y**または静的に参照するその他のオブジェクト。 オブジェクトに対して、実行時に適切な権限がチェックされます**x**自体。  
  
 ゲート リンクは、2 つのオブジェクト間のメタデータの依存関係と常に組み合わせて使用されます。 このメタデータの依存関係とは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カタログで確立されるリレーションシップです。このリレーションシップにより、別のオブジェクトが依存しているオブジェクトの削除が回避されます。  
  
 ゲート リンクは、多くの依存オブジェクトに権限を許可することが不適切または管理不可能である場合に役立ちます。 CLR アセンブリ (CLR プロシージャ、トリガー、関数、型、集計など) への [!INCLUDE[tsql](../../includes/tsql-md.md)] エントリ ポイントを定義するオブジェクトと、それらを定義する際のベースになるアセンブリとの間にゲート リンクが導入されています。 このようなオブジェクトに対してゲート セキュリティを使用するということは、CLR アセンブリ内で定義された [!INCLUDE[tsql](../../includes/tsql-md.md)] エントリ ポイントを呼び出すために呼び出し元で必要になるのは、その [!INCLUDE[tsql](../../includes/tsql-md.md)] エントリ ポイントに対する適切な権限のみであることを意味します。 呼び出し元には、そのアセンブリまたはそのアセンブリが静的に参照するその他のアセンブリに対する権限は不要です。 アセンブリに対する権限は、[!INCLUDE[tsql](../../includes/tsql-md.md)] エントリ ポイントの作成時にチェックされます。  
  
## <a name="sql-server-authorization-based-security"></a>SQL Server 承認ベースのセキュリティ  
 CLR ベースのデータベース オブジェクトの呼び出しと、これらのオブジェクト間で実行される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ チェックを支える基本的な規則を次に示します。最初の 3 つの規則では、どの権限がどのオブジェクトに対してチェックされるかを定義し、4 つ目の規則では、権限がチェックされる対象の実行コンテキストを定義します。  
  
1.  呼び出しが同じオブジェクト内で発生する場合を除いて、すべての呼び出しに `EXECUTE` 権限が必要になります。つまり、同じアセンブリ内での呼び出しには権限チェックは必要ありません。 権限は実行時にチェックされます。  
  
2.  ゲート リンクでは、呼び出し元オブジェクトの作成時に、呼び出し先に対する `REFERENCE` 権限が必要になります。 呼び出し元オブジェクトの作成時に、そのオブジェクトの所有者の権限がチェックされます。  
  
3.  テーブル アクセス リンクでは、アクセス先のテーブルまたはビューに対する `SELECT` 権限、`INSERT` 権限、`UPDATE` 権限、または `DELETE` 権限が必要になります。  
  
4.  現在の実行コンテキストに対して権限がチェックされます。 呼び出し元とは異なる実行コンテキストでプロシージャや関数を作成できます。 アセンブリは、常に、プロシージャ、関数、またはトリガーに対して定義されている実行コンテキストで作成されます。  
  
## <a name="see-also"></a>関連項目  
 [CLR 統合のセキュリティ](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
