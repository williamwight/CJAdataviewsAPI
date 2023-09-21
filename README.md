---
title: Dataviews APIs
description: Manage CJA dataviews through APIs
---
# Dataviews

* GET multiple dataviews: Retrieves a list of dataviews for a specified company
* GET a single dataview: Retrieves information for a single dataview
* POST validate a dataview: Checks a dataview for correct fields before creating
* POST create a dataview: Creates a dataview for a specified company
* PUT copy a dataview: Copies a dataview
* PUT modify a dataview: Modifies or updates a dataveiw with new data
* DELETE delete a dataview: Removes a dataview

## GET /data/dataviews {Retrieval of Data Views for a Company}

Use this endpoint to retrieve multiple data views associated with a company.

`GET https://cja.adobe.io/data/dataviews`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -L 'https://cja.adobe.io/data/dataviews?expansion=name%2Cowner%2Corganization%2Cdescription&limit=3&page=0' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {GLOBAL_COMPANY_ID}' \
-H 'Authorization: Bearer {AUTHORIZATION_TOKEN}'
```

#### Response

```JSON
{
    "content": [
        {
            "name": "Example 1 Data View",
            "description": "",
            "owner": {
                "imsUserId": "{IMS_USER_ID}",
                "ownerId": "{OWNER_ID}",
                "name": "Example name 1",
                "type": "imsUser"
            },
            "organization": "{IMS_ORG_ID}",
            "systemUserOwned": false,
            "id": "{DATA_VIEW_ID}"
        },
        {
            "name": "Example 2 Data View",
            "description": "",
            "owner": {
                "imsUserId": "{IMS_USER_ID}",
                "ownerId": "{OWNER_ID}",
                "name": "Example name 2",
                "type": "imsUser"
            },
            "organization": "{IMS_ORG_ID}",
            "systemUserOwned": false,
            "id": "{DATA_VIEW_ID}"
        },
        {
            "name": "Example 3 Data View",
            "description": "",
            "owner": {
                "imsUserId": "{IMS_USER_ID}",
                "ownerId": "{OWNER_ID}",
                "name": "Example name 3",
                "type": "imsUser"
            },
            "organization": "{IMS_ORG_ID}",
            "systemUserOwned": false,
            "id": "{DATA_VIEW_ID}"
        }
    ],
    "number": 0,
    "totalElements": 1170,
    "totalPages": 390,
    "numberOfElements": 3,
    "firstPage": true,
    "lastPage": false,
    "sort": null,
    "size": 3
}
```

### Request example details

The example above requests:

* the data views associated with {IMS_ORG_ID}.
* the name, owner, organization, and description of the data views to be included in the response.
* the `limit` of results per page be `3`.
* the `page` to be shown is the first page which is `0`.

### Response example details

The example above responds with:

* the page `number` `0` is being displayed.
* the page displayed is the `firstPage`, which is `true`.
* the `numberOfElements` per page is `3`.
* the `totalElements` of the `IMS_ORG_ID` is `1170`.
* the `totalPages` of data views is `390` when the `numberOfElements` per page is `3`.
* the `name`, `owner`, `organization`, and `description` of the data views, as asked for in the expansion parameter of the request.
* the `id` of the data views returned.

### Request Parameters

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `expansion` | optional | string | Comma-delimited list of additional fields to include on response. Includes the enums `name`, `description`, `owner`, `isDeleted`, `parentDataGroupId`, `segmentList`, `currentTimezoneOffset`, `timezoneDesignator`, `modified`, `createdDate`, `organization`, `curationEnabled`, `recentRecordedAccess`, `sessionDefinition`, `externalData`, and `containerNames`. |
| `parentDataGroupId` | optional | string | Filters data views by a single parent data group ID |
| `externalIds` | optional | string | Comma-delimited list of external IDs that limit the response |
| `externalParentIds` | optional | string | Comma-delimited list of external parent IDs that limit the response |
| `dataViewIds` | optional | string | Comma-delimited list of data view IDs that limit the response |
| `includeType` | optional | string | Include additional data views not owned by user |
| `cached` | optional | boolean | If it returns cached results. The default value is `true`. |
| `limit` | optional | integer | Number of results per page |
| `page` | optional | integer | The page number to be displayed. The first page is `0`. |
| `sortDirection` | optional | string | Sort direction (ASC or DESC) |
| `sortProperty` | optional | string | Property to sort by. Only `modifiedDate` and `id` are currently allowed. The default value is `id`. |

### Response Parameters

| Name | Type | Description |
| --- | --- | --- |
| `content` | container | The data views requested. Contains the `name`, `description`, `isDeleted`, `parentDataGroupId`, `segmentList`, `currentTimezoneOffset`, `timezoneDesignator`, `modifiedDate`, `createdDate`, `organization`, `modifiedBy`, `curationEnabled`, `recentRecordedAccess`, `sessionDefinition`, `externalData`, `containerNames`, and `id` parameters. |
| `name` | string | The name of a Data View |
| `description` | string | The description of a Data View |
| `owner` | container | The owner of a Data View. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` | string | The IMS user ID of the owner of a dataview |
| `name` | string | The name of the owner of a dataview |
| `isDeleted` | boolean | If the data view is deleted |
| `parentDataGroupId` | string | Filters data views by a single parent data group ID |
| `segmentList` | array of strings |  |
| `currentTimezoneOffset` | integer |  |
| `timezoneDesignator` | string | The timezone used by the data view |
| `modifiedDate` | string | The date the data view was last modified |
| `createdDate` | string | The date the data view was created |
| `organization` | string | The organization the data view belongs to |
| `modifiedBy` | string | Who modified the data view |
| `curationEnabled` | boolean |  |
| `recentRecordedAccess` | string | The most recent recorded access of the data view |
| `sessionDefinition` | conatiner | The parameters that define a session. Contains the `numPeriods`, `granularity`, `func`, and `events` parameters. |
| `numPeriods` | integer | |
| `granularity` | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS` |
| `events` | array of strings |  |
| `externalData` | container | The IDs of external entities linked to the data view. Contains the `externalParentId`, and `externalId` parameters.|
| `externalId` | string |  |
| `externalParentId` | string | The ID of the parent data group used by the data view |
| `containerNames` | container | Optional names to replace the default container names. Contains the `event`, `session`, and `people` parameters. |
| `event` | string | The name of the event container |
| `session` | string | The name of the session container |
| `people` | string | The name of the people container |
| `id` | string | The ID of the given data view |
| `pageable` | container | Contains the `sort`, `paged`, `unpaged`, `pageNumber`, `pageSize`, and `offset` parameters |
| `sort` | container | Contains the `sorted`, `unsorted`, and `empty` parameters |
| `sorted` | boolean |  |
| `unsorted` | boolean |  |
| `empty` | boolean |  |
| `paged` | boolean |  |
| `unpaged` | boolean |  |
| `pageNumber` | integer |  |
| `pageSize` | integer |  |
| `offset` | integer |  |
| `totalElements` | integer | The number of data sets belonging to the organization |
| `totalPages` | integer | The number of pages able to be displayed with the chosen filters |
| `lastPage` | boolean | If the shown page is the last page of data sets |
| `firstPage` | boolean | If the shown page is the first page of data sets |
| `numberOfElements` | integer | The number of data sets displayed per page |
| `size` | integer | The number of data sets displayed per page |
| `number` | integer | The page number being displayed. The first page is `0`. |

## POST /data/dataviews {Creation of Data Views}

Use this endpoint to create a data view using a JSON payload.

`POST https://cja.adobe.io/data/dataviews`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -L 'https://cja.adobe.io/data/dataviews?expansion=name%2Cdescription%2CparentDataGroupId%2CcurrentTimezoneOffset%2CtimezoneDesignator%2Corganization%2CsessionDefinition%2CexternalData' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {GLOBAL_COMPANY_ID}' \
-H 'Authorization: Bearer {AUTHORIZATION_TOKEN}'\
-H 'Content-Type: application/json' \
--data-raw '{
  "name": "testView",
  "description": "A Test Data View",
  "parentDataGroupId": "{PARENT_DATA_GROUP_ID}",
  "timezoneDesignator": "US/Mountain",
  "sessionDefinition": [
    {
      "numPeriods": 15,
      "granularity": "MINUTE",
      "func": "INACTIVITY",
      "events": [
        "string"
      ]
    }
  ],
  "organization": "{IMS_ORG_ID}",
  "externalData": {
    "externalParentId": "{EXTERNAL_PARENT_ID}"
  }
}'
```

#### Response

```JSON
{
    "name": "testView",
    "description": "A Test Data View",
    "parentDataGroupId": "{PARENT_DATA_GROUP_ID}",
    "currentTimezoneOffset": -6.0,
    "timezoneDesignator": "US/Mountain",
    "organization": "{IMS_ORG_ID}",
    "sessionDefinition": [
        {
            "numPeriods": 15,
            "granularity": "minute",
            "func": "inactivity",
            "events": [
                "string"
            ]
        }
    ],
    "externalData": {
        "externalParentId": "{EXTERNAL_PARENT_ID}"
    },
    "id": "{DATA_VIEW_ID}"
}
```

### Request example details

The example above requests the following:

* the `name` of the data view should be `testView`.
* the `parentDataGroupId` should be the given `{PARENT_DATA_GROUP_ID}`.
* `inactivity` be described as 15 minutes.

### Response example details

The response example above responds the following:

* the `id` of the created data view is `{DATA_VIEW_ID}`

### Request Parameters

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `expansion` |  | string | Comma-delimited list of additional fields to include on response. Includes the enums `name`, `description`, `owner`, `isDeleted`, `parentDataGroupId`, `segmentList`, `currentTimezoneOffset`, `timezoneDesignator`, `modified`, `createdDate`, `organization`, `curationEnabled`, `recentRecordedAccess`, `sessionDefinition`, `externalData`, and `containerNames`. |

#### Request Body

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `name` |  | string | The name of the data view |
| `description` |  | string | The description of a data view |
| `owner` |  | container | The owner of a data view. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` |  | string | The IMS user ID of the owner of a data view |
| `name` |  | string | The name of the owner of a data view |
| `isDeleted` |  | boolean | If the data view is deleted |
| `parentDataGroupId` |  | string | The data group ID associated with the data view |
| `segmentList` | | array of strings |  |
| `currentTimezoneOffset` | | integer |  |
| `timezoneDesignator` | | string | The timezone used by the data view |
| `modifiedDate` | | string | The date the data view was last modified |
| `createdDate` | | string | The date the data view was created |
| `organization` | | string | The organization the data view belongs to |
| `modifiedBy` | | string | Who last modified the data view |
| `curationEnabled` |  | boolean |  |
| `recentRecordedAccess` |  | string |  |
| `sessionDefinition` |  | container | Contains the `numPeriods`, `granularity`, `func`, and `events` parameters |
| `numPeriods` |  | integer |  |
| `granularity` |  | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` |  | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS`. |
| `events` |  | array of strings |  |
| `externalData` |  | container | Contains the `externalId`, and `externalParentId` parameters |
| `externalId` |  | string |  |
| `externalParentId` |  | string | The ID of the parent data group used by the data view |
| `containerNames` |  | container | Contains the `event`, `session`, and `people` parameters |
| `event` | | string | The name of the event container |
| `session` | | string | The name of the session container |
| `people` | | string | The name of the people container |
| `id` | | string | The ID of the data view |

