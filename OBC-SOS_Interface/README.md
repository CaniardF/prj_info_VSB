```plantUML
@startuml obc_sos_dependencies

skinparam DefaultTextAlignment center
skinparam ComponentBackgroundColor<<done>> GreenYellow
skinparam ComponentBackgroundColor<<ongoing>> LightSkyBlue
skinparam ComponentBackgroundColor<<todo>> LemonChiffon

left to right direction

title OBC / SOS integration task dependencies

package "OBC side" {
    frame "TTC implementation - VCDH-253" {
        [TTC Development]<<done>> as OBC_TTC_dev
        [TTC testing]<<done>> as OBC_TTC_test
        [TTC integration]<<ongoing>> as OBC_TTC_integ

        OBC_TTC_dev --> OBC_TTC_test
        OBC_TTC_test --> OBC_TTC_integ
    }

    frame "X-band downlink - VCDH-108" {
        [XDL implementation]<<done>> as OBC_XDL_impl
        [XDL testing]<<done>> as OBC_XDL_test
        [XDL integration]<<ongoing>> as OBC_XDL_integ

        OBC_XDL_impl --> OBC_XDL_test
        OBC_XDL_test --> OBC_XDL_integ
    }

    [Define Satlog filtering\ninterface]<<todo>> as OBC_Satlog_filter_design
    [Implement Satlog\nfiltering]<<todo>> as OBC_Satlog_filter_impl
    OBC_Satlog_filter_design -> OBC_Satlog_filter_impl

    [Satlog over S-Band\n implementation]<<todo>> as OBC_Satlog_sband
    [Control XDL over TTC]<<todo>> as OBC_XDL_over_TTC

    OBC_TTC_integ --> OBC_XDL_over_TTC
    OBC_XDL_integ --> OBC_XDL_over_TTC
    OBC_TTC_integ --> OBC_Satlog_filter_design
}

package "SOS side" {
    [XLinkS control]<<todo>> as SOS_xlinks_control
    [Satlog extraction]<<todo>> as SOS_satlog_extraction
    [XDL unpacking]<<todo>> as SOS_XDL_unpacking
}

OBC_Satlog_filter_design --> SOS_XDL_unpacking
OBC_XDL_integ --> SOS_XDL_unpacking
OBC_Satlog_filter_impl --> SOS_satlog_extraction

@enduml

```
