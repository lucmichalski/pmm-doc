```plantuml
@startuml "pmm-context1"
!includeurl https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Context.puml
'LAYOUT_WITH_LEGEND()

System_Boundary(pmm,"Percona Monitoring and Management") {
    System(client, "PMM Client")
    System(server, "PMM Server")
    System(platform,"Percona Platform")
}
Rel_R(client, server, "")
Rel_L(server, client, "")
Rel_R(server, platform,"")
Rel_L(platform, server,"")
@enduml
```


```plantuml
@startuml "pmm-context2"
!includeurl https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Context.puml
'LAYOUT_WITH_LEGEND()

Enterprise_Boundary(customer,"Customer System") {
    System(client, "PMM Client")
    SystemDb_Ext(database, "Database")
'    System_Ext(application, "Application")
}
'Rel_L(client, database, "Monitors")
'Rel_L(application, database, "")
@enduml
```
