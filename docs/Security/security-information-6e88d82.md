<!-- loio6e88d8218f0d4f7693048881c9e07c79 -->

# Security Information

This document is an overview of security-relevant information that applies to Identity Authentication, and contains recommendations about how administrators should secure it.

While this document is intended to support administrators and security responsible specialists to use Identity Authentication in a secure manner, there may be further elements to consider depending on usage, integrations as well as applicable industry or local legal regulations.



<a name="loio6e88d8218f0d4f7693048881c9e07c79__section_dy3_bxm_j1b"/>

## Updates and Notifications

For more information, see [Updates and Notifications](../updates-and-notifications-8e44a7a.md).

For more information, see [Updates and Notifications](https://help.sap.com/viewer/6d6d63354d1242d185ab4830fc04feb1/Cloud/en-US/8e44a7a2bb2241deb6d7f4131aa9494b.html).



## Before You Start

Before you secure Identity Authentication, protect the cloud application that trusts Identity Authentication.For more information about protecting SAP BTP applications, see [Security, Neo Environment](https://help.sap.com/viewer/ea72206b834e4ace9cd834feed6c0e09/Cloud/en-US/3438252775d84bdfa211e79147561c99.html).



<a name="loio6e88d8218f0d4f7693048881c9e07c79__section_xq4_2mx_p5b"/>

## Security Recommendations

SAP BTP Security Recommendations collects information which enables you to secure the configuration and operation of SAP BTP services in your landscape.

For more information, see [Security Recommendations](https://help.sap.com/docs/BTP/c8a9bb59fe624f0981efa0eff2497d7d/531f33def8074ccdb6f1f784a34dafcb.html?sec_checklist=identity%20authentication).



<a name="loio6e88d8218f0d4f7693048881c9e07c79__section_rfg_hfn_j1b"/>

## Communication Protocol

Identity Authentication is fully web browser based application, with all access over HTTPS. Every page of the Identity Authentication application is currently delivered via Transport Layer Security \(TLS\). Access to Identity Authentication is encrypted-in-transit over HTTPS using 256-bit TLS encryption.



## User Administration

Set user permissions in accordance with the scenario you are configuring. For more information, see [Scenarios](../scenarios-fb9898d.md).

You have the following options:

-   For a business-to-consumer scenario, allow *Public* user application access.
-   For a business-to-business scenario, allow *Private* user application access.
-   For a business-to-employee scenario, allow *Internal* user application access.

For more information about the settings for user application access, see [Configure User Access to the Application](../Operation-Guide/configure-user-access-to-the-application-8b147c4.md).

You can also define rules for authentication according to different risk factors. For more information, see [Configure Risk-Based Authentication for an Application](../Operation-Guide/configure-risk-based-authentication-for-an-application-bc52fbf.md#loiobc52fbf3d59447bbb6aa22f80d8b6056).



## User Authentication

Identity Authentication protects your users during authentication in the following ways:

-   With SAML 2.0 or OpenID Connect

    Identity Authentication supports the single sign-on \(SSO\) mechanism. Every user with an account is able to use SSO for the cloud applications that use Identity Authentication.

-   With an application certificate

    The Identity Authentication authentication interfaces that receive REST API calls are protected, since they require an application certificate. Use the certificate when implementing REST APIs for your application. For more information, see the REST API configurations in [Development](../Development/development-55ab9b8.md).




<a name="loio6e88d8218f0d4f7693048881c9e07c79__section_vcg_wrk_25b"/>

## Authorizations

Applications configured in Identity Authentication can manage business user authorizations for applications. For such applications, the *Authorization* tab shows a list of authorization policies created by the application. You can also create custom authorization policies. These authorization policies are stored as user groups. You can assign authorization policies to business users with the admin console, but you can also use a SCIM API.



## Password Security

Identity Authentication does not store plain text passwords in the database, but only their iterated random-salted secure hash values. The random salt is at least 512 bits, and it is different for each password. Only generic hash functions are used with minimum 512 bits key length. No default passwords are delivered, used, or accepted anywhere.

Identity Authentication can use also passwords from on-premise systems for user authentication. These passwords are not stored by Identity Authentication. It sends the user ID and the password for authentication to the on-premise system via the Transport Layer Security \(TLS\) connection. The management of these passwords depends on the integrated on-premise system that supports them, for example Microsoft Active Directory.

Identity Authentication supports three levels of password security. You should use the highest level of security that matches the requirements of your application. The passwords are managed based on password policy rules. For more information, see [Configuring Password Policies](../Operation-Guide/configuring-password-policies-12b3395.md).



## Session Security

Session cookies in Identity Authentication are protected with a Transport Layer Security \(TLS\) and with the *Secure* and *HttpOnly* attributes. You do not need to make any additional configurations for Identity Authentication.



## Network and Communication Security

Identity Authentication is setup in a fenced network, separated from the SAP internal network.

Customer applications run in a shared environment where the business data is isolated from each other, the SAP BTP services uses a shared SAP BTP infrastructure. The internal traffic is controlled by firewalls. SAP administrative access is done via terminal service that requires strong authentication.

All communication channels are protected with TLS, and you should configure the cloud application to use TLS and to check the SAML 2.0 signature.



## Data Storage Security

Data storage security is about how Identity Authentication protects its own database. Data storage security is ensured by the isolated tenant that each customer receives. Only tenant-specific requests can access the tenant's database. These requests are performed by a tenant service, which works with a dependency injection framework and makes sure that all the services, for example the persistence service and the mail service, are injected with the instances dedicated to the given tenant.



## Security-Relevant Logging and Tracing

You can download a CSV file with a history of operations performed by administrators. For more information, see [Export Change Logs with a History of Administration Operations](../Monitoring-and-Reporting/export-change-logs-with-a-history-of-administration-operations-9d96aae.md).

You can retrieve the statistics on the number of user logon request per month. This number is counted on each single authentication managed via Identity Authentication. For more information, see [View Usage Statistics](../Monitoring-and-Reporting/view-usage-statistics-a299d84.md).

**Related Information**  


[Security on SAP Community Network](http://scn.sap.com/community/security)

[SAP Data Center](http://www.sapdatacenter.com/)

[SAP Security Notes](https://support.sap.com/securitynotes)

[SAP Security Certificates](https://www.sap.com/corporate/en/company/quality.html#certificates)

