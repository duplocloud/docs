# BYOH

## Introduction <a href="#0-toc-title" id="0-toc-title"></a>

If you have a host already running somewhere in the cloud or on-premise, you can bring that to DuploCloud using BYOH functionality and let DuploCloud manage the host, let it be running the containers or installing the compliance agents.

## Add new BYO host <a href="#1-toc-title" id="1-toc-title"></a>

To configure BYOH go to **Deployments > Hosts > BYO-HOSTS**. Click on **add** and provide the name, IP Address and in the Fleet type select Native App (if you don’t, DuploCloud will not manage the containers but manage the compliance agents on the host), provide the username, password/Private key file. Make sure SSH access to the host is opened to access from DuploCloud.

![](<../.gitbook/assets/Screen Shot 2022-06-24 at 4.17.53 PM.png>)

## Confirm server agent status <a href="#2-toc-title" id="2-toc-title"></a>

Within about 5 minutes of adding the host, you can go to **Security > Agents >** and see that the agent on host is in Active state.