### Response Parameters

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the data view |
| `description` | string | The description of a data view |
| `owner` | container | The owner of a data view. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` | string | The IMS user ID of the owner of a data view |
| `name` | string | The name of the owner of a data view |
| `isDeleted` | boolean | If the data view is deleted |
| `parentDataGroupId` | string | The data group ID associated with the data view |
| `segmentList` | array of strings |  |
| `currentTimezoneOffset` | integer |  |
| `timezoneDesignator` | string | The timezone used by the data view |
| `modifiedDate` | string | The date the data view was last modified |
| `createdDate` | string | The date the data view was created |
| `organization` | string | The organization the data view belongs to |
| `modifiedBy` | string | Who last modified the data view |
| `curationEnabled` |  boolean |  |
| `recentRecordedAccess` | string |  |
| `sessionDefinition` | container | Contains the `numPeriods`, `granularity`, `func`, and `events` parameters |
| `numPeriods` | integer |  |
| `granularity` | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS`. |
| `events` | array of strings |  |
| `externalData` | container | Contains the `externalId`, and `externalParentId` parameters |
| `externalId` | string |  |
| `externalParentId` | string | The ID of the parent data group used by the data view |
| `containerNames` | container | Contains the `event`, `session`, and `people` parameters |
| `event` | string | The name of the event container |
| `session` | string | The name of the session container |
| `people` | string | The name of the people container |
| `id` | string | The ID of the data view |

