---
title: CVE-API
description: 
published: true
date: 2021-05-15T15:58:53.884Z
tags: mongodb, javascript, github, cve, nodejs, vuejs, express.js, bash, scripting
editor: markdown
dateCreated: 2020-06-07T16:02:40.269Z
---

> This Project is not maintained and still 'Under Development'.
> Any ideas or feedback are welcome.
{.is-danger}


CVE-API is my own custom API made with the data from:
https://cve.mitre.org/

**CVE.mitre** uses a public github repo which stores all vulnerabilities in json format. [Github Repo](https://github.com/CVEProject/cvelist).

As of writing ((07/06/2020) i have over **140k documents** in the DB).

# Overview

~~Website: https://api-cve.now.sh~~

**I have this project running inside docker.**
Website: https://cve.parkhost.eu
`process is still the same it only runs on my own hardware instead of free tier which goes to sleep at inactivity and takes ages to boot up.`

- Source = [cve.mitre - Github repo](https://github.com/CVEProject/cvelist)
- DB = MongoDB - [MongoDB](Mongodb.com) -> Docker
- API = NodeJS - Express -> Docker
- Front = NodeJS - Vuejs -> Docker



> The most of the ***mongo*** commands are further explained [here](/MongoDB) in my mongodb section.
{.is-info}

```diagram
PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3NzZweCIgaGVpZ2h0PSI0NTFweCIgdmlld0JveD0iLTAuNSAtMC41IDc3NiA0NTEiIGNvbnRlbnQ9IiZsdDtteGZpbGUgaG9zdD0mcXVvdDtlbWJlZC5kaWFncmFtcy5uZXQmcXVvdDsgbW9kaWZpZWQ9JnF1b3Q7MjAyMC0xMS0yMlQxMTo1MTo0Mi4wODFaJnF1b3Q7IGFnZW50PSZxdW90OzUuMCAoV2luZG93cykmcXVvdDsgZXRhZz0mcXVvdDtFR0Q0RVhSMVpUMW1WNE54dHhWRSZxdW90OyB2ZXJzaW9uPSZxdW90OzEzLjEwLjAmcXVvdDsgdHlwZT0mcXVvdDtlbWJlZCZxdW90OyZndDsmbHQ7ZGlhZ3JhbSBpZD0mcXVvdDtWWnJtbzMxZURWZ2txYVplRnRrRyZxdW90OyBuYW1lPSZxdW90O1BhZ2UtMSZxdW90OyZndDs3WmhiYjVzd0ZJQi9UYVQxWVJPWFFOUEgzTnB0V3JkSTBiYjJrWUlMWGdsbXhpUmt2MzdIWUFNR3NtUVpTRkcxUENUMnNYMDRseStIQXlOenZzbnVxQk1IOThSRDRjalF2R3hrTGthR29SdUdCajljc2hjUzNiSUxpVSt4SjJTVllJMS9JU0VVQi8wVWV5aFJOakpDUW9aalZlaVNLRUl1VTJRT3BXU25ibnNtb1hyVjJQRlJTN0IybmJBdC9ZNDlGaFRTaWFWVjh2Y0krNEc4c3E2SmxZMGpOd3RCRWpnZTJkVkU1bkpremlraHJCaHRzamtLZWZSa1hJcHp0d2RXUzhNb2l0Z3BCNHppd05ZSlUrR2JzSXZ0cGJOZ1lzeUg3ajdFa1llb09USm51d0F6dEk0ZGx5L3NJTXNnQzlnbWhKa093eWVTd2s3djAxTXBjTndYbjNMcGw1U0JHaVRrU1pGYTNZSngyM1RoelJaUmhyS2FTTGh5aDhnR01icUhMV0xWRmxFVlhGbVNsMTJWSkxrbHFPVm5JbVNPd01JdkZWZVJnNEVJWG5jZ3plT0JQQkkwSjRrTFZwOXhocngrQW1LcEFURzBka0FtQXdWa2ZKRUJNU2ZXVVVTR2lvaDFrUkc1MW83L2FZYUtpSDA4SWlqeXByeGk4d0lVT2ttQ1hUVWtLTVBzQWNiYU8wdk1IbXNyQys2a0ppZDdPWW5BenRvaFBuMnNyMVhIOHBseWJvVW9Ca2NSRmNLRVVmS0M1aVFrTkxmWXZNMC9mMHBPUWxMcUlxVnVNSWY2aUNrMUdYbktUYWlkd0ZxQ3JJNEVTUmxGb2NQd1ZyMTFkV1ZOWEdGRk1OaGI4cUdiQjJxSVZGRjRJMDdWYnpWTlJSTlZrVzQxRkJVeGFDbktJU3JkUG9tcjZ4NjRLaGxSQ0ttQU9jRElHVGpVY3orK3JOekxJN0kyTkZOMmF1Nmh5cWlLek1GeVB6a3o5d21Zd0FaQlFwWW92VmFncW5MVlhhTCtzYXFNMjJSWkYwV1cxU2dHMXMyWlpObU44bVNOQnlQcnBvTXNPMlM4dllXQnovTGtGSUpua3R0WU1XZi9USWxjZUZ0MHZWUFlvSS9qckZxVVd1NHdDMUxRcWMyL0xlSDdSMElpcVJoc0xIU3Ixd054ellZRzd0QUlNSlZraXNBRTV5bmZ3R2x6VWtaa0s4Nm5JZllqL2k4QXhQaDlic2E3Q1F5UFAxT3hzTUdleHcvUFloN1dQTkRXYkdRdHVJTTREQ1cyRWVHTmZvTmxJYVRGSTRJd2dQdjBWN0NmM3Q4WWFzT25YN2ZibS9JV1Z3ZmQ2S0cva2EzVThNak0wNFNSRFN6Zms4Z25pOWwvWG5yaXhlNTRaTkxIUS9HaUgrUkY0T0dXVGxjRVNQZGJVQXpOMmpLTGdZd0VSdFBWQi9oKzg1bDQ2T1A2cXJ3dTdlRHVPSTRIdHI0U1NudkMxTlNQYzFveTJUdW5YYStOaXJSNWVIcytXUU1CZTB0aDE0cS8wd05Hdno1Y25VZGo3dGtyZzdFZkZ1MUdNOWRaTTN0aUVhYlYyOUdpaWF0ZU1wdkwzdz09Jmx0Oy9kaWFncmFtJmd0OyZsdDsvbXhmaWxlJmd0OyI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gMzUgMzU1IEMgMzUgMzQ2LjcyIDQ4LjQzIDM0MCA2NSAzNDAgQyA3Mi45NiAzNDAgODAuNTkgMzQxLjU4IDg2LjIxIDM0NC4zOSBDIDkxLjg0IDM0Ny4yMSA5NSAzNTEuMDIgOTUgMzU1IEwgOTUgNDA1IEMgOTUgNDEzLjI4IDgxLjU3IDQyMCA2NSA0MjAgQyA0OC40MyA0MjAgMzUgNDEzLjI4IDM1IDQwNSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gOTUgMzU1IEMgOTUgMzYzLjI4IDgxLjU3IDM3MCA2NSAzNzAgQyA0OC40MyAzNzAgMzUgMzYzLjI4IDM1IDM1NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyNSIgeT0iMzAiIHdpZHRoPSI4MCIgaGVpZ2h0PSI4MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzYwIiB5PSIzNDAiIHdpZHRoPSI4MCIgaGVpZ2h0PSI4MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNjc1IiB5PSIzNDAiIHdpZHRoPSI4MCIgaGVpZ2h0PSI4MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA2NSAxMTAgTCA2NSAzMzMuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2ZmZmZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NSAzMzguODggTCA2MS41IDMzMS44OCBMIDY1IDMzMy42MyBMIDY4LjUgMzMxLjg4IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iI2ZmZmZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA5NiAzODAgTCAzNTMuNjMgMzgwIiBmaWxsPSJub25lIiBzdHJva2U9IiNmZmZmZmYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzU4Ljg4IDM4MCBMIDM1MS44OCAzODMuNSBMIDM1My42MyAzODAgTCAzNTEuODggMzc2LjUgWiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjZmZmZmZmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ0Ni4zNyAzODAgTCA2NjguNjMgMzgwIiBmaWxsPSJub25lIiBzdHJva2U9IiNmZmZmZmYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDQxLjEyIDM4MCBMIDQ0OC4xMiAzNzYuNSBMIDQ0Ni4zNyAzODAgTCA0NDguMTIgMzgzLjUgWiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjZmZmZmZmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY3My44OCAzODAgTCA2NjYuODggMzgzLjUgTCA2NjguNjMgMzgwIEwgNjY2Ljg4IDM3Ni41IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iI2ZmZmZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjEzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMHB4OyBtYXJnaW4tbGVmdDogNjVweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj48Yj48Zm9udCBzdHlsZT0iZm9udC1zaXplOiAxNHB4Ij5HaXRodWIgQ1ZFIGpzb248L2ZvbnQ+PC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSI2NSIgeT0iMTQiIGZpbGw9IiNGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc2l6ZT0iMTJweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+R2l0aHViIENWRSBqc29uPC90ZXh0Pjwvc3dpdGNoPjwvZz48cmVjdCB4PSIwIiB5PSI0MzAiIHdpZHRoPSIxNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDQwcHg7IG1hcmdpbi1sZWZ0OiA3MHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxiPjxmb250IHN0eWxlPSJmb250LXNpemU6IDE0cHgiPkN1c3RvbSBNb25nb0RCPC9mb250PjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iNzAiIHk9IjQ0NCIgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkhlbHZldGljYSIgZm9udC1zaXplPSIxMnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5DdXN0b20gTW9uZ29EQjwvdGV4dD48L3N3aXRjaD48L2c+PHJlY3QgeD0iMjkwIiB5PSI0MzAiIHdpZHRoPSIyMjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDQwcHg7IG1hcmdpbi1sZWZ0OiA0MDBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PGZvbnQgY29sb3I9IiNGRkZGRkYiPjxiPjxmb250IHN0eWxlPSJmb250LXNpemU6IDE0cHgiPkN1c3RvbSBFeHByZXNzIEFQSSAoTm9kZUpTKTxiciAvPjwvZm9udD48L2I+PC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSI0MDAiIHk9IjQ0NCIgZmlsbD0iI0ZGRkZGRkYiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc2l6ZT0iMTJweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+Q3VzdG9tIEV4cHJlc3MgQVBJIChOb2RlSlMpJiN4YTs8L3RleHQ+PC9zd2l0Y2g+PC9nPjxyZWN0IHg9IjY1NSIgeT0iNDMwIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ0MHB4OyBtYXJnaW4tbGVmdDogNzE1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PGRpdiBzdHlsZT0iZm9udC1zaXplOiAxNHB4Ij48Yj48Zm9udCBzdHlsZT0iZm9udC1zaXplOiAxNHB4Ij5Gcm9udFBhZ2UgKFVYKTwvZm9udD48L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjcxNSIgeT0iNDQ0IiBmaWxsPSIjRkZGRkZGIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXNpemU9IjEycHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPkZyb250UGFnZSAoVVgpPC90ZXh0Pjwvc3dpdGNoPjwvZz48L2c+PHN3aXRjaD48ZyByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiLz48YSB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLC01KSIgeGxpbms6aHJlZj0iaHR0cHM6Ly9kZXNrLmRyYXcuaW8vc3VwcG9ydC9zb2x1dGlvbnMvYXJ0aWNsZXMvMTYwMDAwNDI0ODciIHRhcmdldD0iX2JsYW5rIj48dGV4dCB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEwcHgiIHg9IjUwJSIgeT0iMTAwJSI+Vmlld2VyIGRvZXMgbm90IHN1cHBvcnQgZnVsbCBTVkcgMS4xPC90ZXh0PjwvYT48L3N3aXRjaD48L3N2Zz4=
```

# Scripts
These are some scripts i use to maintain the database.

---
## Import all json files into mongodb
This will import all CVE files into the database
Is needed to run the first time and fill up the database.
It can take up to 45 minutes to import all documents.


### Bash:
```bash

#!/bin/bash
#Imports all json CVE files into MONGODB

# FILES=find /path/to/cvelist/ -type f -name "*.json"

for f in `find /path/to/cvelist -type f -name "*.json"`
do
        echo "Processing $f file..."
        mongoimport --db testdb --collection CVE --file /path/to/cvelist/$f

```
---
### Powershell (will only import everything from the year 2020):
```powershell
$files = gci '$env:SystemDrive\path\to\cvelist\' -Name *.json -Depth 99

write-host 'starting import'
foreach($f in $files) {
    mongoimport --db testdb --collection CVE --file "$env:SystemDrive\path\to\cvelist\2020\$($f)"
}

```
---
## MongoDB sync import
This will get all files that are new/changed and stores them in a .dat file with the current date + time:

> ***Todo:***
> - [ ] If no changes detected skip the process
> - [ ] If reserved CVE added skipt the process

----

```bash

#!/bin/bash
#GET ALL CHANGED FILE NAMES

cd /cd/into/your/git_repo && git fetch

CURRENTSHA="$(git rev-parse HEAD)"
NEWSHA="$(git rev-parse FETCH_HEAD)"

FILES="$(git diff --name-only ${CURRENTSHA} ${NEWSHA})"
FILENAME=/path/to/data/_"$(date +%Y%m%d%H%M)".dat

## saves the git diff (FILES) into file (FILENAME)
printf "$FILES" > "$FILENAME"

## Should be only 1 file living in this directory
## After the import the file is moved to 'archive'
DAT=`find /path/to/.dat/file*.dat`

values=`cat $DAT`

cd /path/to/cvelist && git pull

# Foreach json in the .dat file import it to mongodb
for v in $values
do
        echo "Processing $v file..."
        mongoimport --host localhost --collection CVE --upsertFields CVE_data_meta.ID  /path/to/cvelist/$v

done

# Move the .dat to archive
mv $DAT /path/to/archive/

```

-----

## Shows changes since last git pull

```bash
#!/bin/bash
#GET ALL CHANGED FILE NAMES

git fetch

CURRENTSHA="$(git rev-parse HEAD)"
NEWSHA="$(git rev-parse FETCH_HEAD)"

FILES="$(git diff --name-only ${CURRENTSHA} ${NEWSHA})"

echo "${FILES}"
echo "${FILES}" | wc -l

```

## Cleanup Reserved CVE's

```bash
# Select databse
use <DatabaseName>

# Show the amount of documents found
db.<collection_name>.find({"CVE_data_meta.STATE": "RESERVED"}).count()

# Delete all documents at once
db.<collection_name>.deleteMany({{"CVE_data_meta.STATE": "RESERVED"}})
## result:
## { "acknowledged" : true, "deletedCount" : 96XX }
```

# PowerShell Script
This will get all your installed application on a Windows system and sends it to the API.
The API will filter the incoming (JSON) request so it will split into `[ApplicationName] Version`

> This is my test script, it will redirect to localhost -_-'
{.is-warning}

```powershell
$URL = 'http://localhost:3000/input'

$Apps = Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*, HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select DisplayName, DisplayVersion, PSChildName
$json = [PSCustomObject][Ordered]@{ }

$more = @'
[
    {
        "ProductName":  "7-Zip 19.00 (x64)",
        "Version":  "19.00"
    },
    {
        "ProductName": "Microsoft Visual C++ 2013 Redistributable (x86) ",
        "Version":  "12.0.30501.0"
    },
    {
        "ProductName":  "Microsoft Exchange Server 2019",
        "Version":  "update"
    }
]
'@

$json = foreach ($App in $Apps) {
  if ($App.DisplayName -ne $null) {
    [ordered]@{ProductName = "$($App.DisplayName)"
      Version              = "$($App.DisplayVersion)"
    }
  }
  else {
    [ordered]@{ PSChild = "$($App.PSChildName)" 
      Version           = "$($App.DisplayVersion)"
    }
  }
}

$jsontest = @'
[
    {
        "ProductName": "Steam ",
        "Version":  "2.10.91.91"
    }
]
'@

$jsontestmessage = $jsontest

$jsonmessage = ConvertTo-Json $json -Depth 100



$parameters = @{
  "URI"         = $URL
  "Method"      = 'POST'
  "Body"        = $jsontestmessage
  "ContentType" = 'application/json'
}
 
Invoke-RestMethod @parameters


```
  
  

# Ideas
- [x] Backend with FeatherJS (1 apr 2021)
	- [x] Mongoose as DB connection
- [ ] Update Front-end to VUE 3
	- [ ] Better/multiple search options 
- [x] Automation Scripts to check windows 10
- [ ] Script to check Windows Server (Roles)
- [ ] Linux applications (mostly server based)
- [ ] Mail option

----

