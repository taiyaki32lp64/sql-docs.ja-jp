---
title: CREATE TRIGGER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: mathoma
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE TRIGGER
- TRIGGER
- CREATE_TRIGGER_TSQL
- TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- CREATE TRIGGER statement
- multiple triggers
- deferred name resolution, DML triggers
- DML triggers, creating
- nested triggers
- server-scoped triggers
- DDL triggers, creating
- triggers [SQL Server], creating
- database-scoped triggers [SQL Server]
ms.assetid: edeced03-decd-44c3-8c74-2c02f801d3e7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7735298fc669d8e5b385501cd3f235a0a08abb9d
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982699"
---
# <a name="create-trigger-transact-sql"></a>CREATE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]


DML トリガー、DDL トリガー、またはログオン トリガーを作成します。 トリガーとは、特別な種類のストアド プロシージャであり、データベース サーバーでイベントが発生したときに自動的に実行されます。 DML トリガーは、ユーザーがデータ操作言語 (DML) イベントを介してデータを変更しようとしたときに実行されます。 DML イベントは、テーブルやビューに対する INSERT、UPDATE、または DELETE ステートメントによって発生するイベントです。 これらのトリガーは、テーブル行が影響を受けるかどうかにかかわらず、有効なイベントが発生したときに起動されます。 詳しくは、「 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)」をご覧ください。  
  
DDL トリガーは、さまざまなデータ定義言語 (DDL) イベントに対応して起動されます。 本来、これらのイベントは、[!INCLUDE[tsql](../../includes/tsql-md.md)] の CREATE、ALTER、DROP ステートメント、および DDL に類似した処理を実行するシステム ストアド プロシージャに対応するものです。 

ログオン トリガーは、ユーザーのセッションの確立時に発生する LOGON イベントに応答して起動されます。 トリガーは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントから直接作成することも、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイム (CLR) 内に作成したアセンブリのメソッドから作成し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアップロードすることもできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、特定のステートメントに対して複数のトリガーを作成できます。  
  
> [!IMPORTANT]  
>  上位の特権の下では、トリガー内の悪意のあるコードを実行できます。 この脅威を緩和する方法について詳しくは、「[トリガーのセキュリティの管理](../../relational-databases/triggers/manage-trigger-security.md)」をご覧ください。  
  
> [!NOTE]  
>  この記事では、SQL Server への .NET Framework CLR の統合について説明します。 CLR 統合は、Azure SQL Database には適用されません。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
``` 
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
[ WITH APPEND ]  
[ NOT FOR REPLICATION ]   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME <method specifier [ ; ] > }  
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
```  
  
``` 
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a 
-- table (DML Trigger on memory-optimized tables)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
AS { sql_statement  [ ; ] [ ,...n ] }  
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ EXECUTE AS Clause ]  
  
```  
  
``` 
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE or UPDATE statement (DDL Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { ALL SERVER | DATABASE }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type | event_group } [ ,...n ]  
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Trigger on a LOGON event (Logon Trigger)  
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON    
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
```  
  
## <a name="syntax"></a>構文  
  
``` 
-- Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
  AS { sql_statement  [ ; ] [ ,...n ] [ ; ] > }  
  
<dml_trigger_option> ::=   
        [ EXECUTE AS Clause ]  
  
```  
  
```  
-- Azure SQL Database Syntax  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, 
-- REVOKE, or UPDATE STATISTICS statement (DDL Trigger)   
  
CREATE [ OR ALTER ] TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type | event_group } [ ,...n ]   
AS { sql_statement  [ ; ] [ ,...n ]  [ ; ] }  
  
<ddl_trigger_option> ::=   
    [ EXECUTE AS Clause ]  
```  
  
## <a name="arguments"></a>引数
OR ALTER  
**適用対象**:Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 以降)。 
  
トリガーが既に存在する場合にのみ、条件付きでビューを変更します。 
  
*schema_name*  
DML トリガーが属しているスキーマの名前。 DML トリガーのスコープは、そのトリガーが作成されたテーブルまたはビューのスキーマです。 *schema_name* は DDL トリガーやログオン トリガーでは指定できません。  
  
*trigger_name*  
トリガーの名前。 *trigger_name* は、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従う必要があります。ただし、*trigger_name* の先頭に # または ## を指定することはできません。  
  
*table* | *view*  
DML トリガーが実行されるテーブルまたはビュー。 このテーブルまたはビューは、トリガー テーブルまたはトリガー ビューと呼ばれることがあります。 テーブルまたはビューの完全修飾名の指定は省略可能です。 ビューは、INSTEAD OF トリガーによってのみ参照できます。 DML トリガーは、ローカルまたはグローバルの一時テーブルに対しては定義できません。  
  
