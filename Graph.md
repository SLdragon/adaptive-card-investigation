## Microsoft Graph API metadata
The metadata document also helps you to understand the data model of the resources and relationships in Microsoft Graph. The metadata document ($metadata) is published at the service root. You can view the service document for the v1.0 and beta versions of the Microsoft Graph API via the following URLs.

Microsoft Graph API v1.0 metadata

  https://graph.microsoft.com/v1.0/$metadata

Microsoft Graph API beta metadata

  https://graph.microsoft.com/beta/$metadata

## Sample definition
You can call graph API to get user information as below:
```
https://graph.microsoft.com/v1.0/me
```

Response:
```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users/$entity",
    "businessPhones": [
        "+1 412 555 0109"
    ],
    "displayName": "Megan Bowen",
    "givenName": "Megan",
    "jobTitle": "Auditor",
    "mail": "MeganB@M365x214355.onmicrosoft.com",
    "mobilePhone": null,
    "officeLocation": "12/1110",
    "preferredLanguage": "en-US",
    "surname": "Bowen",
    "userPrincipalName": "MeganB@M365x214355.onmicrosoft.com",
    "id": "48d31887-5fad-4d73-a9f5-3c356e68a038"
}
```

From the response json file, you can find the user entity definition as below:

```xml
<EntityType Name="user" BaseType="graph.directoryObject" OpenType="true">
  ...
  <Property Name="displayName" Type="Edm.String"/>
  <Property Name="employeeHireDate" Type="Edm.DateTimeOffset"/>
  <Property Name="employeeId" Type="Edm.String"/>
  <Property Name="employeeOrgData" Type="graph.employeeOrgData"/>
  <Property Name="employeeType" Type="Edm.String"/>
  <Property Name="externalUserState" Type="Edm.String"/>
  <Property Name="externalUserStateChangeDateTime" Type="Edm.DateTimeOffset"/>
  <Property Name="faxNumber" Type="Edm.String"/>
  <Property Name="givenName" Type="Edm.String"/>
  <Property Name="securityIdentifier" Type="Edm.String"/>
  ...
  <NavigationProperty Name="appRoleAssignments" Type="Collection(graph.appRoleAssignment)" ContainsTarget="true"/>
  <NavigationProperty Name="createdObjects" Type="Collection(graph.directoryObject)"/>
  <NavigationProperty Name="directReports" Type="Collection(graph.directoryObject)"/>
  <NavigationProperty Name="licenseDetails" Type="Collection(graph.licenseDetails)" ContainsTarget="true"/>
  <NavigationProperty Name="manager" Type="graph.directoryObject"/>
  <NavigationProperty Name="memberOf" Type="Collection(graph.directoryObject)"/>
  ...
</EntityType>
```

## OpenAPI definition for Graph API
The repo can be found here: https://github.com/microsoftgraph/msgraph-metadata

The API definition file can be found here: https://github.com/microsoftgraph/msgraph-metadata/tree/master/openapi/v1.0

A sample User Get option and User definition is as below:

