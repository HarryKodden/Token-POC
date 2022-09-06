# README

Introduction

<!--
@startuml assets/ResearchCloud

title "ResearchCloud Provisioning Services"

actor user
participant SRC as "ResearchCloud"
participant SRAM

group Authenticate ResearchCloud
user -> SRC: Logon to "ResearchCloud"
user <-- SRC: Redirect to SRAM
user -> SRAM: Authenticate
SRC <-- SRAM: Access Token (SRC)
end

group Obtain Refresh token for Service XYZ
user -> SRC: connect to XYZ
SRC -> SRAM: /oidc/device_authorization client_id=XYZ, scope=openid+offline_access
SRC <-- SRAM: device_code="xxx", verification=https://...
SRC -> SRAM: /oidc/token device_code="xxx"
SRC <-- SRAM: pending...
user -> SRAM: using verification link
user <- SRAM: Authenticate + Consent
user -> SRAM: Accepted !
SRC --> SRAM: /oidc/token grant_type=device_token, device_code="xxx"

SRC <-- SRAM: access_token="aaa", refresh_token="rrr"
group repeatable...
SRC --> SRAM: /oidc/token grant_type=refresh_token, refresh_token="rrr"
SRC <-- SRAM: access_token="aaa", refresh_token="rrr"
end
end

group Provision/Refresh workspace connected to XYZ
SRC -> XYZ: Provision, pass access_token "aaa"
end

group XYZ
user -> XYZ
XYZ -> SRAM: /oidc/userinfo access_token="aaa"
XYZ <-- SRAM: user details
end

@enduml

-->

![ResearchCloud](assets/ResearchCloud.svg)
