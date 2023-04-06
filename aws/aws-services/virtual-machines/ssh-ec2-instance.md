---
description: Connect an EC2 instance with SSH by Session ID or by downloading a key
---

# Connect EC2 instance

Once an EC2 Instance is created, you connect it with SSH either by using Session ID or by downloading a key.

In the DuploCloud Portal, navigate to **DevOps** --> **Hosts** and select the host to which you want to connect.

## SSH EC2 Linux instance

### SSH using session id

After you select the Host, on the Host's page click the **Actions** menu and select **SSH**. A new browser tab opens and you can connect your Host using SSH with by session ID. Connection to the host launches in a new browser tab.

<figure><img src="../../../.gitbook/assets/SSH1.png" alt=""><figcaption><p>Host page with <strong>Actions</strong> menu and <strong>SSH</strong> option</p></figcaption></figure>

### &#x20;SSH by downloading key

1. After you select the Host, on the Host's page click the **Actions** menu and select **Connection Details**. The **Connection Info for Host** window opens. Follow the instructions to connect to the server.
2. Click **Download Key**.



![Connection Info for Host window with Download Key button](<../../../.gitbook/assets/image (1) (1) (2).png>)



#### Disable the option to download the SSH key

If you don't want to display the Download Key button, disable the button's visibility.

1. In the DuploCloud Portal, navigate to **Administrator** -> **System Settings**.
2. Click the **System Config** tab.
3. Click **Add**. The **Add Config** pane displays.
4. From the **Config Type** list box, select **Flags**.
5. From the **Key** list box, select **Disable SSH Key Download**.
6. From the **Value** list box, select **true**.
7. Click **Submit**.

<figure><img src="../../../.gitbook/assets/image (2) (6).png" alt=""><figcaption><p><strong>Add Config</strong> pane with <strong>Disable SSH Key Download Key</strong> selected</p></figcaption></figure>

### Powershell EC2 Windows instance

