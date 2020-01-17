---
title: データベース エンジン PowerShell リファレンス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ed2e407b724f57d6ded518b864e3b1d78b4c489e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064966"
---
# <a name="database-engine-powershell-reference"></a>データベース エンジン PowerShell リファレンス
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、[!INCLUDE[ssDE](../includes/ssde-md.md)]で一般的な操作を実行するための一連の Windows PowerShell 2.0 コマンドレットが含まれています。 また、クエリ式と URN (Uniform Resource Name) は、SQL Server PowerShell パスに変換したり、 [!INCLUDE[ssDE](../includes/ssde-md.md)]で 1 つ以上のオブジェクトを指定するために使用したりできます。  
  
## <a name="database-engine-cmdlets"></a>データベース エンジンのコマンドレット  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] に含まれている [!INCLUDE[ssDE](../includes/ssde-md.md)]用のコマンドレットは比較的少ないです。 [!INCLUDE[ssDE](../includes/ssde-md.md)] を操作する PowerShell スクリプトの多くは、SQL Server PowerShell プロバイダーおよび管理オブジェクト モデルを使用します。 詳細については、「 [SQL Server PowerShell プロバイダー](../powershell/sql-server-powershell-provider.md)」を参照してください。  
  
 Windows PowerShell 環境で SQL Server コマンドレットに関するヘルプを参照する方法については、「 [SQL Server PowerShell のヘルプの参照](../powershell/sql-server-powershell.md)」を参照してください。  
  
### <a name="in-this-section"></a>このセクションの内容  
 ここでは、これらのコマンドレットについて説明します。  
  
|説明|コマンドレット|  
|-----------------|------------|  
|`sqlcmd` ユーティリティを使用して実行できるスクリプトなど、Transact-SQL スクリプトと XQuery スクリプトを実行します。|[Invoke-Sqlcmd コマンドレット](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|データベース エンジン オブジェクトがポリシー ベースの管理ポリシーに準拠しているかどうかを評価します。|[Invoke-PolicyEvaluation コマンドレット](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>その他のコマンドレットに関する情報  
 `Encode-Sqlname` コマンドレットと `Decode-Sqlname` コマンドレットでは、PowerShell パスではサポートされていない文字を含んだ SQL Server 識別子を指定できます。 詳細については、「 [PowerShell での SQL Server 識別子](../powershell/sql-server-identifiers-in-powershell.md)」を参照してください。  
  
 `Convert-UrnToPath` コマンドレットを使用して、[!INCLUDE[ssDE](../includes/ssde-md.md)] オブジェクトの Unique Resource Name を SQL Server PowerShell プロバイダーのパスに変換します。 詳細については、「 [URN から SQL Server プロバイダー パスへの変換](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md)」を参照してください。  
  
## <a name="query-expressions-and-unique-resource-names"></a>クエリ式および Unique Resource Name  
 クエリ式は、オブジェクト モデル階層内の 1 つまたは複数のオブジェクトを列挙する条件のセットを指定するために XPath と同様の構文を使用する文字列です。 URN (Unique Resource Name) は、単一のオブジェクトを一意に識別する特定の種類のクエリ式文字列です。 詳細については、「 [クエリ式と Uniform Resource Name](../powershell/query-expressions-and-uniform-resource-names.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
