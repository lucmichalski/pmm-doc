## PMM in context

Percona Monitoring and Management (PMM) comprises:

- PMM Client
- PMM Server
- Percona Platform

```plantuml
@startuml "pmm-basic-context"
!includeurl https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Context.puml
LAYOUT_WITH_LEGEND()

Person_Ext(user, "User")
System_Ext(database, "Monitored System")
Boundary(pmm, "PMM") {
    System(server, "PMM Server")
    System(client, "PMM Client")
}
Boundary(platform, "Percona Platform") {
    System(security_threat_tool, "Security Threat Tool")
    System(dbaas, "DBaaS")
}
Rel(user, client, "Configure")
Rel(user, server, "Monitor")
Rel_R(database, client, " ")
Rel_R(client, server, " ")
Rel_L(server, client, " ")
Rel_R(server, platform, " ")
@enduml
```

## PMM Client

```plantuml
@startuml "pmm-client"
!includeurl https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Container.puml
LAYOUT_WITH_LEGEND()
'LAYOUT_TOP_DOWN()
LAYOUT_LEFT_RIGHT()

Person_Ext(user, "User")
Boundary(server, "PMM Server")
Boundary(external_system, "Monitored System") {
    SystemDb_Ext(database, "Database")
}
Boundary(client, "PMM Client") {
    Boundary(exporters, "Exporters"){
        System(exporter, "Exporter")
    }
    System(pmm_admin, "pmm-admin")
    System(pmm_agent, "pmm-agent")
    System(vmagent, "vmagent", "VictoriaMetrics")
}
Rel(user, pmm_admin, "Configure")
Rel(database, exporter, " ")
Rel(database, pmm_agent, " ")
Rel(pmm_admin, server, " ")
Rel(pmm_agent, server, " ")
Rel(vmagent, server, "'Push' metrics")
Rel(exporter, vmagent, " ")
Rel(exporter, server, "'Pull' metrics")
@enduml
```

## PMM Server

```plantuml
@startuml "pmm-server"
!includeurl https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Component.puml
LAYOUT_WITH_LEGEND()
LAYOUT_LEFT_RIGHT()

Person_Ext(user, "User")
Boundary(client, "PMM Client")

System_Boundary(server, "PMM Server") {
        System(qan, "Query Analytics")
        System(grafana, "Grafana")
        SystemDb(postgresql, "PostgreSQL")
        SystemDb(victoria_metrics, "Victoria Metrics")
        System(pmm_managed, "pmm-managed")
    }

Rel(client, victoria_metrics, " ")

Rel(user, grafana, " ")
Rel(grafana, pmm_managed, " ")
Rel(qan, pmm_managed, " ")
Rel(victoria_metrics, pmm_managed, " ")
Rel(postgresql, pmm_managed, " ")
Rel_R(client, pmm_managed, " ")

@enduml
```


## Exporters TODO

```plantuml
@startuml "pmm-exporters"
!includeurl https://raw.githubusercontent.com/stawirej/C4-PlantUML/master/C4_Component.puml
LAYOUT_LEFT_RIGHT()


System_Boundary(monitored, "Monitored Services") {
    ComponentDb(mysql, "MySQL", "")

}
System_Boundary(exporters, "Exporters") {
    Component(mysqld_exporter, "mysqld_exporter", "")

}

Rel(mysql, mysqld_exporter, "")


@enduml
```
