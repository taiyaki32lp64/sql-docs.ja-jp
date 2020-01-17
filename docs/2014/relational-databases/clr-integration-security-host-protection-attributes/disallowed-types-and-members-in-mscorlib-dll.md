---
title: Mscorlib.dll に型とメンバーを許可されていません |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: daf82d4b-2f6d-44ca-9148-75193321b6d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 43f71d7dc73239b240b841e14a11f3f28f755b61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874354"
---
# <a name="disallowed-types-and-members-in-mscorlibdll"></a>mscorlib.dll の許可されない型およびメンバー
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共通言語統合 (CLR) のプログラミングには、型またはメンバーを持つの使用が許可されない、`HostProtectionAttribute`を指定する、`System.Security.Permissions.HostProtectionResource`列挙の値を持つ`ExternalProcessMgmt`、 `ExternalThreading`、 `MayLeakOnAbort`、 `SecurityInfrastructure`、 `SelfAffectingProcessMgmnt`、`SelfAffectingThreading`、 **SharedState**、 `Synchronization`、または`UI`します。 次の表は、ホスト保護属性 (HPA) 値が許可されない mscorlib.dll アセンブリのメンバーおよび型を示しています。  
  
> [!NOTE]  
>  この一覧は、サポートされているアセンブリから作成されたものです。 詳細については、次を参照してください。[サポートされている .NET Framework ライブラリ](../clr-integration/database-objects/supported-net-framework-libraries.md)します。  
  
|型またはメンバー|HPA 値|  
|--------------------|--------------------|  
|SyncStream.BeginRead()|ExternalThreading|  
|SyncStream.BeginWrite()|ExternalThreading|  
|System.Collections.ArrayList.Synchronized()|Synchronization|  
|System.Collections.Hashtable.Synchronized()|Synchronization|  
|System.Collections.Queue.Synchronized()|Synchronization|  
|System.Collections.SortedList.Synchronized()|Synchronization|  
|System.Collections.Stack.Synchronized()|Synchronization|  
|System.Console.Beep()|UI|  
|System.Console.get_Error()|UI|  
|System.Console.get_In()|UI|  
|System.Console.get_KeyAvailable()|UI|  
|System.Console.get_Out()|UI|  
|System.Console.OpenStandardError()|UI|  
|System.Console.OpenStandardInput()|UI|  
|System.Console.OpenStandardOutput()|UI|  
|System.Console.Read()|UI|  
|System.Console.ReadKey()|UI|  
|System.Console.ReadLine()|UI|  
|System.Console.SetError()|UI|  
|System.Console.SetIn()|UI|  
|System.Console.SetOut()|UI|  
|System.Console.Write()|UI|  
|System.Console.WriteLine()|UI|  
|System.Diagnostics.LogMessageEventHandler|ExternalThreading、Synchronization|  
|System.IO.FileStream.BeginRead()|ExternalThreading|  
|System.IO.FileStream.BeginWrite()|ExternalThreading|  
|System.IO.Stream.Synchronized()|Synchronization|  
|System.IO.TextReader.Synchronized()|Synchronization|  
|System.IO.TextWriter.Synchronized()|Synchronization|  
|System.Reflection.Emit.AssemblyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.ConstructorBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.CustomAttributeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EnumBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EventBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.FieldBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodRental|MayLeakOnAbort|  
|System.Reflection.Emit.ModuleBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.PropertyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.TypeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.UnmanagedMarshal|MayLeakOnAbort|  
|System.Security.Principal.WindowsPrincipal|SecurityInfrastructure|  
|System.Threading.AutoResetEvent|ExternalThreading、Synchronization|  
|System.Threading.EventWaitHandle|ExternalThreading、Synchronization|  
|System.Threading.ManualResetEvent|ExternalThreading、Synchronization|  
|System.Threading.Monitor|ExternalThreading、Synchronization|  
|System.Threading.Mutex|ExternalThreading、Synchronization|  
|System.Threading.ReaderWriterLock|ExternalThreading、Synchronization|  
|System.Threading.Thread.AllocateDataSlot()|ExternalThreading、SharedState|  
|System.Threading.Thread.AllocateNamedDataSlot()|ExternalThreading、SharedState|  
|System.Threading.Thread.BeginCriticalRegion()|ExternalThreading、Synchronization|  
|System.Threading.Thread.EndCriticalRegion()|ExternalThreading、Synchronization|  
|System.Threading.Thread.FreeNamedDataSlot()|ExternalThreading、SharedState|  
|System.Threading.Thread.GetData()|ExternalThreading、SharedState|  
|System.Threading.Thread.GetNamedDataSlot()|ExternalThreading、SharedState|  
|System.Threading.Thread.Join()|ExternalThreading、Synchronization|  
|System.Threading.Thread.set_ApartmentState()|Synchronization、SelfAffectingThreading|  
|System.Threading.Thread.set_CurrentUICulture()|ExternalThreading|  
|System.Threading.Thread.set_IsBackground()|SelfAffectingThreading|  
|System.Threading.Thread.set_Name()|ExternalThreading|  
|System.Threading.Thread.set_Priority()|SelfAffectingThreading|  
|System.Threading.Thread.SetApartmentState()|Synchronization、SelfAffectingThreading|  
|System.Threading.Thread.SetData()|ExternalThreading、SharedState|  
|System.Threading.Thread.SpinWait()|ExternalThreading、Synchronization|  
|System.Threading.Thread.Start()|ExternalThreading、Synchronization|  
|System.Threading.Thread.TrySetApartmentState()|Synchronization、SelfAffectingThreading|  
|System.Threading.ThreadPool|ExternalThreading、Synchronization|  
|System.Threading.Timer|ExternalThreading、Synchronization|  
|System.Threading.TimerBase|ExternalThreading、Synchronization|  
  
## <a name="see-also"></a>参照  
 [ホスト保護属性と CLR 統合プログラミング](host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll の許可されない型およびメンバー](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [System.dll の許可されない型およびメンバー](disallowed-types-and-members-in-system-dll.md)   
 [System.Data.dll の許可されない型およびメンバー](disallowed-types-and-members-in-system-data-dll.md)   
 [System.Core.dll の許可されない型およびメンバー](disallowed-types-and-members-in-system-core-dll.md)  
  
  
