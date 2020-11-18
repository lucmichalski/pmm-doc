```plantuml
@startuml "pmm-client"
!include https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Component.puml
LAYOUT_TOP_DOWN()

System_Boundary(customer_system, "Customer_System") {
Person(user, "User")
SystemDb_Ext(database, "Database")

System_Boundary(pmm_client,"PMM Client") {
    Component(pmm_agent, "pmm-agent", "golang")
    Component(pmm_admin, "pmm-admin", "golang")

    System_Boundary(exporters, "Exporters"){
        Component(exporter1, "node_exporter","golang")
        Component(exporter2, "mysqld_exporter","golang")
        Component(exporter3, "mongodb_exporter","golang")
        Component(exporter4, "postgres_exporter","golang")
        Component(exporter5, "proxysql_exporter","golang")
        Component(exporter6, "rds_exporter","golang")
    }
}
Rel_R(user, pmm_admin, "Configure")
Rel_L(pmm_agent, pmm_admin, "")
Rel_R(pmm_admin, pmm_agent, "")
Rel_L(pmm_agent, exporters,"")
Rel_R(exporters, pmm_agent, "")
Rel(database, exporters, "")
}
@enduml
```