DATABASE  
DDL トリガーのスコープを現在のデータベースに適用します。 これを指定すると、現在のデータベースで *event_type* または *event_group* が発生するたびにトリガーが起動します。  
  
ALL SERVER  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
DDL トリガーまたはログオン トリガーのスコープを現在のサーバーに適用します。 これを指定すると、現在のサーバーの任意の場所で *event_type* または *event_group* が発生するたびにトリガーが起動します。  
  
WITH ENCRYPTION  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
CREATE TRIGGER ステートメントのテキストをわかりにくくします。 WITH ENCRYPTION を使用すると、そのトリガーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーションの一部としてパブリッシュできなくなります。 WITH ENCRYPTION は、CLR トリガーに対しては指定できません。  
  
EXECUTE AS  
トリガーを実行するセキュリティ コンテキストを指定します。 これにより、トリガーが参照するデータベース オブジェクトの権限を検証するときに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが使用するユーザー アカウントを制御できます。  
  
このオプションは、メモリ最適化テーブルのトリガーに必要です。  
  
詳細については、「[EXECUTE AS 句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)」を参照してください。  
  
NATIVE_COMPILATION  
トリガーをネイティブでコンパイルすることを示します。  
  
このオプションは、メモリ最適化テーブルのトリガーに必要です。  
  
SCHEMABINDING  
トリガーによって参照されているテーブルを削除または変更できないようにします。  
  
このオプションは、メモリ最適化テーブルのトリガーで必要であり、従来のテーブルのトリガーではサポートされていません。  
  
FOR | AFTER  
FOR または AFTER を指定した場合は、トリガー元の SQL ステートメントで指定したすべての操作が正常に開始された場合のみ、DML トリガーが起動されます。 このトリガーの実行前に、すべての連鎖参照操作と制約チェックも成功している必要があります。  
  
ビューに AFTER トリガーを定義することはできません。  
  
INSTEAD OF  
トリガーをアクティブにする SQL ステートメントの "*代わりに*" DML トリガーを起動するように指定します。したがって、トリガーをアクティブにするステートメントの操作は無効になります。 DDL トリガーまたはログオン トリガーに INSTEAD OF を指定することはできません。  
  
テーブルまたはビューに対する INSERT、UPDATE、または DELETE の各ステートメントに、INSTEAD OF トリガーを 1 つだけ定義できます。 ビューにビューを定義して、各ビューに独自の INSTEAD OF トリガーを定義することもできます。  
  
INSTEAD OF トリガーは、WITH CHECK OPTION を使用する更新可能なビューには定義できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] これを行うと、WITH CHECK OPTION が指定されている更新可能なビューに INSTEAD OF トリガーを追加した場合にエラーが発生します。 INSTEAD OF トリガーを定義する前に、ALTER VIEW を使用してそのオプションを削除する必要があります。  
  
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }  
テーブルまたはビューに対して試行されたときに、DML トリガーをアクティブにするデータ変更ステートメントを指定します。 少なくとも 1 つのオプションを指定します。 これらのオプションを任意の順序で組み合わせて、トリガー定義内で使用できます。  
  
INSTEAD OF トリガーでは、ON DELETE 連鎖操作を指定する参照関係があるテーブルで、DELETE オプションを使用することはできません。 同様に、ON UPDATE 連鎖操作を指定する参照関係があるテーブルで、UPDATE オプションを使用することはできません。  
  
WITH APPEND  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
既存のトリガーに対して、新しいトリガーを追加します。 WITH APPEND は、INSTEAD OF トリガーと共に使用することはできず、AFTER トリガーが明示的に指定されている場合も使用できません。 旧バージョンとの互換性を保つために、WITH APPEND は、INSTEAD OF または AFTER の指定がなく、FOR が指定されている場合のみ使用してください。 EXTERNAL NAME を使用している場合 (つまり、トリガーが CLR トリガーの場合)、WITH APPEND は指定できません。  
  
