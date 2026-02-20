## NRTS taxonomy v1

```mermaid

flowchart LR

    subgraph API-used["NetBox API Endpoints Used (6)"]
        API3[api-dcim]
        API4[api-extras]
        API5[api-ipam]
        API7[api-status]
        API8[api-tenancy]
        API9[api-users]
    end

    subgraph dcim["DCIM (19)"]
        D1[cable-terminations]
        D2[cables]
        D3[device-bays]
        D4[device-roles]
        D5[device-types]
        D6[devices]
        D7[interfaces]
        D8[locations]
        D9[manufacturers]
        D10[rack-types]
        D11[racks]
        D12[regions]
        D13[site-groups]
        D14[sites]
    end


    subgraph dcim-sites
        D14-1[region]
        D14-2[group]
        D14-3[name]
        D14-4[slug]
        D14-5[status]
        D14-6[cf_Road]
        D14-7[cf_Marker_Post]
        D14-8[cf_CW]
        D14-9[cf_MP_Offset]
        D14-10[cf_Hardshoulder]
        D14-11[cf_Span]
        D14-12[cf_SPC]
        D14-13[latitude]
        D14-14[longitude]
        D14-15[owner]
        D14-16[physical_address]
        D14-17[cf_NRTS_ID]
        D14-18[cf_TAF]
        D14-19[cf_NL_UID]
    end


