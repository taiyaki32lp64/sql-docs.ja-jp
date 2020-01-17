---
title: SQL Server スキーマ (DB2ToSQL) への DB2 スキーマのマッピング |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 50845a9bdf3c3185d7b69bb86a75b2a3d332ef6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074174"
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>SQL Server スキーマ (DB2ToSQL) への DB2 スキーマのマッピング
DB2 の場合に、各データベースは、1 つまたは複数のスキーマを持っています。 SSMA は既定では、DB2 スキーマのすべてのオブジェクトを移行、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマという名前のデータベース。 ただし、DB2 スキーマの間のマッピングをカスタマイズすることができますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 と SQL Server スキーマ  
DB2 データベースには、スキーマが含まれています。 インスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]複数のスキーマがそれぞれの複数のデータベースが含まれています。  
  
マップ、スキーマの DB2 の概念、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースとそのスキーマのいずれかの概念です。 たとえば、DB2 のという名前のスキーマがある**HR**します。 インスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]という名前のデータベースがあります。 **HR**、そのデータベースは、スキーマとします。 1 つのスキーマは、 **dbo** (またはデータベース所有者) スキーマ。 既定では、DB2 スキーマ**HR**にマップされます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースおよびスキーマ**HR.dbo**します。 SSMA を指す、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマとしてデータベースとスキーマの組み合わせ。  
  
DB2 の間のマッピングを変更して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマ。  
  
## <a name="modifying-the-target-database-and-schema"></a>ターゲット データベースおよびスキーマの変更  
SSMA では、使用可能な任意に、DB2 スキーマをマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマ。  
  
**データベースとスキーマを変更するには**  
  
1.  DB2 メタデータ エクスプ ローラーで選択**スキーマ**します。  
  
    **スキーマ マッピング** タブは、個々 のデータベースを選択した場合にも使用可能な**スキーマ**フォルダー、または個別のスキーマ。 一覧で、**スキーマ マッピング** タブを選択したオブジェクトのカスタマイズします。  
  
2.  右側のウィンドウでをクリックして、**スキーマ マッピング**タブ。  
  
    対象の値を後に、すべての DB2 スキーマの一覧が表示されます。 このターゲットは、2 部構成の表記法で示されます (*database.schema*) で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトとデータを移行します。  
  
3.  変更、およびクリックするマッピングが含まれている行を選択**変更**します。  
  
    **ターゲット スキーマの選択**ダイアログ ボックスで、使用可能なターゲット データベース スキーマや型、データベースとスキーマの 2 部構成の表記 (database.schema) で、テキスト ボックスに名前をクリックを参照することがあります**OK**.  
  
4.  ターゲットの変更、**スキーマ マッピング**タブ。  
  
**マッピングのモード**  
  
-   SQL Server へのマッピング  
  
ソース データベースは、任意のターゲット データベースにマップできます。 既定では、ソース データベースがマップされているターゲットに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SSMA を使用してを接続したデータベース。 マップされるターゲット データベースでは、非既存ではかどうか[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、メッセージが表示されますが、 **"、データベースやスキーマがターゲットに存在しません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ。これが同期中に作成されます。続行することでしょうか。"** [はい] をクリックします。 同様に、ターゲットの存在しないスキーマをスキーマにマップできます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同期中に作成されるデータベース。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>既定のデータベースとスキーマを元に戻す  
DB2 スキーマの間のマッピングをカスタマイズする場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]スキーマでは、既定値にマッピングを戻すことができます。  
  
**既定のデータベースとスキーマに戻すには**  
  
1.  スキーマ マッピング タブで、任意の行を選択し をクリックして**既定値にリセット**既定のデータベースとスキーマに戻す。  
  
## <a name="next-steps"></a>次の手順  
DB2 オブジェクトへの変換を分析する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトを実行できます[データ移行レポート (SSMA 一般的)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)します。  
  
## <a name="see-also"></a>関連項目  
[SQL Server に接続する&#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[SQL Server にデータベースを移行する DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
