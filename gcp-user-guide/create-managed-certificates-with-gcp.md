# Create Managed Certificates with GCP

Create SSL/TLS certificates to secure your applications in GCP Managed Certificates. You can then import your certificates to use with your DuploCloud Services.&#x20;

1. **Open Google Cloud Console**: Visit the Google Cloud Console at [https://console.cloud.google.com/](https://console.cloud.google.com/).
2. **Select your Project**: If you have multiple projects, select the project where you want to create the Managed Certificate from the project dropdown menu in the top left corner.
3. **Navigate to "Security"**: On the left sidebar, click on "Security" to expand the menu.
4. **Select "SSL certificates"**: Under the "Security" menu, click on "SSL certificates". This will open the SSL certificates management page.
5. **Click on "Create Certificate"**: On the SSL certificates management page, click on the "Create certificate" button.
6. **Fill in Certificate Details**:
   * **Certificate Name**: Enter a name for your certificate.
   * **Domains**: Enter the domain names for which you want to create the certificate. You can enter multiple domain names separated by commas.
   * **Managed by**: Choose whether you want to manage the certificate with Google-managed certificates or external certificates.
   * **Certificate Authority**: If you choose to manage the certificate with Google-managed certificates, select the certificate authority you want to use.
7. **Review and Create**: After filling in the details, review the information to ensure it's correct. Then, click on the "Create" button to create the Managed Certificate.
8. **Verification**: If you're using Google-managed certificates, Google Cloud Platform will automatically verify ownership of the domains you provided during the creation process. This verification process may take some time.
9. **View Certificate Details**: Once the certificate is created and verified, you can view its details, including the expiration date, status, and associated domains, on the SSL certificates management page.
