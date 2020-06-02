---
title: SAML
---

## Metadata URL

The SAML metadata URL is available at `https://<your Pactflow host>/auth/saml/metadata`.

## Configuring Azure Active Directory

### Create a non gallery application

* Follow the [Microsoft documentation](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/add-non-gallery-app) for creating a non gallery application.
  * Choose `Non-gallery application` at the `Add your own app` screen.
  * Set the name to `Pactflow On-Premesis` when prompted.

* When the application has been created, assign the users that should be allowed to login to Pactflow.

* Once the users have been assigned, select the `Single sign-on` tab. Select `SAML`.
  * Unfortunately, the metadata format provided by the SAML library that Pactflow uses is not accepted by Azure AD, so manual configuration is required.

* Set the Identifier (Entity ID) to `https://pactflow.<your company domain>` eg. `https://pactflow.mycompany.com`. This field must match the [PACTFLOW_SAML_ISSUER](/docs/on-premises/environment-variables/#pactflow_saml_issuer) environment variable.

* Set the Reply URL to `https://<your Pactflow host>/auth/saml/callback`

* Leave the Sign On URL, Relay State and Logout Url fields blank.

### Configure the Pactflow environment variables

You can find a template for the required environment variables [here](/docs/on-premises/environment-variables/templates#azure-active-directory).

* Set the [PACTFLOW_SAML_ISSUER](/docs/on-premises/environment-variables/#pactflow_saml_issuer) to the `Identifier (Entity ID)`.
* Set the [PACTFLOW_SAML_IDP_SSO_TARGET_URL](/docs/on-premises/environment-variables/#pactflow_saml_idp_sso_target_url) to the `Login URL`.
* Set the [PACTFLOW_SAML_IDP_ENTITY_ID](/docs/on-premises/environment-variables/#pactflow_saml_idp_entity_id) to the `Azure AD Identifier`
* Set the [PACTFLOW_SAML_IDP_CERT_FINGERPRINT](/docs/on-premises/environment-variables/#pactflow_saml_idp_cert_fingerprint) to the `Thumbprint`
* Set the [PACTFLOW_SAML_IDP_NAME](/docs/on-premises/environment-variables/#pactflow_saml_idp_name) to your choice - this is a display name for the login button.
* Set the identifier, email and name attributes as per the [template](/docs/on-premises/environment-variables/templates#azure-active-directory).