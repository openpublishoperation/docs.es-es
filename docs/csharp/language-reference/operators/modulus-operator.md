---
title: "Operador % (Referencia de C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "%_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "% (operador) [C#]"
  - "operador de módulo [C#]"
ms.assetid: 3b74f4f9-fd9c-45e7-84fa-c8d71a0dfad7
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Operador % (Referencia de C#)
El operador de `%` calcula el resto después de dividir el primer operando por el segundo.  Todos los tipos numéricos han predefinido a operadores del resto.  
  
## Comentarios  
 Los tipos definidos por el usuario pueden sobrecargar el operador `%` \(vea [operador](../../../csharp/language-reference/keywords/operator.md)\).  Cuando se sobrecarga un operador binario, el operador de asignación correspondiente, si existe, también se sobrecarga de modo implícito.  
  
## Ejemplo  
 [!code-cs[csRefOperators#9](../../../csharp/language-reference/operators/codesnippet/CSharp/modulus-operator_1.cs)]  
  
## Comentarios  
 Observe los errores de redondeo que presenta el tipo double.  
  
## Vea también  
 [Referencia de C\#](../../../csharp/language-reference/index.md)   
 [Guía de programación de C\#](../../../csharp/programming-guide/index.md)   
 [operadores de C\#](../../../csharp/language-reference/operators/index.md)