*event_type*  
発生後に DDL トリガーが起動される [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語イベントの名前。 DDL トリガーで使用できるイベントの一覧については、「[DDL イベント](../../relational-databases/triggers/ddl-events.md)」を参照してください。  
  
*event_group*  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 言語イベントの定義済みグループの名前。 DDL トリガーは、*event_group* に属する [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語イベントの発生後に起動します。 DDL トリガーで使用できるイベント グループの一覧については、「[DDL イベント グループ](../../relational-databases/triggers/ddl-event-groups.md)」を参照してください。  
  
*event_group* は、対応するイベントの種類を sys.trigger_events カタログ ビューに追加した場合、CREATE TRIGGER が終了した後でマクロとしても動作します。  
  
NOT FOR REPLICATION  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
トリガーに関係するテーブルがレプリケーション エージェントによって変更される場合は、トリガーを実行しないことを示します。  
  
*sql_statement*  
トリガー条件とトリガー動作。 トリガー条件には、試行された DML イベント、DDL イベント、またはログオン イベントによってトリガー動作が実行されるかどうかを判定するための補足の条件を指定します。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで指定されたトリガー動作は、操作が試行されると有効になります。  
  
トリガーには、いくつかの例外を除き、任意の数と種類の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを含めることができます。 詳細については、「解説」を参照してください。 トリガーは、データ変更またはデータ定義ステートメントに基づいてデータをチェックまたは変更するものであり、ユーザーに値は返されません。 トリガー内の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントには、[フロー制御言語](~/t-sql/language-elements/control-of-flow.md)が主に使用されます。  
  
DML トリガーでは、deleted および inserted 論理 (概念) テーブルが使用されます。 それらは、トリガーが定義されるテーブル、つまり、ユーザー操作の対象となるテーブルと構造的に類似しています。 deleted および inserted テーブルには、ユーザー操作によって変更される行の古い値または新しい値が格納されます。 たとえば、`deleted` テーブルのすべての値を取得するには、次のように指定します。  
  
```sql  
SELECT * FROM deleted;  
```  
  
詳しくは、「[inserted テーブルと deleted テーブルの使用](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)」をご覧ください。  
  
DDL トリガーおよびログオン トリガーでは、[EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md) 関数を使用して、トリガー起動イベントに関する情報を取得できます。 詳しくは、「[EVENTDATA 関数の使用](../../relational-databases/triggers/use-the-eventdata-function.md)」をご覧ください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、テーブルまたはビューに対する INSTEAD OF トリガーによって、**text**、**ntext**、または **image** 型の列を更新できます。  
  
> [!IMPORTANT]
>  **ntext**、**text**、および **image** データ型は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の将来のバージョンで削除される予定です。 新しい開発作業では、これらのデータ型の使用は避け、現在これらのデータ型を使用しているアプリケーションは修正するようにしてください。 代わりに、 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)、 [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)、 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) を使用してください。 AFTER トリガーと INSTEAD OF トリガーでは両方とも、inserted テーブルおよび deleted テーブルで **varchar(MAX)** 、 **nvarchar(MAX)** 、および **varbinary(MAX)** 型のデータがサポートされます。  
  
メモリ最適化テーブルのトリガーの場合、最上位レベルで許可される唯一の *sql_statement* は ATOMIC ブロックです。 ATOMIC ブロック内で使用できる T-SQL は、ネイティブ プロシージャ内で使用できる T-SQL によって制限されます。  
  
\< method_specifier > **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
CLR トリガーに対して、トリガーにバインドするアセンブリのメソッドを指定します。 このメソッドは引数を受け取らず、void を返す必要があります。 *class_name* は有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子であり、アセンブリ内にアセンブリで可視のクラスとして存在している必要があります。 このクラスの名前が名前空間で修飾されており、名前空間の部分がピリオド (.) で分けられている場合は、このクラス名を角かっこ ([ ]) または引用符 (" ") で区切る必要があります。 入れ子になったクラスは使用できません。  
  
> [!NOTE]  
>  既定では、CLR コードを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能はオフになっています。 マネージド コード モジュールを参照するデータベース オブジェクトを作成、変更、削除することはできますが、[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) によって [clr enabled オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)が有効になっていない場合、これらの参照は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでは実行されません。  
  
## <a name="remarks-for-dml-triggers"></a>DML トリガーの解説  
DML トリガーは主に、ビジネス ルールとデータの整合性を設定するために使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ALTER TABLE と CREATE TABLE ステートメントで宣言参照整合性 (DRI) を使用できます。 ただし、DRI ではデータベース間の参照整合性は提供されません。 参照整合性とは、テーブルの主キーと外部キー間の関係についての規則です。 参照整合性を設定するには、ALTER TABLE と CREATE TABLE で、PRIMARY KEY と FOREIGN KEY 制約を使用します。 トリガー テーブルに制約が存在する場合、これらは INSTEAD OF トリガーが実行された後、AFTER トリガーが実行される前にチェックされます。 制約違反の場合は、INSTEAD OF トリガーの動作がロールバックされ、AFTER トリガーは起動されません。  
  
