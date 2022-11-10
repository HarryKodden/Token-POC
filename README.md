# Provisioning Flow

<!---
@startuml assets/ResearchCloud

title "ResearchCloud Provisioning Services"

actor user
participant SRC as "ResearchCloud"
participant SRAM

group Authenticate ResearchCloud
user -> SRC: Logon to "ResearchCloud"
user <- SRC: Redirect to SRAM
user -> SRAM: Authenticate
SRC <- SRAM: Access Token (SRC)
end

group Connect to Service ...
user -> SRC: Connect with a service...
SRC -> SRAM: GET /api/services/mine
SRC <- SRAM: Response with all services available to user
user <- SRC: Show services
user -> SRC: Select service **XYZ**
SRC -> SRAM: **/oidc/device_authorization**\nclient_id=XYZ\nscope=openid+offline_access
SRC <- SRAM: device_code="xxx"\nverification_link=https://...
user <- SRC: Present verification link to user
SRC -> SRAM: **/oidc/token**\ngrant_type=device_token\ndevice_code="xxx"
SRC <- SRAM: pending...
user -> SRAM: click verification link
user <- SRAM: Authenticate + Consent
user -> SRAM: Accepted !
SRC -> SRAM: **/oidc/token**\ngrant_type=device_token\ndevice_code="xxx"

SRC <- SRAM: id_token="iii"\naccess_token="aaa"\nrefresh_token="rrr"
group repeatable...
SRC -> SRAM: **/oidc/token**\ngrant_type=refresh_token\nrefresh_token="rrr"
SRC <- SRAM: id_token="iii"\naccess_token="aaa"\nrefresh_token="rrr"
end
end

group Provision/Refresh workspace connected to XYZ
SRC -> XYZ: Provision service\npass access_token "aaa"
end

group XYZ
user -> XYZ: User connects to service...
XYZ -> SRAM: **/oidc/userinfo**\naccess_token="aaa"
XYZ <- SRAM: user details
end

@enduml
-->

![ResearchCloud](assets/ResearchCloud.svg)

## Note for contribution

Please update diagram before commit & push to repostitory:

```shell
plantuml -tsvg README.md
```
