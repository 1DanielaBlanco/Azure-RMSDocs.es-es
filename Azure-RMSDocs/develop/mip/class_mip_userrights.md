# <a name="class-mipuserrights"></a>clase mip::UserRights 
Representa un grupo de usuarios y los derechos asociados con ellos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline UserRights(const UserList& users, const RightList& rights)  |  Constructor [UserRights](#classmip_1_1_user_rights).
public inline const UserList& Users() const  |  Obtiene los usuarios asociados a un conjunto de derechos.
public inline const RightList& Rights() const  |  Obtiene los derechos asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userrights"></a>UserRights
Constructor [UserRights](#classmip_1_1_user_rights).
  
#### <a name="parameters"></a>Parámetros
* users Grupo de usuarios que comparten los mismos derechos 
* rights Derechos compartidos por grupo de usuarios
  
### <a name="userlist"></a>UserList
Obtiene los usuarios asociados a un conjunto de derechos.
  
#### <a name="returns"></a>Devuelve
Usuarios asociados a un conjunto de derechos
  
### <a name="rightlist"></a>RightList
Obtiene los derechos asociados a un grupo de usuarios.
  
#### <a name="returns"></a>Devuelve
Derechos asociados a un grupo de usuarios