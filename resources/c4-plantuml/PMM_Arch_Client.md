```plantuml
@startuml "pmm-client"
!include https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Component.puml
LAYOUT_LEFT_RIGHT()

Person(administrator, "Administrator")

System_Boundary(customer_system, "Customer System") {
    SystemDb_Ext(database, "Database")
    System_Ext(application, "Application")

    System_Boundary(pmm_client,"PMM Client") {
        Component(pmm_agent, "pmm-agent", "golang")
        Component(pmm_admin, "pmm-admin", "golang")

        System_Boundary(exporters, "Exporters"){

        }
    }
}

Rel(database, exporters, " ")
Rel(exporters, pmm_agent, " ")

Rel_L(application, database, " ")
Rel_R(database, application, " ")

@enduml
```