テーブルで実行される最初と最後の AFTER トリガーを、sp_settriggerorder を使用して指定できます。 1 つのテーブルで、INSERT、UPDATE、DELETE の各操作に対して、最初の AFTER トリガーと最後の AFTER トリガーをそれぞれ 1 つだけ指定できます。 同じテーブルにそれ以外の AFTER トリガーが存在する場合、それらはランダムに実行されます。  
  
ALTER TRIGGER ステートメントを使って最初と最後のトリガーを変更し、変更したトリガーに設定されていた最初と最後を示す属性を削除した場合は、sp_settriggerorder を使用して順序の値を再設定する必要があります。  
  
AFTER トリガーは、そのトリガーを起動する SQL ステートメントが正常に実行された後にのみ実行されます。 このステートメントの実行には、更新または削除されるオブジェクトに関連付けられている連鎖的なすべての参照操作と制約チェックの実行も含まれます。 AFTER トリガーは、同じテーブルの INSTEAD OF トリガーを再帰的に起動することはありません。  
  
テーブルに定義された INSTEAD OF トリガーによって、通常は INSTEAD OF トリガーを起動するステートメントがそのテーブルで再度実行される場合、トリガーの再帰呼び出しは行われません。 代わりに、そのステートメントでは、テーブルに INSTEAD OF トリガーが存在しないものとして処理が行われ、制約操作と AFTER トリガーの実行が連鎖的に開始されます。 たとえば、トリガーがテーブルの INSTEAD OF INSERT トリガーとして定義されているとします。 さらに、そのトリガーが、同じテーブルに対して INSERT ステートメントを実行する場合、INSTEAD OF トリガーによって開始される INSERT ステートメントでは、トリガーの再度の呼び出しは行われません。 トリガーによって開始される INSERT では、制約動作の実行処理とテーブルに定義されている AFTER INSERT トリガーの起動処理が開始されます。  
  
ビューに定義された INSTEAD OF トリガーによって、通常 INSTEAD OF トリガーを起動するステートメントがそのビューに対して再び実行される場合、そのトリガーの再帰呼び出しは行われません。 代わりに、そのステートメントは、そのビューの基になるベース テーブルに対する変更として解決されます。 この場合、ビューの定義では、更新可能なビューの制限をすべて満たしている必要があります。 更新可能なビューの定義については、「[ビューを使用したデータ変更](../../relational-databases/views/modify-data-through-a-view.md)」をご覧ください。  
  
たとえば、トリガーがビューの INSTEAD OF UPDATE トリガーとして定義されているとします。 さらに、そのトリガーが同じビューを参照する UPDATE ステートメントを実行する場合、INSTEAD OF トリガーによって開始される UPDATE ステートメントでは、トリガーの再度の呼び出しは行われません。 トリガーによって開始される UPDATE ステートメントは、ビューに INSTEAD OF トリガーが存在しないものとして処理が行われます。 この UPDATE によって変更された列は、単一のベース テーブルに対して解決される必要があります。 基になるベース テーブルを変更するたびに、制約の適用とそのテーブルに定義された AFTER トリガーの起動が連鎖的に開始されます。  
  
### <a name="testing-for-update-or-insert-actions-to-specific-columns"></a>特定の列に対する UPDATE または INSERT 操作のテスト  
[!INCLUDE[tsql](../../includes/tsql-md.md)] トリガーは、特定の列に対する UPDATE または INSERT による変更に基づいて特定の操作を実行するように設定できます。 これを行うには、トリガー内で [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md) または [COLUMNS_UPDATED](../../t-sql/functions/columns-updated-transact-sql.md) を使用します。 UPDATE() では、1 つの列に対する UPDATE または INSERT の試行がテストされます。 COLUMNS_UPDATED では、複数の列に対して実行される UPDATE または INSERT 操作がテストされます。 この関数は、挿入または更新された列を示すビット パターンを返します。  
  
### <a name="trigger-limitations"></a>トリガーの制限  
CREATE TRIGGER はバッチ内の最初のステートメントとして使用する必要があり、1 つのテーブルにのみ適用されます。  
  
トリガーは現在のデータベース内でしか作成できませんが、他のデータベース内のオブジェクトを参照することができます。  
  
トリガーを修飾するトリガー スキーマ名を指定する場合は、テーブル名を同じ方法で修飾します。  
  
1 つのトリガー動作を、同じ CREATE TRIGGER ステートメント内の複数のユーザー操作 (たとえば、INSERT と UPDATE) に対して定義できます。  
  
INSTEAD OF DELETE/UPDATE トリガーは、外部キーがあり、DELETE/UPDATE 操作に対する連鎖操作が定義されているテーブルには定義できません。  
  
トリガーの内部では任意の SET ステートメントを指定できます。 選択した SET オプションは、トリガーの実行中有効で、終了後は元の設定に戻ります。  
  
