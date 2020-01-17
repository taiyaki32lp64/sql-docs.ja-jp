---
title: Sybase ASE スキーマの SQL Server スキーマ (SybaseToSQL) へのマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5c39e81f8faffed606e6ca94315c47d383174c91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028872"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Sybase ASE スキーマの SQL Server スキーマへのマッピング (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE)、各データベースは、1 つまたは複数のスキーマを持っています。 既定では、SSMA は、同じデータベースおよびスキーマ内にデータベースおよびスキーマ内のすべてのオブジェクトを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 ただし、ASE の間のマッピングをカスタマイズすることができますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベースとスキーマです。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE と SQL Server または SQL Azure のスキーマ  
ASE と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure として 2 つのパーツ表記を使用してデータベースとそのスキーマを指定または*database.schema*します。 たとえば、ASE で**デモ**データベースである可能性があります、 **dbo**スキーマ。 データベースとスキーマのペアとして指定されている**demo.dbo**します。 場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure では、同じデータベースとスキーマを持っているペアも指定されてとして**demo.dbo**します。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲット データベースおよびスキーマの変更  
SSMA では、使用可能な任意に、ASE スキーマをマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のスキーマ。  
  
**データベースとスキーマを変更するには**  
  
1.  Sybase メタデータ エクスプ ローラーで選択**データベース**します。  
  
    **スキーマ マッピング** タブは、個々 のデータベースを選択した場合にも使用可能な**スキーマ**フォルダー、または個別のスキーマ。 一覧で、**スキーマ マッピング** タブを選択したオブジェクトのカスタマイズします。  
  
2.  右側のウィンドウでをクリックして、**スキーマ マッピング**タブ。  
  
    対象の値を続けて、そのスキーマを持つすべての ASE データベースの一覧が表示されます。 このターゲットは、2 部構成の表記法で示されます (*database.schema*) で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure が、オブジェクトとデータを移行します。  
  
3.  変更、およびクリックするマッピングが含まれている行を選択**変更**します。  
  
4.  **ターゲット スキーマの選択**ダイアログ ボックスで、使用可能なターゲット データベース スキーマや型、データベースとスキーマの 2 部構成の表記 (database.schema) で、テキスト ボックスに名前をクリックを参照することがあります**OK**.  
  
5.  ターゲットの変更、**スキーマ マッピング**タブ。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソース データベースは、任意のターゲット データベースにマップできます。 既定では、ソース データベースがマップされているターゲットに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA を使用してを接続したデータベース。 マップされるターゲット データベースでは、非既存ではかどうか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、メッセージが表示されますが、 **"、データベースやスキーマがターゲットに存在しません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ。これが同期中に作成されます。続行することでしょうか。"** [はい] をクリックします。 同様に、ターゲットの存在しないスキーマをスキーマにマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同期中に作成されるデータベース。  
  
-   SQL Azure へのマッピング  
  
ソース データベースに接続されているターゲットの SQL Azure データベース、または接続されているターゲットの SQL Azure データベース内の任意のスキーマをマップできます。 ソース スキーマ 接続されているターゲット データベースでは、存在しないスキーマをマップするかどうかは、メッセージが表示されるが **"スキーマが対象のメタデータには存在できません。これが同期中に作成されます。続行しますか?"** はい をクリックします。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>既定のデータベースとスキーマを元に戻す  
ASE、スキーマ間のマッピングをカスタマイズする場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のスキーマ マッピングを既定値を戻すことができます。  
  
**既定のデータベースとスキーマに戻すには**  
  
1.  スキーマ マッピング タブで、任意の行を選択し をクリックして**既定値にリセット**既定のデータベースとスキーマに戻す。  
  
## <a name="next-steps"></a>次の手順  
Sybase ASE オブジェクトへの変換を分析する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクトを実行できます[変換レポートを作成](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)します。 それ以外の場合できます[ASE データベース オブジェクトの定義の変換](converting-sybase-ase-database-objects-sybasetosql.md)に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクトの定義。  
  
## <a name="see-also"></a>関連項目  
[SQL Server - Azure SQL DB への Sybase ASE データベース移行&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