```yaml
'/users/{user-id}':
    description: Provides operations to manage the collection of user entities.
    get:
      tags:
        - users.user
      summary: Get a user
      description: Retrieve the properties and relationships of user object.
      externalDocs:
        description: Find more info here
        url: https://docs.microsoft.com/graph/api/user-get?view=graph-rest-1.0
      operationId: users.user.GetUser
      parameters:
        - name: $select
          in: query
          description: Select properties to be returned
          style: form
          explode: false
          schema:
            uniqueItems: true
            type: array
            items:
              enum:
                - id
                - deletedDateTime
                - accountEnabled
                - ageGroup
                - assignedLicenses
                - assignedPlans
                - authorizationInfo
                - businessPhones
                - city
                - companyName
                - consentProvidedForMinor
                - country
                - createdDateTime
                - creationType
                - department
                - displayName
                - employeeHireDate
                - employeeId
                - employeeOrgData
                - employeeType
                - externalUserState
                - externalUserStateChangeDateTime
                - faxNumber
                - givenName
                - identities
                - imAddresses
                - isResourceAccount
                - jobTitle
                - lastPasswordChangeDateTime
                - legalAgeGroupClassification
                - licenseAssignmentStates
                - mail
                - mailNickname
                - mobilePhone
                - officeLocation
                - onPremisesDistinguishedName
                - onPremisesDomainName
                - onPremisesExtensionAttributes
                - onPremisesImmutableId
                - onPremisesLastSyncDateTime
                - onPremisesProvisioningErrors
                - onPremisesSamAccountName
                - onPremisesSecurityIdentifier
                - onPremisesSyncEnabled
                - onPremisesUserPrincipalName
                - otherMails
                - passwordPolicies
                - passwordProfile
                - postalCode
                - preferredDataLocation
                - preferredLanguage
                - provisionedPlans
                - proxyAddresses
                - securityIdentifier
                - showInAddressList
                - signInSessionsValidFromDateTime
                - state
                - streetAddress
                - surname
                - usageLocation
                - userPrincipalName
                - userType
                - mailboxSettings
                - deviceEnrollmentLimit
                - aboutMe
                - birthday
                - hireDate
                - interests
                - mySite
                - pastProjects
                - preferredName
                - responsibilities
                - schools
                - skills
                - appRoleAssignments
                - createdObjects
                - directReports
                - licenseDetails
                - manager
                - memberOf
                - oauth2PermissionGrants
                - ownedDevices
                - ownedObjects
                - registeredDevices
                - scopedRoleMemberOf
                - transitiveMemberOf
                - calendar
                - calendarGroups
                - calendars
                - calendarView
                - contactFolders
                - contacts
                - events
                - inferenceClassification
                - mailFolders
                - messages
                - outlook
                - people
                - drive
                - drives
                - followedSites
                - extensions
                - agreementAcceptances
                - managedDevices
                - managedAppRegistrations
                - deviceManagementTroubleshootingEvents
                - planner
                - insights
                - settings
                - onenote
                - photo
                - photos
                - activities
                - onlineMeetings
                - presence
                - authentication
                - chats
                - joinedTeams
                - teamwork
                - todo
              type: string
        - name: $expand
          in: query
          description: Expand related entities
          style: form
          explode: false
          schema:
            uniqueItems: true
            type: array
            items:
              enum:
                - '*'
                - appRoleAssignments
                - createdObjects
                - directReports
                - licenseDetails
                - manager
                - memberOf
                - oauth2PermissionGrants
                - ownedDevices
                - ownedObjects
                - registeredDevices
                - scopedRoleMemberOf
                - transitiveMemberOf
                - calendar
                - calendarGroups
                - calendars
                - calendarView
                - contactFolders
                - contacts
                - events
                - inferenceClassification
                - mailFolders
                - messages
                - outlook
                - people
                - drive
                - drives
                - followedSites
                - extensions
                - agreementAcceptances
                - managedDevices
                - managedAppRegistrations
                - deviceManagementTroubleshootingEvents
                - planner
                - insights
                - settings
                - onenote
                - photo
                - photos
                - activities
                - onlineMeetings
                - presence
                - authentication
                - chats
                - joinedTeams
                - teamwork
                - todo
              type: string
      responses:
        2XX:
          description: Retrieved entity
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/microsoft.graph.user'
        4XX:
          $ref: '#/components/responses/error'
        5XX:
          $ref: '#/components/responses/error'
      x-ms-docs-operation-type: operation
```

User definition: 
```yaml
    microsoft.graph.user:
      value:
        ...
        country: String
        createdDateTime: '0001-01-01T00:00:00.0000000+00:00'
        createdObjects:
          - '@odata.type': microsoft.graph.directoryObject
        creationType: String
        department: String
        deviceEnrollmentLimit: '0'
        deviceManagementTroubleshootingEvents:
          - '@odata.type': microsoft.graph.deviceManagementTroubleshootingEvent
        directReports:
          - '@odata.type': microsoft.graph.directoryObject
        displayName: String
        drive:
          '@odata.type': microsoft.graph.drive
        drives:
          - '@odata.type': microsoft.graph.drive
        employeeHireDate: '0001-01-01T00:00:00.0000000+00:00'
        employeeId: String
        employeeOrgData:
          '@odata.type': microsoft.graph.employeeOrgData
        employeeType: String
        events:
          - '@odata.type': microsoft.graph.event
        extensions:
          - '@odata.type': microsoft.graph.extension
        ...
        jobTitle: String
        joinedTeams:
          - '@odata.type': microsoft.graph.team
        ...
        userPrincipalName: String
        userType: String
```
