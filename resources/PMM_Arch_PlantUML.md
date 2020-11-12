```plantuml format="png" classes="uml myDiagram"

@startuml "bigbankplc"
!includeurl https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master/C4_Container.puml
' uncomment the following line and comment the first to use locally
' !include C4_Container.puml

skinparam wrapWidth 200
skinparam maxMessageSize 200

LAYOUT_TOP_DOWN
'LAYOUT_AS_SKETCH
'LAYOUT_WITH_LEGEND

Person(customer, User, "PMM user")
Container(client, "PMM Client", "tech", "desc")
Container(server, "PMM Server", "tech", "desc")
Container(platform, "Percona Platform", "tech", "")
ContainerDb(database, "Database","","")
Container(application,"Customer Application","","")

Rel(customer, client, "Uses", "HTTPS")
Rel(customer, server, "Uses", "HTTPS")

Rel_R(client, server, "Uses", "HTTPS")
Rel_R(server, platform, "Uses", "HTTPS")

Rel(client, database,"","")
Rel_R(database, application,"","")

@enduml
```
