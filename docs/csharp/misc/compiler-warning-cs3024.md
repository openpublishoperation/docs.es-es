---
title: "Advertencia del compilador CS3024 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "CS3024"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS3024"
ms.assetid: fef9db31-9a7f-42d5-ad37-3e7faf661f95
caps.latest.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 7
---
# Advertencia del compilador CS3024
El tipo de restricción 'tipo' no es conforme a CLS  
  
 El compilador emite esta advertencia porque el uso de un tipo conforme a CLS como una restricción de tipo genérico puede hacer que sea imposible que código escrito en algunos lenguajes pueda usar la clase genérica.  
  
### Para eliminar esta advertencia  
  
1.  Use un tipo conforme a CLS para la restricción de tipo.  
  
## Ejemplo  
 El ejemplo siguiente genera el error CS3024 en varias ubicaciones:  
  
```  
// cs3024.cs // Compile with: /target:library [assembly: System.CLSCompliant(true)] [type: System.CLSCompliant(false)] public class TestClass // CS3024 { public ushort us; } [type: System.CLSCompliant(false)] public interface ITest // CS3024 {} public interface I<T> where T : TestClass {} public class TestClass_2<T> where T : ITest {} public class TestClass_3<T> : I<T> where T : TestClass {} public class TestClass_4<T> : TestClass_2<T> where T : ITest {} public class Test { public static int Main() { return 0; } }  
```  
  
## Vea también  
 [Restricciones de tipos de parámetros](../../csharp/programming-guide/generics/constraints-on-type-parameters.md)