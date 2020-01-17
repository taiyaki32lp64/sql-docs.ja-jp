---
title: SUSER_SID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a31be66b07c6d5c463f5220e6359942cd507849b
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981741"
---
# <a name="suser_sid-transact-sql"></a>SUSER_SID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定されたログイン名のセキュリティ ID 番号 (SID) を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
## <a name="arguments"></a>引数  
 **'** *login* **'**  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降
  
 ユーザーのログイン名を指定します。 *login* は **sysname** です。 *login* は省略可能で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインか、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザーまたはグループを指定できます。 *login* の指定を省略すると、現在のセキュリティ コンテキストについての情報が返されます。 パラメーターに "NULL" という語が含まれていると、NULL が返されます。  
  
 *Param2*  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降
  
 ログイン名を検証するかどうかを指定します。 *Param2* のデータ型は **int** で、省略可能です。 *Param2* が 0 の場合、ログイン名は検証されません。 *Param2* で 0 が指定されていない場合、Windows ログイン名と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に格納されたログイン名がまったく同じであるかどうかが確認されます。  
  
## <a name="return-types"></a>戻り値の型  
 **varbinary(85)**  
  
## <a name="remarks"></a>Remarks  
 SUSER_SID は、ALTER TABLE または CREATE TABLE の中で、DEFAULT 制約として使用できます。 SUSER_SID は、選択リストの中、WHERE 句の中、また、式を使える所ならどこにでも使用できます。 SUSER_SID の後には、パラメーターを指定しない場合も含め、常にかっこが必要です。  
  
 SUSER_SID を引数なしで呼び出すと、現在のセキュリティ コンテキストの SID が返されます。 EXECUTE AS を使用してコンテキストを切り替えたバッチ内で SUSER_SID を引数なしで呼び出すと、権限を借用したコンテキストの SID が返されます。 権限を借用したコンテキストから SUSER_SID(ORIGINAL_LOGIN()) を呼び出すと、元のコンテキストの SID が返されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序と Windows 照合順序が異なる場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と Windows ストアでログインを格納する形式が異なると、SUSER_SID は失敗することがあります。 たとえば、Windows コンピューター TestComputer のログインが User で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にはそのログインが TESTCOMPUTER\User として格納されている場合、ログイン TestComputer\User を参照したときにログイン名を正しく解決できないことがあります。 このログイン名の検証をスキップするには、*Param2* を使用します。 照合順序が異なると、多くの場合、次に示すような [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー 15401 が発生します。  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-suser_sid"></a>A. SUSER_SID を使用する  
 次の例では、現在のセキュリティ コンテキストのセキュリティ ID 番号 (SID) を返します。  
  
```  
SELECT SUSER_SID();  
```  
  
### <a name="b-using-suser_sid-with-a-specific-login"></a>B. SUSER_SID を特定のログインと共に使用する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] における `sa` というログインのセキュリティ ID 番号を返します。  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-suser_sid-with-a-windows-user-name"></a>C. SUSER_SID を Windows ユーザー名と共に使用する  
 次の例では、Windows ユーザーである `London\Workstation1` のセキュリティ ID 番号を返します。  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降
  
```  
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-suser_sid-as-a-default-constraint"></a>D. SUSER_SID を DEFAULT 制約として使用する  
 次の例では、`SUSER_SID` ステートメントで `DEFAULT` を `CREATE TABLE` 制約として使用しています。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   varbinary(85) DEFAULT SUSER_SID(),  
login_name  varchar(30) DEFAULT SYSTEM_USER,  
login_dept  varchar(10) DEFAULT 'SALES',  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>E. Windows ログイン名と SQL Server に格納されたログイン名を比較する  
 次の例は、*Param2* を使用して Windows から SID を取得する方法を示しています。この例では、その SID を `SUSER_SNAME` 関数への入力として使用しています。 Windows に格納された形式 (`TestComputer\User`) でログインを指定し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に格納された形式 (`TESTCOMPUTER\User`) のログインを取得しています。  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>参照  
 [ORIGINAL_LOGIN &#40;Transact-SQL&#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [binary と varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