## GET /data/dataviews/{dataViewId} {Retrieval of a Data View by dataViewId}

Use this endpoint to retrieve data associated with a specific data view.

`GET https://cja.adobe.io/data/dataviews/{DATA_VIEW_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -L 'https://cja.adobe.io/data/dataviews/{DATA_VIEW_ID}?expansion=name%2Cowner%2Cdescription%2CparentDataGroupId%2CtimezoneDesignator%2CexternalData%2CcontainerNames' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {GLOBAL_COMPANY_ID}' \
-H 'Authorization: Bearer {AUTHORIZATION_TOKEN}'
```

#### Response

```JSON
{
    "name": "Example Data View 1",
    "description": "An example Data View",
    "owner": {
        "imsUserId": "{IMS_USER_ID}",
        "ownerId": "{OWNER_ID}",
        "name": "Example name 1",
        "type": "imsUser"
    },
    "parentDataGroupId": "{PARENT_DATA_GROUP_ID}",
    "timezoneDesignator": "US/Mountain",
    "externalData": {
        "externalParentId": "{EXTERNAL_PARENT_ID}"
    },
    "id": "{DATA_VIEW_ID}"
}
```

### Request example details

The example above requests the `name`. `owner`, `description`, `parentDataGroupId`, `timezoneDesignator`, `externalData`, and `containerNames` of the data view using the `expansion` parameter.

