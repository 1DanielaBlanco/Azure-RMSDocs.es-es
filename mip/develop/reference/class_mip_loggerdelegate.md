---
title: clase mip LoggerDelegate
description: Referencia de la clase mip LoggerDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b25cdb177735feccfa5c4d344613e4747d18b77f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445859"
---
# <a name="class-miploggerdelegate"></a>clase mip::LoggerDelegate 
Una clase que define la interfaz para el registrador de SDK de MIP.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath, LogLevel logLevel)  |  Inicialice el registrador.
 public LogLevel GetLogLevel() const  |  Obtenga el nivel de registro más bajo que pueda desencadenar un evento de registro.
 public void Flush()  |  Vacíe el registrador.
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Escriba una instrucción de registro en el archivo de registro.
  
## <a name="members"></a>Miembros
  
### <a name="init"></a>Init
Inicialice el registrador.

Parámetros:  
* **storagePath**: la ruta de acceso a la ubicación donde se puede almacenar el estado persistente, incluidos los registros,. 


* **logLevel**: obtenga el nivel de registro más bajo que pueda desencadenar un evento de registro.


  
### <a name="loglevel"></a>LogLevel
Obtenga el nivel de registro más bajo que pueda desencadenar un evento de registro.

  
**Devuelve**: el nivel de registro más bajo que pueda desencadenar un evento de registro.
  
### <a name="flush"></a>Vaciar
Vacíe el registrador.
  
### <a name="writetolog"></a>WriteToLog
Escriba una instrucción de registro en el archivo de registro.

Parámetros:  
* **level**: nivel de registro para la instrucción de registro. 


* **message**: el mensaje para la instrucción de registro. 


* **function**: el nombre de función para la instrucción de registro. 


* **file**: el nombre de archivo donde se generó la instrucción de registro. 


* **line**: el número de línea donde se generó la instrucción de registro.

