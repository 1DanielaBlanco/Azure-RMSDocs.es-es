# <a name="class-mipistream"></a>clase mip::IStream 
Interfaz base para los flujos protegidos.
Procede de Windows::Storage::Streams::IRandomAccessStream::IRandomAccessStream y Windows::Storage::Streams::FileRandomAccessStream::FileRandomAccessStream. [https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx)[https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx)
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::shared_future<int64_t> ReadAsync(uint8_t* pbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  Lee un bloque de datos del flujo de forma asincrónica.
public std::shared_future<int64_t> WriteAsync(const uint8_t* cpbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  Escribe un bloque de datos en el flujo de forma asincrónica.
public std::future<bool> FlushAsync(std::launch launchType)  |  Vacía el búfer del flujo de salida de forma asincrónica.
 public int64_t Read(uint8_t* pbBuffer, int64_t cbBuffer)  |  Lee un bloque de datos del flujo de forma sincrónica.
 public int64_t Write(const uint8_t* cpbBuffer, int64_t cbBuffer)  |  Escribe un bloque de datos en el flujo de forma sincrónica.
 public bool Flush()  |  Vacía el búfer del flujo de salida de forma sincrónica.
 public SharedStream Clone()  |  Clona el flujo.
 public void Seek(uint64_t u64Position)  |  Busca una posición en el flujo.
 public bool CanRead() const  |  Determina si el flujo se puede leer o no.
 public bool CanWrite() const  |  Determina si el flujo se puede escribir o no.
 public uint64_t Position()  |  Obtiene la posición actual del flujo desde el principio (en bytes)
 public uint64_t Size()  |  Obtiene el tamaño del flujo (en bytes)
 public void Size(uint64_t u64Value)  |  Establece el tamaño del flujo (en bytes)
public virtual std::vector<uint8_t> Read(uint64_t u64size)  |  Lee un bloque de datos del flujo de forma sincrónica.
  
## <a name="members"></a>Miembros
  
### <a name="readasync"></a>ReadAsync
Lee un bloque de datos del flujo de forma asincrónica.

Parámetros:  
* **pbBuffer**: búfer en el que se debe leer el flujo 


* **cbBuffer**: tamaño del búfer 


* **cbOffset**: desplazamiento desde el principio del flujo de entrada donde debe comenzar la lectura 


* **launchType**: tipo de inicio asincrónico



  
**Devuelve**: futuro asincrónico que contiene el número real de bytes leídos. Asegúrese de que el búfer existe hasta que el resultado se recupere de std::future
  
### <a name="writeasync"></a>WriteAsync
Escribe un bloque de datos en el flujo de forma asincrónica.

Parámetros:  
* **cpbBuffer**: búfer de datos que se van a escribir 


* **cbBuffer**: tamaño del búfer 


* **cbOffset**: desplazamiento desde el principio del flujo de salida hasta el lugar donde debe comenzar la escritura 


* **launchType**: tipo de inicio asincrónico



  
**Devuelve**: futuro asincrónico que contiene el número real de bytes escritos. Asegúrese de que el búfer existe hasta que el resultado se recupere de std::future
  
### <a name="flushasync"></a>FlushAsync
Vacía el búfer del flujo de salida de forma asincrónica.

Parámetros:  
* **launchType**: tipo de inicio asincrónico



  
**Devuelve**: futuro asincrónico que contiene si el vaciado se realizó correctamente o no
  
### <a name="read"></a>Lectura
Lee un bloque de datos del flujo de forma sincrónica.

Parámetros:  
* **pbBuffer**: búfer en el que se debe leer el flujo 


* **cbBuffer**: tamaño del búfer



  
**Devuelve**: número real de bytes leídos
  
### <a name="write"></a>Escribir
Escribe un bloque de datos en el flujo de forma sincrónica.

Parámetros:  
* **cpbBuffer**: búfer de datos que se van a escribir 


* **cbBuffer**: tamaño del búfer



  
**Devuelve**: número real de bytes escritos
  
### <a name="flush"></a>Vaciar
Vacía el búfer del flujo de salida de forma sincrónica.

  
**Devuelve**: si el vaciado se realizó correctamente o no
  
### <a name="sharedstream"></a>SharedStream
Clona el flujo.

  
**Devuelve**: flujo clonado
  
### <a name="seek"></a>Seek
Busca una posición en el flujo.

Parámetros:  
* **u64Position**: desplazamiento de bytes desde el principio del flujo


  
### <a name="canread"></a>CanRead
Determina si el flujo se puede leer o no.

  
**Devuelve**: determina si el flujo se puede leer o no
  
### <a name="canwrite"></a>CanWrite
Determina si el flujo se puede escribir o no.

  
**Devuelve**: determina si el flujo se puede escribir o no
  
### <a name="position"></a>Posición
Obtiene la posición actual del flujo desde el principio (en bytes)

  
**Devuelve**: posición actual del flujo desde el principio (en bytes)
  
### <a name="size"></a>Tamaño
Obtiene el tamaño del flujo (en bytes)

  
**Devuelve**: tamaño del flujo (en bytes)
  
### <a name="size"></a>Tamaño
Establece el tamaño del flujo (en bytes)

Parámetros:  
* **u64Value**: tamaño del flujo (en bytes)


  
### <a name="read"></a>Lectura
Lee un bloque de datos del flujo de forma sincrónica.

Parámetros:  
* **u64size**: tamaño de los datos que se van a leer (en bytes)



  
**Devuelve**: vector de lectura de datos real