トリガーが起動すると、ストアド プロシージャの場合と同様に、呼び出し側アプリケーションに結果が返されます。 トリガーを実行しても結果がアプリケーションに返されないようにするには、結果を返す SELECT ステートメントや変数を割り当てるステートメントをトリガーから除外します。 ユーザーに結果を返す SELECT ステートメントまたは変数の割り当てを行うステートメントを含むトリガーでは、特別な処理が必要です。 返された結果を、トリガー テーブルの変更が許可されているすべてのアプリケーションに書き込む必要があります。 トリガー内で変数を割り当てる必要がある場合は、トリガーの先頭で SET NOCOUNT ステートメントを使用して、結果セットが返されないようにします。  
  
TRUNCATE TABLE ステートメントは実質的には DELETE ステートメントですが、個別の行の削除がログに記録されないため、トリガーがアクティブになることはありません。 ただし、TRUNCATE TABLE ステートメントを実行する権限のあるユーザー以外は、このように DELETE トリガーが回避されてしまうことに注意を払う必要はありません。  
  
ログに記録されるかどうかにかかわらず、WRITETEXT ステートメントによってトリガーがアクティブになることはありません。  
  
次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは DML トリガーでは許可されません。  
  
||||  
|-|-|-|  
|ALTER DATABASE|CREATE DATABASE|DROP DATABASE|  
|RESTORE DATABASE|RESTORE LOG|RECONFIGURE|  
  
また、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、トリガーによって起動される操作の対象となるテーブルまたはビューに対して使用する場合は、DML トリガー内では使用できません。  
  
||||  
|-|-|-|  
|CREATE INDEX (CREATE SPATIAL INDEX および CREATE XML INDEX を含む)|ALTER INDEX|DROP INDEX|  
|DBCC DBREINDEX|ALTER PARTITION FUNCTION|DROP TABLE|  
|ALTER TABLE (次の操作で使用する場合)<br /><br /> 列の追加、変更、または削除<br /><br /> パーティションの切り替え<br /><br /> PRIMARY KEY 制約や UNIQUE 制約の追加または削除|||  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではシステム テーブルに対するユーザー定義トリガーがサポートされないため、システム テーブルに対してはユーザー定義トリガーを作成しないことをお勧めします。 

### <a name="optimizing-dml-triggers"></a>DML トリガーの最適化
トリガーは、トランザクションで (黙示的に、またはそれ以外の方法で) 機能し、開いている間はリソースをロックします。 ロックは、トランザクションが (COMMIT で) 確認されるか、(ROLLBACK で) 拒否されるまで、そのままの状態を維持します。 トリガーの実行時間が長くなるほど、別のプロセスがブロックされる可能性が高くなります。 そのため、トリガーは、可能な限り継続時間が短くなるように記述します。 短い継続時間を実現するための 1 つの方法は、DML ステートメントによって変更される行が 0 行のときに、トリガーを解放することです。 

どの行も変更しないコマンドでトリガーを解放するには、システム変数 [ROWCOUNT_BIG](../functions/rowcount-big-transact-sql.md) を使用します。 

次の T-SQL コード スニペットは、行を変更しないコマンドでトリガーを解放する方法を示しています。 このコードは、各 DML トリガーの先頭に存在する必要があります。

```sql
IF (ROWCOUNT_BIG() = 0)
RETURN;
```
  
  
## <a name="remarks-for-ddl-triggers"></a>DDL トリガーの解説  
DDL トリガーでは、標準のトリガーと同様、イベントに応答してストアド プロシージャが開始されます。 ただし、標準のトリガーとは異なり、テーブルまたはビューの UPDATE、INSERT、または DELETE ステートメントに応答して実行されることはありません。 代わりに、それらは、主にデータ定義言語 (DDL) ステートメントに応答して実行されます。 このステートメントの種類には、CREATE、ALTER、DROP、GRANT、DENY、REVOKE、UPDATE STATISTICS ステートメントなどがあります。 DDL と同様の操作を実行する特定のシステム ストアド プロシージャも DDL トリガーを起動できます。  
  
> [!IMPORTANT]  
>  DDL トリガーをテストして、システム ストアド プロシージャの実行に対する応答を確認してください。 たとえば、CREATE TYPE ステートメント、sp_addtype ストアド プロシージャ、および sp_rename ストアド プロシージャは、CREATE_TYPE イベントで作成される DDL トリガーを起動します。  
  
DDL トリガーの詳細については、「[DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)」を参照してください。  
  
DDL トリガーは、ローカルまたはグローバルの一時テーブルおよびストアド プロシージャに影響するイベントに応答して起動されることはありません。  
  