### Response example details

The example above responds the `name`. `owner`, `description`, `parentDataGroupId`, `timezoneDesignator`, `externalData`, and `containerNames` of the data view.

### Request Parameters

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `dataViewId` | required | string | The Data View ID to lookup |
| `expansion` |  | array of strings | Comma-delimited list of additional fields to include on response. Includes the enums `name`, `description`, `owner`, `isDeleted`, `parentDataGroupId`, `segmentList`, `currentTimezoneOffset`, `timezoneDesignator`, `modified`, `createdDate`, `organization`, `curationEnabled`, `recentRecordedAccess`, `sessionDefinition`, `externalData`, and `containerNames`. |

### Response Parameters

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the data view |
| `description` | string | The description of a data view |
| `owner` | container | The owner of a data view. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` | string | The IMS user ID of the owner of a data view |
| `name` | string | The name of the owner of a data view |
| `isDeleted` | boolean | If the data view is deleted |
| `parentDataGroupId` | string | The data group ID associated with the data view |
| `segmentList` | array of strings |  |
| `currentTimezoneOffset` | integer |  |
| `timezoneDesignator` | string | The timezone used by the data view |
| `modifiedDate` | string | The date the data view was last modified |
| `createdDate` | string | The date the data view was created |
| `organization` | string | The organization the data view belongs to |
| `modifiedBy` | string | Who last modified the data view |
| `curationEnabled` |  boolean |  |
| `recentRecordedAccess` | string |  |
| `sessionDefinition` | container | Contains the `numPeriods`, `granularity`, `func`, and `events` parameters |
| `numPeriods` | integer |  |
| `granularity` | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS`. |
| `events` | array of strings |  |
| `externalData` | container | Contains the `externalId`, and `externalParentId` parameters |
| `externalId` | string |  |
| `externalParentId` | string | The ID of the parent data group used by the data view |
| `containerNames` | container | Contains the `event`, `session`, and `people` parameters |
| `event` | string | The name of the event container |
| `session` | string | The name of the session container |
| `people` | string | The name of the people container |
| `id` | string | The ID of the data view |

## PUT /data/dataviews/{dataViewId} {Modification of a Data View by dataViewId}

Use this endpoint to modify a data view by sending a JSON structure containing the values to be changed.

