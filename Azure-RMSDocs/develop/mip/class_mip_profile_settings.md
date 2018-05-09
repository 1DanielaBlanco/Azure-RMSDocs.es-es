# <a name="class-mipprofilesettings"></a>clase mip::Profile::Settings 
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<Profile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  Interfaz para configurar el perfil.
public inline const std::string& GetPath() const  |  Obtiene la ruta de acceso al estado almacenado.
public inline bool GetUseInMemoryStorage() const  |  Obtiene la marca de uso de almacenamiento en memoria.
public inline const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  Obtiene el delegado de autenticación.
public inline const std::shared_ptr<Profile::Observer>& GetObserver() const  |  Obtiene el observador de eventos.
public inline const ApplicationInfo GetApplicationInfo() const  |  Obtiene la información de aplicación.
  
## <a name="members"></a>Miembros
  
### <a name="settings"></a>Configuración
Interfaz para configurar el perfil.
  
#### <a name="parameters"></a>Parámetros
* path La ruta de acceso a un directorio en el que el sdk almacenará el estado del perfil. 
* useInMemoryStorage Marca que indica si se debe almacenar o no el estado en disco. 
* authDelegate El delegado de autenticación utilizado por el SDK para adquirir tokens de autenticación. 
* observer Una clase que implementa la interfaz [Profile::Observer](#classmip_1_1_profile_1_1_observer). Puede se nullptr. 
* applicationInfo Los identificadores de aplicación que se usan para el acceso al servicio.
  
### <a name="getpath"></a>GetPath
Obtiene la ruta de acceso al estado almacenado.
  
#### <a name="returns"></a>Devuelve
Ruta de acceso al estado almacenado.
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Obtiene la marca de uso de almacenamiento en memoria.
  
#### <a name="returns"></a>Devuelve
True si se establece el uso en memoria; de lo contrario, false.
  
### <a name="getauthdelegate"></a>GetAuthDelegate
Obtiene el delegado de autenticación.
  
#### <a name="returns"></a>Devuelve
El delegado de autenticación.
  
### <a name="profileobserver"></a>Profile::Observer
Obtiene el observador de eventos.
  
#### <a name="returns"></a>Devuelve
El observador de eventos.
  
### <a name="applicationinfo"></a>ApplicationInfo
Obtiene la información de aplicación.
  
#### <a name="returns"></a>Devuelve
El tipo de aplicación.