DML トリガーと異なり、DDL トリガーのスコープはスキーマではありません。 このため、DDL トリガーに関するメタデータのクエリに、OBJECT_ID、OBJECT_NAME、OBJECTPROPERTY、OBJECTPROPERTYEX などの関数を使用することはできません。 代わりに、カタログ ビューを使用してください。 詳しくは、「[DDL トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-ddl-triggers.md)」をご覧ください。  
  
> [!NOTE]  
>  サーバー スコープの DDL トリガーは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーの **[トリガー]** フォルダーに表示されます。 このフォルダーは、 **[Server Objects]** フォルダーにあります。 データベース スコープの DDL トリガーは、 **[データベース トリガー]** フォルダーに表示されます。 このフォルダーは対応するデータベースの **[Programmability]** フォルダーにあります。  
  
## <a name="logon-triggers"></a>ログオン トリガー  
ログオン トリガーは、LOGON イベントに応答してストアド プロシージャを実行します。 このイベントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでユーザー セッションが確立されるときに発生します。 ログオン トリガーは、ログインの認証段階が終了した後、ユーザー セッションが確立される前に発生します。 したがって、通常は、エラー メッセージや PRINT ステートメントからのメッセージはユーザーに表示されますが、このトリガー内で発生したすべてのメッセージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに記録されます。 詳細については、「[ログオン トリガー](../../relational-databases/triggers/logon-triggers.md)」を参照してください。  
  
認証に失敗した場合、ログオン トリガーは起動しません。  
  
ログオン トリガーでは、分散トランザクションはサポートされていません。 分散トランザクションを含むログオン トリガーが起動されると、エラー 3969 が返ります。  
  
### <a name="disabling-a-logon-trigger"></a>ログオン トリガーを無効にする  
ログオン トリガーを使用すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] sysadmin **固定サーバー ロールのメンバーを含むすべてのユーザーの** への接続を効率的に禁止できます。 ログオン トリガーによって接続が禁止されているときでも、 **sysadmin** 固定サーバー ロールのメンバーは、専用管理者接続を使用するか、または [!INCLUDE[ssDE](../../includes/ssde-md.md)] を最小構成モード (-f) で起動することにより、接続できます。 詳細については、「 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。  
  
## <a name="general-trigger-considerations"></a>トリガーについての留意事項  
  
### <a name="returning-results"></a>結果の返送  
今後のバージョンの SQL Server では、トリガーを使用して結果を返す機能が削除される予定です。 結果セットを返すトリガーは、それを処理するように設計されていないアプリケーションでは予期しない動作を起こすことがあります。 新しい開発作業では、トリガーを使用して結果セットを返すことを避け、現在この方法を使用しているアプリケーションについては変更を検討してください。 トリガーが結果セットを返さないようにするには、[disallow results from triggers オプション](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md)を 1 に設定します。  
  
ログオン トリガーでは、結果セットを返すことは常に禁止されているため、この動作は構成できません。 ログオン トリガーで結果セットが生成されると、トリガーは起動に失敗し、トリガーを起動したログインの試行は拒否されます。  
  
### <a name="multiple-triggers"></a>複数のトリガー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、各 DML イベント、DDL イベント、または LOGON イベントに対して複数のトリガーを作成できます。 たとえば、既に UPDATE トリガーが作成されているテーブルに対して CREATE TRIGGER FOR UPDATE を実行すると、追加の更新トリガーが作成されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、各テーブルにおいて、INSERT、UPDATE、DELETE の各データ修正イベントに許可されるトリガーは 1 つだけでした。  
  
### <a name="recursive-triggers"></a>再帰トリガー  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ALTER DATABASE によって RECURSIVE_TRIGGERS 設定が有効になっている場合、トリガーの再帰呼び出しもサポートされます。  
  
再帰トリガーでは、次の種類の再帰呼び出しが有効になります。  
  
-   間接再帰  
  
     間接再帰では、アプリケーションでテーブル T1 が更新されると、 この操作によってトリガー TR1 が起動し、テーブル T2 が更新されます。 次にトリガー T2 が起動し、テーブル T1 が更新されます。  
  
-   直接再帰  
  
     直接再帰では、アプリケーションによってテーブル T1 が更新されます。 この操作によってトリガー TR1 が起動し、テーブル T1 が更新されます。 テーブル T1 が更新されると、トリガー TR1 が再び起動するという動作が続きます。  
  
