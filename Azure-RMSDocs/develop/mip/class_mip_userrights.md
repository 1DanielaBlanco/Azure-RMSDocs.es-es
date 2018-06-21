# <a name="class-mipuserrights"></a>clase mip::UserRights 
Representa un grupo de usuarios y los derechos asociados con ellos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public UserRights(const UserList& users, const RightList& rights)  |  Constructor [UserRights](class_mip_userrights.md).
 public const UserList& Users() const  |  Obtiene los usuarios asociados a un conjunto de derechos.
 public const RightList& Rights() const  |  Obtiene los derechos asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userrights"></a>UserRights
Constructor [UserRights](class_mip_userrights.md).

Parámetros:  
* **users**: grupo de usuarios que comparten los mismos derechos 


* **rights**: derechos compartidos por grupo de usuarios


  
### <a name="userlist"></a>UserList
Obtiene los usuarios asociados a un conjunto de derechos.

  
**Devuelve**: usuarios asociados a un conjunto de derechos
  
### <a name="rightlist"></a>RightList
Obtiene los derechos asociados a un grupo de usuarios.

  
**Devuelve**: derechos asociados a un grupo de usuarios