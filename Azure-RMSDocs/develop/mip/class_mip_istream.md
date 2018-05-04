# <a name="class-mipistream"></a>clase mip::IStream 
Interfaz base para los flujos protegidos.
Procede de Windows::Storage::Streams::IRandomAccessStream::IRandomAccessStream y Windows::Storage::Streams::FileRandomAccessStream::FileRandomAccessStream. [https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx)[https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx)
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public std::shared_future< int64_t > ReadAsync | Lee un bloque de datos del flujo de forma asincrónica.
public std::shared_future< int64_t > WriteAsync | Escribe un bloque de datos en el flujo de forma asincrónica.
public std::future< bool > FlushAsync | Vacía el búfer del flujo de salida de forma asincrónica.
public int64_t Read | Lee un bloque de datos del flujo de forma sincrónica.
public int64_t Write | Escribe un bloque de datos en el flujo de forma sincrónica.
public bool Flush | Vacía el búfer del flujo de salida de forma sincrónica.
public SharedStream Clone | Clona el flujo.
public void Seek | Busca una posición en el flujo.
public bool CanRead | Determina si el flujo se puede leer o no.
public bool CanWrite | Determina si el flujo se puede escribir o no.
public uint64_t Position | Obtiene la posición actual del flujo desde el principio (en bytes)
public uint64_t Size | Obtiene el tamaño del flujo (en bytes)
public void Size | Establece el tamaño del flujo (en bytes)
public inline virtual std::vector< uint8_t > Read | Lee un bloque de datos del flujo de forma sincrónica.
## <a name="members"></a>Miembros
### <a name="readasync"></a>ReadAsync
Lee un bloque de datos del flujo de forma asincrónica.
#### <a name="parameters"></a>Parámetros
* pbBuffer Búfer en el que se debe leer el flujo 
* cbBuffer Tamaño del búfer 
* cbOffset Desplazamiento desde el principio del flujo de entrada donde debe comenzar la lectura 
* launchType Tipo de inicio asincrónico
#### <a name="returns"></a>Devuelve
Futuro asincrónico que contiene el número real de bytes leídos Asegúrese de que el búfer existe hasta que el resultado se recupere de std::future
### <a name="writeasync"></a>WriteAsync
Escribe un bloque de datos en el flujo de forma asincrónica.
#### <a name="parameters"></a>Parámetros
* cpbBuffer Búfer de datos que se van a escribir 
* cbBuffer Tamaño del búfer 
* cbOffset Desplazamiento desde el principio del flujo de salida hasta el lugar donde debe comenzar la escritura 
* launchType Tipo de inicio asincrónico
#### <a name="returns"></a>Devuelve
Futuro asincrónico que contiene el número real de bytes escritos Asegúrese de que el búfer existe hasta que el resultado se recupere de std::future
### <a name="flushasync"></a>FlushAsync
Vacía el búfer del flujo de salida de forma asincrónica.
#### <a name="parameters"></a>Parámetros
* launchType Tipo de inicio asincrónico
#### <a name="returns"></a>Devuelve
Futuro asincrónico que contiene si el vaciado se realizó correctamente o no
### <a name="read"></a>Lectura
Lee un bloque de datos del flujo de forma sincrónica.
#### <a name="parameters"></a>Parámetros
* pbBuffer Búfer en el que se debe leer el flujo 
* cbBuffer Tamaño del búfer
#### <a name="returns"></a>Devuelve
Número real de bytes leídos
### <a name="write"></a>Escribir
Escribe un bloque de datos en el flujo de forma sincrónica.
#### <a name="parameters"></a>Parámetros
* cpbBuffer Búfer de datos que se van a escribir 
* cbBuffer Tamaño del búfer
#### <a name="returns"></a>Devuelve
Número real de bytes escritos
### <a name="flush"></a>Vaciar
Vacía el búfer del flujo de salida de forma sincrónica.
#### <a name="returns"></a>Devuelve
Si el vaciado se realizó correctamente o no
### <a name="sharedstream"></a>SharedStream
Clona el flujo.
#### <a name="returns"></a>Devuelve
Flujo clonado
### <a name="seek"></a>Seek
Busca una posición en el flujo.
#### <a name="parameters"></a>Parámetros
* u64Position Desplazamiento de bytes desde el principio del flujo
### <a name="canread"></a>CanRead
Determina si el flujo se puede leer o no.
#### <a name="returns"></a>Devuelve
Si el flujo se puede leer o no
### <a name="canwrite"></a>CanWrite
Determina si el flujo se puede escribir o no.
#### <a name="returns"></a>Devuelve
Si el flujo se puede escribir o no
### <a name="position"></a>Posición
Obtiene la posición actual del flujo desde el principio (en bytes)
#### <a name="returns"></a>Devuelve
Posición actual del flujo desde el principio (en bytes)
### <a name="size"></a>Tamaño
Obtiene el tamaño del flujo (en bytes)
#### <a name="returns"></a>Devuelve
Tamaño del flujo (en bytes)
### <a name="size"></a>Tamaño
Establece el tamaño del flujo (en bytes)
#### <a name="parameters"></a>Parámetros
* u64Value Tamaño del flujo (en bytes)
### <a name="read"></a>Lectura
Lee un bloque de datos del flujo de forma sincrónica.
#### <a name="parameters"></a>Parámetros
* u64size Tamaño de los datos que se van a leer (en bytes)
#### <a name="returns"></a>Devuelve
Vector de lectura de datos real