次の例では、間接トリガー再帰と直接トリガー再帰の両方を使用します。ここでは、テーブル T1 で 2 つの更新トリガー TR1 と TR2 が定義されているとします。 トリガー TR1 によって、テーブル T1 が再帰的に更新されます。 UPDATE ステートメントでは、TR1 と TR2 が 1 回ずつ実行されます。 さらに、TR1 が起動すると、TR1 (再帰的) と TR2 の実行が開始されます。 トリガーの inserted テーブルと deleted テーブルには、そのトリガーを呼び出した UPDATE ステートメントのみに対応する行が格納されています。  
  
> [!NOTE]  
>  この動作は、ALTER DATABASE によって RECURSIVE_TRIGGERS 設定が有効になっている場合にのみ実行されます。 あるイベントに対して定義されている複数のトリガーの実行順序は定義されていません。 個々のトリガーは自己完結している必要があります。  
  
RECURSIVE_TRIGGERS の設定を無効にすると、直接再帰のみが無効になります。 間接再帰呼び出しを無効にするには、sp_configure を使用して、サーバー オプション nested triggers を 0 に設定します。  
  
いずれかのトリガーで ROLLBACK TRANSACTION が実行されると、入れ子のレベルにかかわらず、それ以降のトリガーは実行されません。  
  
### <a name="nested-triggers"></a>入れ子になったトリガー  
トリガーは、最大 32 レベルの入れ子にすることができます。 トリガーによって別のトリガーが存在するテーブルが変更された場合、2 番目のトリガーがアクティブになり、3 番目のトリガーを呼び出すことができ、以下同様になります。 この連鎖的なトリガーで無限ループが発生すると、入れ子レベルを超過した時点でトリガーは取り消されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] トリガーで、CLR ルーチン、データ型、または集計を参照することによってマネージド コードが開始された場合、この参照は 32 レベルの入れ子制限の 1 レベルとしてカウントされます。 マネージド コード内から呼び出されたメソッドは、この制限としてはカウントされません。  
  
入れ子にされたトリガーを無効にするには、sp_configure の nested triggers オプションを 0 (オフ) に設定します。 既定の構成では、入れ子になったトリガーがサポートされます。 入れ子になったトリガーがオフの場合、ALTER DATABASE によって RECURSIVE_TRIGGERS がどのように設定されていても、再帰トリガーは無効になります。  
  
INSTEAD OF トリガー内で入れ子になっている最初の AFTER トリガーは、**nested triggers** サーバー構成オプションが 0 でも起動されます。 ただし、この設定では、後の AFTER トリガーは起動されません。 アプリケーションの入れ子になっているトリガーを見直して、**nested triggers** サーバー構成オプションが 0 に設定されている場合に、アプリケーションがビジネス ルールに従っているかどうかを判断します。 該当しない場合は、適切な変更を行います。  
  
### <a name="deferred-name-resolution"></a>名前の遅延解決  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[tsql](../../includes/tsql-md.md)] のストアド プロシージャ、トリガー、およびバッチで、コンパイル時に存在しないテーブルを参照できます。 この機能を名前の遅延解決といいます。  
  
## <a name="permissions"></a>アクセス許可  
DML トリガーを作成するには、トリガーを作成するテーブルまたはビューに対する ALTER 権限が必要です。  
  
サーバー スコープ (ON ALL SERVER) の DDL トリガー、またはログオン トリガーを作成するには、サーバーに対する CONTROL SERVER 権限が必要です。 データベース スコープ (ON DATABASE) の DDL トリガーを作成するには、現在のデータベースに対する ALTER ANY DATABASE DDL TRIGGER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-a-dml-trigger-with-a-reminder-message"></a>A. DML トリガーを事前通知と組み合わせて使用する  
次の DML トリガーは、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の `Customer` テーブルでデータの追加または変更が試行されたときに、クライアントに対してメッセージを表示します。  
  
```sql  
CREATE TRIGGER reminder1  
ON Sales.Customer  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Customer Relations', 16, 10);  
GO  
```  
  
### <a name="b-using-a-dml-trigger-with-a-reminder-e-mail-message"></a>B. DML トリガーを電子メール メッセージと組み合わせて使用する  
次の例は、`MaryM` テーブルが変更されたときに、指定したユーザー (`Customer`) に電子メールを送信します。  
  
```sql  
CREATE TRIGGER reminder2  
ON Sales.Customer  
AFTER INSERT, UPDATE, DELETE   
AS  
   EXEC msdb.dbo.sp_send_dbmail  
        @profile_name = 'AdventureWorks2012 Administrator',  
        @recipients = 'danw@Adventure-Works.com',  
        @body = 'Don''t forget to print a report for the sales force.',  
        @subject = 'Reminder';  
GO  
```  
  
