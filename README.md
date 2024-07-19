Blah

```plantUML
@startuml obc_sos_dependencies

skinparam DefaultTextAlignment center
skinparam ComponentStyle rectangle  '

left to right direction

title OBC / SOS integration task dependencies

package "TTC implementation - VCDH-253" {
    [TTC Development] as OBC_TTC_dev
    [TTC testing] as OBC_TTC_test
    [TTC integration] as OBC_TTC_integ

    OBC_TTC_dev --> OBC_TTC_test
    OBC_TTC_test --> OBC_TTC_integ
}

package "X-band downlink - VCDH-108" {
    [XDL implementation] as OBC_XDL_impl
    [XDL testing] as OBC_XDL_test
    [XDL integration] as OBC_XDL_integ

    OBC_XDL_impl --> OBC_XDL_test
    OBC_XDL_test --> OBC_XDL_integ
}

[Define Satlog filtering\ninterface] as OBC_Satlog_filter_design
[Implement Satlog\nfiltering] as OBC_Satlog_filter_impl
OBC_Satlog_filter_design --> OBC_Satlog_filter_impl

[Satlog over S-Band\n implementation]
[Control XDL over TTC] as OBC_XDL_over_TTC

OBC_TTC_integ --> OBC_XDL_over_TTC
OBC_XDL_integ --> OBC_XDL_over_TTC
OBC_TTC_integ --> OBC_Satlog_filter_design

[XLinkS control]<<SOS>> as SOS_xlinks_control
[Satlog extraction] as SOS_satlog_extraction
[XDL unpacking] as SOS_XDL_unpacking

OBC_Satlog_filter_design --> SOS_XDL_unpacking
OBC_XDL_integ --> SOS_XDL_unpacking
OBC_Satlog_filter_impl --> SOS_satlog_extraction

@enduml

```
