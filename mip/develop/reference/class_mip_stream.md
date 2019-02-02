---
title: clase mip::Stream
description: 'Documenta la clase MIP:: Stream de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4289b39ba454b19c6836a7eaccb6333cbb9000b4
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651707"
---
# <a name="class-mipstream"></a>clase mip::Stream 
Una clase que define la interfaz entre el SDK de MIP y el contenido basado en el flujo.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  Lee en un búfer desde el flujo.
public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  Escribe en el flujo desde un búfer.
public bool Flush()  |  Vacía el flujo.
public void Seek(int64_t position)  |  Busca la posición específica en el flujo.
public bool CanRead() const  |  Una comprobación de si se puede leer la secuencia.
public bool CanWrite() const  |  Una comprobación de si se puede escribir en la secuencia.
public int64_t Position()  |  Obtiene la posición actual en el flujo.
public int64_t Size()  |  Obtiene el tamaño del contenido dentro del flujo.
public void Size(int64_t value)  |  Establece el tamaño del flujo.
  
## <a name="members"></a>Miembros
  
### <a name="read-function"></a>Read, función
Lee en un búfer desde el flujo.

Parámetros:  
* **buffer**: puntero a un búfer 


* **bufferLength**: tamaño del búfer. 



  
**Devuelve**: Número de bytes leídos.
  
### <a name="write-function"></a>Write (función)
Escribe en el flujo desde un búfer.

Parámetros:  
* **buffer**: puntero a un búfer 


* **bufferLength**: tamaño del búfer. 



  
**Devuelve**: Número de bytes escritos.
  
### <a name="flush-function"></a>Flush (función)
Vacía el flujo.

  
**Devuelve**: False else es True si se realiza correctamente.
  
### <a name="seek-function"></a>Seek (función)
Busca la posición específica en el flujo.

Parámetros:  
* **position**: para buscar en el flujo.


  
### <a name="canread-function"></a>CanRead (función)
Una comprobación de si se puede leer la secuencia.

  
**Devuelve**: True si se puede leer false else.
  
### <a name="canwrite-function"></a>Función CanWrite
Una comprobación de si se puede escribir en la secuencia.

  
**Devuelve**: True si se puede escribir false else.
  
### <a name="position-function"></a>Position, función
Obtiene la posición actual en el flujo.

  
**Devuelve**: Posición dentro de la secuencia.
  
### <a name="size-function"></a>Función de tamaño
Obtiene el tamaño del contenido dentro del flujo.

  
**Devuelve**: El tamaño de la secuencia.
  
### <a name="size-function"></a>Función de tamaño
Establece el tamaño del flujo.

Parámetros:  
* **stream**: tamaño.