`PUT https://cja.adobe.io/data/dataviews/{DATA_VIEW_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -L -X PUT 'https://cja.adobe.io/data/dataviews/{DATA_VIEW_ID}?expansion=name%2Cdescription%2Cowner%2Cmodified' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {GLOBAL_COMPANY_ID}' \
-H 'Authorization: Bearer {AUTHORIZATION_TOKEN}'\
-H 'Content-Type: application/json' \
--data-raw '{
  "name": "testView",
  "description": "A Test Data View",
  "parentDataGroupId": "{PARENT_DATA_GROUP_ID}",
  "timezoneDesignator": "US/Mountain",
  "sessionDefinition": [
    {
      "numPeriods": 15,
      "granularity": "MINUTE",
      "func": "INACTIVITY",
      "events": [
        "string"
      ]
    }
  ],
  "organization": "{IMS_ORG_ID}",
  "externalData": {
    "externalParentId": "{EXTERNAL_PARENT_ID}"
  }
}'
```

#### Response

```JSON
{
    "name": "testView",
    "description": "A Test Data View",
    "owner": {
        "imsUserId": "{IMS_USER_ID}",
        "ownerId": "{OWNER_ID}",
        "name": "null null",
        "type": "imsUser"
    },
    "modifiedDate": "2023-09-19T20:32:20Z",
    "modifiedBy": "{IMS_USER_ID}",
    "id": "{DATA_VIEW_ID}"
}
```

### Request example details

The example above requests to modify the `{DATA_VIEW_ID}` using the `--data-raw`.

### Response example details

The example above responds with the updated values of the data view.

### Request Parameters

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `dataViewId` | required | string | The Data View ID to update |
| `expansion` |  | string | Comma-delimited list of additional fields to include on response. Includes the enums `name`, `description`, `owner`, `isDeleted`, `parentDataGroupId`, `segmentList`, `currentTimezoneOffset`, `timezoneDesignator`, `modified`, `createdDate`, `organization`, `curationEnabled`, `recentRecordedAccess`, `sessionDefinition`, `externalData`, and `containerNames`. |

