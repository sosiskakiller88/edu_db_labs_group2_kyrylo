# Проєктування бази даних
## Модель бізнес-об'єктів

@startuml
action action #white;line:white;text:white;

entity User #c7e4ab
entity User.id #d1d1fa
entity User.email #d1d1fa
entity User.password #d1d1fa
entity User.roleId #d1d1fa

User.id -up-* User
User.email -up-* User
User.password -up-* User
User.roleId -up-* User

entity Role #c7e4ab
entity Role.id #d1d1fa
entity Role.name #d1d1fa
entity Role.description #d1d1fa

Role.id -up-* Role
Role.name -up-* Role
Role.description -up-* Role

entity PermHasRole #c7e4ab
entity PermHasRole.permisionId #d1d1fa
entity PermHasRole.roleName #d1d1fa

PermHasRole.permisionId --* PermHasRole
PermHasRole.roleName --* PermHasRole

entity Permision #c7e4ab
entity Permision.id #d1d1fa
entity Permision.name #d1d1fa

Permision.id --* Permision
Permision.name --* Permision

entity PubRequest #c7e4ab
entity PubRequest.name #d1d1fa
entity PubRequest.date #d1d1fa

PubRequest.name --* PubRequest
PubRequest.date --* PubRequest

entity MediaData #c7e4ab
entity MediaData.id #d1d1fa
entity MediaData.name #d1d1fa
entity MediaData.fileType #d1d1fa

MediaData.id --* MediaData
MediaData.name --* MediaData
MediaData.fileType --* MediaData

entity Action #c7e4ab
entity Action.id #d1d1fa
entity Action.name #d1d1fa
entity Action.description #d1d1fa

Action.id --* Action
Action.name --* Action
Action.description --* Action

entity Guest
entity RegisteredUser
entity Editor
entity Admin

entity AccountManage
entity DataManage
entity SearchManage
entity SupportManage

Guest ..> Role :instanceOf
RegisteredUser ..> Role :instanceOf
Editor ..> Role :instanceOf
Admin ..> Role :instanceOf

AccountManage .up.> Action :instanceOf
DataManage .up.> Action :instanceOf
SearchManage .up.> Action :instanceOf
SupportManage .up.> Action :instanceOf

Permision "1.1" -- "0.*" PermHasRole
PermHasRole "0.*" -- "1.1" Role
Role "1.1" -right- "0.*" User

MediaData "0.*" -- "1.1" PubRequest
PubRequest "0.*" -- "1.1" Action

Action "0.*" -- "1.1" User
@enduml

## ER-модель

@startuml

entity User  {
+ id : Int
+ email : Text
+ password : Text
+ roleId : Int
  }

entity Role  {
+ id : Int
+ name : Text
+ description : Text
  }

entity "Permision has role" as PermHasRole  {
+ permisionId : Int
+ roleName : Text
  }

entity Permision  {
+ id : Int
+ name : Text
  }

entity "Public request" as PubRequest  {
+ name : Text
+ date : Text
  }

entity "Media data" as MediaData  {
+ id : Int
+ name : Text
+ fileType: Text
  }

entity Action  {
+ id : Int
+ name : Text
+ description : Text
  }

object Guest
object RegisteredUser
object Editor
object Admin

object AccountManage
object DataManage
object SearchManage
object SupportManage

Guest .up.> Role
RegisteredUser .up.> Role
Editor .up.> Role
Admin .up.> Role

AccountManage .up.> Action
DataManage .up.> Action
SearchManage .up.> Action
SupportManage .up.> Action

Permision "1.1" -- "0.*" PermHasRole
PermHasRole "0.*" -- "1.1" Role
Role "1.1" -- "0.*" User

MediaData "0.*" -- "1.1" PubRequest
PubRequest "0.*" -- "1.1" Action

Action "0.*" -- "1.1" User

@enduml


