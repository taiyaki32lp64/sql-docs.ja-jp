---
title: SET FIPS_FLAGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FIPS_FLAGGER
- SET_FIPS_FLAGGER_TSQL
- FIPS_FLAGGER_TSQL
- SET FIPS_FLAGGER
dev_langs:
- TSQL
helpviewer_keywords:
- SET FIPS_FLAGGER statement
- FIPS 127-2 standard
- FIPS_FLAGGER option
ms.assetid: e82f6bee-6cf6-4061-be22-9ad2e8e9d3d6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f666a327db29468c5bbd91bf7106d7c6e4f61f64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929047"
---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  FIPS 127-2 標準に準拠しているかどうかをチェックします。 これは ISO 標準を基準にしています。 SQL Server の FIPS 準拠については、「[FIPS 140-2 準拠モードで SQL Server の 2016 を使用する方法](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode)」をご覧ください。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>引数  
 **'** *level* **'**  
 FIPS 127-2 標準に対してすべてのデータベース操作の準拠性をチェックするレベルを指定します。 データベース操作が、選択した ISO 標準のレベルと競合する場合、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では警告が生成されます。  
  
 *level* の値には次のいずれかを指定します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|ENTRY|ISO エントリレベルの準拠性の標準チェック。|  
|FULL|ISO 完全準拠性の標準チェック|  
|INTERMEDIATE|ISO 中間レベルの準拠性の標準チェック。|  
|OFF|標準チェックなし。|  
  
## <a name="remarks"></a>Remarks  
 `SET FIPS_FLAGGER` は、実行時ではなく解析時に設定されます。 解析時に設定されるということは、SET ステートメントがバッチまたはストアド プロシージャ内に指定されている場合は、コードが実際にその場所まで実行されるかどうかに関係なく、設定が有効になることを意味します。つまり他のどのステートメントが実行されるよりも前に、`SET` ステートメントは有効になります。 たとえば、絶対に実行されることのない `IF...ELSE` ステートメント ブロックに `SET` ステートメントが指定されていたとしても、`IF...ELSE` ステートメント ブロックは解析されるので、`SET` ステートメントは有効になります。  
  
 `SET FIPS_FLAGGER` がストアド プロシージャで設定された場合、`SET FIPS_FLAGGER` の値は、制御がストアド プロシージャから返された後、元に戻されます。 したがって、動的 SQL に指定されている `SET FIPS_FLAGGER` ステートメントは、動的 SQL ステートメントの後にあるステートメントにまったく影響しません。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