#### Request Body

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `name` |  | string | The name of the data view |
| `description` |  | string | The description of a data view |
| `owner` |  | container | The owner of a data view. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` |  | string | The IMS user ID of the owner of a data view |
| `name` |  | string | The name of the owner of a data view |
| `isDeleted` |  | boolean | If the data view is deleted |
| `parentDataGroupId` |  | string | The data group ID associated with the data view |
| `segmentList` | | array of strings |  |
| `currentTimezoneOffset` | | integer |  |
| `timezoneDesignator` | | string | The timezone used by the data view |
| `modifiedDate` | | string | The date the data view was last modified |
| `createdDate` | | string | The date the data view was created |
| `organization` | | string | The organization the data view belongs to |
| `modifiedBy` | | string | Who last modified the data view |
| `curationEnabled` |  | boolean |  |
| `recentRecordedAccess` |  | string |  |
| `sessionDefinition` |  | container | Contains the `numPeriods`, `granularity`, `func`, and `events` parameters |
| `numPeriods` |  | integer |  |
| `granularity` |  | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` |  | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS`. |
| `events` |  | array of strings |  |
| `externalData` |  | container | Contains the `externalId`, and `externalParentId` parameters |
| `externalId` |  | string |  |
| `externalParentId` |  | string | The ID of the parent data group used by the data view |
| `containerNames` |  | container | Contains the `event`, `session`, and `people` parameters |
| `event` | | string | The name of the event container |
| `session` | | string | The name of the session container |
| `people` | | string | The name of the people container |
| `id` | | string | The ID of the data view |

### Response Parameters

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the data view |
| `description` | string | The description of a data view |
| `owner` | container | The owner of a data view. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` | string | The IMS user ID of the owner of a data view |
| `name` | string | The name of the owner of a data view |
| `isDeleted` | boolean | If the data view is deleted |
| `parentDataGroupId` | string | The data group ID associated with the data view |
| `segmentList` | array of strings |  |
| `currentTimezoneOffset` | integer |  |
| `timezoneDesignator` | string | The timezone used by the data view |
| `modifiedDate` | string | The date the data view was last modified |
| `createdDate` | string | The date the data view was created |
| `organization` | string | The organization the data view belongs to |
| `modifiedBy` | string | Who last modified the data view |
| `curationEnabled` |  boolean |  |
| `recentRecordedAccess` | string |  |
| `sessionDefinition` | container | Contains the `numPeriods`, `granularity`, `func`, and `events` parameters |
| `numPeriods` | integer |  |
| `granularity` | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS`. |
| `events` | array of strings |  |
| `externalData` | container | Contains the `externalId`, and `externalParentId` parameters |
| `externalId` | string |  |
| `externalParentId` | string | The ID of the parent data group used by the data view |
| `containerNames` | container | Contains the `event`, `session`, and `people` parameters |
| `event` | string | The name of the event container |
| `session` | string | The name of the session container |
| `people` | string | The name of the people container |
| `id` | string | The ID of the data view |

## DELETE /data/dataviews/{dataViewId} {Deletion of a Data View by dataViewId}

{DESCRIPTION}

`DELETE https://cja.adobe.io/data/dataviews/{DATA_VIEW_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -L -X DELETE 'https://cja.adobe.io/data/dataviews/{DATA_VIEW_ID}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {GLOBAL_COMPANY_ID}' \
-H 'Authorization: Bearer {AUTHORIZATION_TOKEN}'\
-d ''
```

#### Response

```JSON
{
    "result": "success"
}
```

### Request example details

The example above requests to `DELETE` the `{DATA_VIEW_ID}`.

### Response example details

The example above returns that the `result` of the delete was `success`.

### Request Parameters

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `dataViewId` | required | string | The Data View ID to delete |

### Response Parameters

| Name | Type | Description |
| --- | --- | --- |
| `result` | sting | The result of the delete request |
| `message` | string | A message associated with the result |

## PUT /data/dataviews/copy/{dataViewId} {Copy a data view}

{DESCRIPTION}

`PUT https://cja.adobe.io/data/dataviews/copy/{DATA_VIEW_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -L -X PUT 'https://cja.adobe.io/data/dataviews/copy/{DATA_VIEW_ID}?expansion=name%2Cdescription%2Cowner%2CcreatedDate' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {GLOBAL_COMPANY_ID}' \
-H 'Authorization: Bearer {AUTHORIZATION_TOKEN}'\
-d ''
```

#### Response

```JSON
{
    "name": "testView (Copy)",
    "description": "A test data view",
    "owner": {
        "imsUserId": "{IMS_USER_ID}",
        "ownerId": "{OWNER_ID}",
        "name": "null null",
        "type": "imsUser"
    },
    "createdDate": "2023-09-19T20:20:11Z",
    "componentType": "dataView",
    "id": "{DATA_VIEW_ID}"
}
```

### Request example details

The example above request to copy the `{DATA_VIEW_ID}`.

### Response example details

The example above returns the information of the newly copied data view.

### Request Parameters

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `dataViewId` | required | string | The Data View ID to copy |
| `expansion` |  | array of strings | Comma-delimited list of additional fields to include on response. Includes the enums `name`, `description`, `owner`, `isDeleted`, `parentDataGroupId`, `segmentList`, `currentTimezoneOffset`, `timezoneDesignator`, `modified`, `createdDate`, `organization`, `curationEnabled`, `recentRecordedAccess`, `sessionDefinition`, `externalData`, and `containerNames`. |

### Response Parameters

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the data view |
| `description` | string | The description of a data view |
| `owner` | container | The owner of a data view. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` | string | The IMS user ID of the owner of a data view |
| `name` | string | The name of the owner of a data view |
| `isDeleted` | boolean | If the data view is deleted |
| `parentDataGroupId` | string | The data group ID associated with the data view |
| `segmentList` | array of strings |  |
| `currentTimezoneOffset` | integer |  |
| `timezoneDesignator` | string | The timezone used by the data view |
| `modifiedDate` | string | The date the data view was last modified |
| `createdDate` | string | The date the data view was created |
| `organization` | string | The organization the data view belongs to |
| `modifiedBy` | string | Who last modified the data view |
| `curationEnabled` |  boolean |  |
| `recentRecordedAccess` | string |  |
| `sessionDefinition` | container | Contains the `numPeriods`, `granularity`, `func`, and `events` parameters |
| `numPeriods` | integer |  |
| `granularity` | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS`. |
| `events` | array of strings |  |
| `externalData` | container | Contains the `externalId`, and `externalParentId` parameters |
| `externalId` | string |  |
| `externalParentId` | string | The ID of the parent data group used by the data view |
| `containerNames` | container | Contains the `event`, `session`, and `people` parameters |
| `event` | string | The name of the event container |
| `session` | string | The name of the session container |
| `people` | string | The name of the people container |
| `id` | string | The ID of the data view |

## POST /data/dataviews/validate {Validates a data view}

{DESCRIPTION}

`POST https://cja.adobe.io/data/dataviews/validate`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -L 'https://cja.adobe.io/data/dataviews/validate' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {GLOBAL_COMPANY_ID}' \
-H 'Authorization: Bearer {AUTHORIZATION_TOKEN}'\
-H 'Content-Type: application/json' \
--data-raw '{
    "name": "testView",
    "description": "A Test Data View",
    "owner": {
        "imsUserId": "{IMS_USER_ID}",
        "ownerId": "{OWNER_ID}",
        "name": "null null",
        "type": "imsUser"
    },
    "isDeleted": false,
    "parentDataGroupId": "{PARENT_DATA_GROUP_ID}",
    "timezoneDesignator": "US/Mountain",
    "organization": "{IMS_ORG_ID}",
    "modifiedBy": "{IMS_USER_ID}",
    "sessionDefinition": [
        {
            "numPeriods": 15,
            "granularity": "minute",
            "func": "inactivity",
            "events": [
                "string"
            ]
        }
    ],
    "externalData": {
        "externalParentId": "{EXTERNAL_PARENT_ID}"
    }
}'
```

#### Response

```JSON
{
    "valid": true
}
```

### Request example details

The example above requests to validate the data view information given.

### Response example details

The example response above states the state of the data view is `valid`.

### Request Parameters

#### Request Body

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `name` |  | string | The name of the data view |
| `description` |  | string | The description of a data view |
| `owner` |  | container | The owner of a data view. Contains the `imsUserId`, and `name` parameters. |
| `imsUserId` |  | string | The IMS user ID of the owner of a data view |
| `name` |  | string | The name of the owner of a data view |
| `isDeleted` |  | boolean | If the data view is deleted |
| `parentDataGroupId` |  | string | The data group ID associated with the data view |
| `segmentList` | | array of strings |  |
| `currentTimezoneOffset` | | integer |  |
| `timezoneDesignator` | | string | The timezone used by the data view |
| `modifiedDate` | | string | The date the data view was last modified |
| `createdDate` | | string | The date the data view was created |
| `organization` | | string | The organization the data view belongs to |
| `modifiedBy` | | string | Who last modified the data view |
| `curationEnabled` |  | boolean |  |
| `recentRecordedAccess` |  | string |  |
| `sessionDefinition` |  | container | Contains the `numPeriods`, `granularity`, `func`, and `events` parameters |
| `numPeriods` |  | integer |  |
| `granularity` |  | string | A defined period of time. Includes the following enums: `MINUTE`, `HOUR`, `DAY`, and `WEEK`. |
| `func` |  | string | Includes the enums: `INACTIVITY`, and `BEFORE_EVENTS`. |
| `events` |  | array of strings |  |
| `externalData` |  | container | Contains the `externalId`, and `externalParentId` parameters |
| `externalId` |  | string |  |
| `externalParentId` |  | string | The ID of the parent data group used by the data view |
| `containerNames` |  | container | Contains the `event`, `session`, and `people` parameters |
| `event` | | string | The name of the event container |
| `session` | | string | The name of the session container |
| `people` | | string | The name of the people container |
| `id` | | string | The ID of the data view |


### Response Parameters

| Name | Type | Description |
| --- | --- | --- |
| `valid` | boolean | If the data view is valid |
| `message` | string | Any issues with the provided data view |
| `validator_version` | string | The validator version |