### <a name="c-using-a-dml-after-trigger-to-enforce-a-business-rule-between-the-purchaseorderheader-and-vendor-tables"></a>C. DML AFTER トリガーを使用して、PurchaseOrderHeader テーブルと Vendor テーブルの間にビジネス ルールを設定する  
CHECK 制約で参照できるのは、列レベルまたはテーブル レベルの制約が定義されている列のみであるため、テーブル間にまたがる制約 (ここでは、ビジネス ルール) はすべてトリガーとして定義する必要があります。  
  
次の例は、DML トリガーを AdventureWorks2012 データベースに作成します。 このトリガーでは、`PurchaseOrderHeader` テーブルに新しい発注を挿入しようとしたときに、ベンダーの信用格付けが良好であるかどうか (5 ではない) がチェックされます。 ベンダーの信用格付けを取得するには、`Vendor` テーブルを参照する必要があります。 信用格付けが低い場合は、メッセージが表示され、挿入は発生されません。  
  
```sql  
-- This trigger prevents a row from being inserted in the Purchasing.PurchaseOrderHeader 
-- table when the credit rating of the specified vendor is set to 5 (below average).  
  
CREATE TRIGGER Purchasing.LowCredit ON Purchasing.PurchaseOrderHeader  
AFTER INSERT  
AS  
IF (ROWCOUNT_BIG() = 0)
RETURN;
IF EXISTS (SELECT *  
           FROM Purchasing.PurchaseOrderHeader AS p   
           JOIN inserted AS i   
           ON p.PurchaseOrderID = i.PurchaseOrderID   
           JOIN Purchasing.Vendor AS v   
           ON v.BusinessEntityID = p.VendorID  
           WHERE v.CreditRating = 5  
          )  
BEGIN  
RAISERROR ('A vendor''s credit rating is too low to accept new  
purchase orders.', 16, 1);  
ROLLBACK TRANSACTION;  
RETURN   
END;  
GO  
  
-- This statement attempts to insert a row into the PurchaseOrderHeader table  
-- for a vendor that has a below average credit rating.  
-- The AFTER INSERT trigger is fired and the INSERT transaction is rolled back.  
  
INSERT INTO Purchasing.PurchaseOrderHeader (RevisionNumber, Status, EmployeeID,  
VendorID, ShipMethodID, OrderDate, ShipDate, SubTotal, TaxAmt, Freight)  
VALUES (  
2  
,3  
,261  
,1652  
,4  
,GETDATE()  
,GETDATE()  
,44594.55  
,3567.564  
,1114.8638 );  
GO  
  
```  
  
### <a name="d-using-a-database-scoped-ddl-trigger"></a>D. データベース スコープの DDL トリガーを使用する  
次の例では、DDL トリガーを使用して、データベースのシノニムが削除されないようにします。  
  
```sql  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_SYNONYM  
AS   
IF (@@ROWCOUNT = 0)
RETURN;
   RAISERROR ('You must disable Trigger "safety" to remove synonyms!', 10, 1)  
   ROLLBACK  
GO  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
### <a name="e-using-a-server-scoped-ddl-trigger"></a>E. サーバー スコープの DDL トリガーを使用する  
次の例では、DDL トリガーを使用して、現在のサーバー インスタンスで CREATE DATABASE イベントが発生したときにメッセージを表示し、`EVENTDATA` 関数を使用して、対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのテキストを取得します。 DDL トリガーで EVENTDATA を使用するその他の例については、「[EVENTDATA 関数の使用](../../relational-databases/triggers/use-the-eventdata-function.md)」を参照してください。  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
```sql  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
```  
  
### <a name="f-using-a-logon-trigger"></a>F. ログオン トリガーを使用する  
次のログオン トリガーの例では、*login_test* ログインで既に 3 つのユーザー セッションが実行されている場合に、そのログインのメンバーとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログインを試行すると拒否されます。  
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
```sql  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
  
```  
  
### <a name="g-viewing-the-events-that-cause-a-trigger-to-fire"></a>G. トリガーを起動するイベントを表示する  
次の例は、`sys.triggers` および `sys.trigger_events` カタログ ビューをクエリし、どの [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語イベントでトリガー `safety` が起動されるかを特定します。 トリガー `safety` は、上の例 "D" で作成されます。  
  
```sql  
SELECT TE.*  
FROM sys.trigger_events AS TE  
JOIN sys.triggers AS T ON T.object_id = TE.object_id  
WHERE T.parent_class = 0 AND T.name = 'safety';  
GO  
```  

    

## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [TRIGGER_NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/trigger-nestlevel-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)   
 [UPDATE&#40;&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)   
 [DML トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [DDL トリガーに関する情報の取得](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  


