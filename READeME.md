# Mixpanel Connector Integration Guide

## Introduction

The Mixpanel connector enables seamless integration with the Mixpanel platform, allowing you to manage service accounts through the Mixpanel API. This guide provides comprehensive instructions on configuring and utilizing the Mixpanel Connector within your application.

## Features

- Retrieve all service accounts from your Mixpanel organization
- Create new service accounts with customizable roles and permissions
- Query user profiles from Mixpanel
- Integration with FastAPI for easy API access
- Structured input and output schemas for validation

## Getting Started with Mixpanel

To begin using the Mixpanel connector, follow these steps:

1. **Create a Mixpanel Account:** Visit the Mixpanel website and sign up for an account - <https://mixpanel.com/>
2. **Set Up Your Mixpanel Project:** Once registered, create a new project and obtain the organization ID.
3. **Generate Service Account Credentials:** In your Mixpanel settings, create a service account and generate its credentials. These credentials will be used for authentication when interacting with the Mixpanel API.

## Configuring the Mixpanel Connector

Once you have your Mixpanel account and service account credentials, you can configure the Mixpanel Connector with the following settings:

- `organization_id`: Your Mixpanel organization ID.
- `username`: Your Mixpanel service account username.
- `password`: Your Mixpanel service account password.

## API Endpoints

The connector exposes the following endpoints:

### Get Service Accounts

```
GET /mixpanel/get_service_accounts/{connectorID}
```

Retrieves all service accounts from your Mixpanel organization.

#### Input Schema

The input schema requires your organization ID.

#### Output Schema

The output provides the total count of service accounts and a list of all service accounts retrieved.

### Create Service Account

```
POST /mixpanel/create/{connectorID}
```

Creates a new service account in your Mixpanel organization.

#### Input Schema

- `username`: (Required) Username for the service account.
- `role`: (Optional) Role of the service account.
- `expires`: (Optional) Expiration date for the service account.
- `projects`: (Optional) List of projects to associate with the service account.

#### Output Schema

- `service_account_created`: Indicates if the service account was created successfully.
- `id`: ID of the created service account.

### Query Profiles

```
POST /mixpanel/query_profiles/{connectorID}
```

Queries user profiles from Mixpanel based on the provided filters.

#### Input Schema

- `where`: (Optional) Query filter expression.
- `output_properties`: (Optional) List of properties to retrieve.
- `page`: (Optional) Page number for pagination.
- `session_id`: (Optional) Session ID for pagination.

#### Output Schema

- `results`: List of user profiles that match the query.
- `page`: Current page number.
- `session_id`: (Optional) Session ID for pagination.

### Get Schema

```
GET /mixpanel/get_service_accounts
```

Returns the input and output schema for the service accounts endpoint.

```
GET /mixpanel/create
```

Returns the input and output schema for the create service account endpoint.

```
GET /mixpanel/query_profiles
```

Returns the input and output schema for the query profiles endpoint.

## Implementation Details

The connector uses basic authentication with base64 encoding to authenticate requests to the Mixpanel API. It makes HTTP requests to the Mixpanel API endpoints to retrieve service account information and create new service accounts.

### Creating Service Accounts

When creating a service account, you must provide a username. You can optionally specify a role, an expiration date, and a list of projects to associate with the account.

### Querying User Profiles

The `query_profiles` endpoint allows you to filter user profiles using Mixpanel's query language. You can specify filtering conditions using the `where` parameter and retrieve specific properties using `output_properties`.

## Error Handling

The connector handles errors gracefully and returns appropriate HTTP exceptions with detailed error messages when issues occur during API requests. For creation requests, it will attempt to extract and return the detailed error information from the Mixpanel API response.

## Dependencies

- FastAPI
- Pydantic
- Requests
- Base64
