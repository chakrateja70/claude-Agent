# Mixpanel Connector

## Introduction
The Mixpanel Connector enables seamless integration with Mixpanel, allowing users to automate service account management, data tracking, event imports, and user profile queries. This guide provides comprehensive instructions on configuring and utilizing the Mixpanel Connector within your application.

---

## Getting Started with Mixpanel
To begin using the Mixpanel Connector, follow these steps:

1. **Create a Mixpanel Account:** Sign up for an account on [Mixpanel](https://mixpanel.com/).
2. **Set Up API Credentials:** Generate API credentials within Mixpanel to authenticate your application.
3. **Configure API Access:** Use the API credentials to establish a secure connection between your application and Mixpanel.

---

## Configuring the Mixpanel Connector
Once you have your Mixpanel account and API credentials, you can configure the Mixpanel Connector with the following settings:

- **API Key**: Your Mixpanel API key for authentication.
- **Service Account Credentials**: Required for managing service accounts and user data.

---

## Functionalities
The Mixpanel Connector supports the following actions:

### 1. Create a Service Account
**Description:** Creates a new service account in Mixpanel.

**Inputs:**
- `username` (string, required): Username for the service account.
- `role` (string, optional): Role of the service account.
- `expires` (string, optional): Expiration date for the service account.
- `projects` (array, optional): List of projects associated with the service account.

**Outputs:**
- `service_account_created` (string, required): Indicates if the account was successfully created.
- `id` (string, optional): ID of the created service account.

---

### 2. Get All Service Accounts
**Description:** Retrieves all service accounts from Mixpanel.

**Inputs:**
- `organization_id` (integer, required): Your organization ID.

**Outputs:**
- `total` (integer, required): Total number of service accounts retrieved.
- `service_accounts` (array, required): List of retrieved service accounts.

---

### 3. Query User Profiles
**Description:** Retrieves user profiles from Mixpanel based on query filters.

**Inputs:**
- `where` (string, optional): Query filter expression.
- `output_properties` (array, optional): List of properties to retrieve.
- `page` (integer, optional): Page number for pagination.
- `session_id` (string, optional): Session ID for pagination.

**Outputs:**
- `results` (array, required): List of user profiles matching the query.
- `page` (integer, required): Current page number.
- `session_id` (string, optional): Session ID for pagination.

---

### 4. Import Events
**Description:** Imports events into Mixpanel with strict validation and custom properties.

**Inputs:**
- `strict` (string, required): Strict mode validation flag.
- `events` (array, required): List of events to import.
- `properties` (object, required): Event properties.

**Outputs:**
- `status` (string, required): Response status.
- `num_records_imported` (integer, optional): Number of successfully imported records.

---


## 5. Track Event  
**Description:** Tracks events in Mixpanel with custom properties.  

**Inputs:**  
**Query Params:**  
- `strict` (string, required, defaults to `1`): When set to `1` (recommended), Mixpanel validates the batch and returns errors per event that failed.  
- `project_id` (string, required, defaults to `<YOUR_PROJECT_ID>`): The Mixpanel `project_id`, used to authenticate service account credentials.  

**Body Params:**  
- `event` (string, required): Name of the event.  
- `properties` (object, required): A JSON object containing event properties.  
  - `time` (integer, required): The time at which the event occurred, in seconds or milliseconds since UTC epoch.  
  - `distinct_id` (string, required): The unique identifier of the user who performed the event.  
  - `$insert_id` (string, required): A unique identifier for deduplication. Events with identical values for (`event`, `time`, `distinct_id`, `$insert_id`) are considered duplicates; only the latest one will be counted.  

**Outputs:**  
- `status` (integer, required): `1` for success, `0` for failure.  
- `error` (string, optional): Error message if the request was unsuccessful.

## Best Practices
To make the most out of the Mixpanel Connector, consider the following best practices:

- **Data Organization:** Properly structure and manage your event and profile data to ensure efficient queries.
- **Error Handling:** Implement robust error handling mechanisms to manage failed requests.
- **Collaboration:** Use Mixpanel’s sharing features to collaborate effectively with teams.
- **Security:** Secure your API credentials to prevent unauthorized access to your Mixpanel data.

---

## Conclusion
The Mixpanel Connector offers a powerful solution for automating service account management, event tracking, and user data queries through seamless integration with Mixpanel. By leveraging Mixpanel’s API capabilities, developers can build automation workflows to streamline analytics, event tracking, and user engagement. 

Follow Mixpanel's API usage guidelines and terms of service to maintain compliance and functionality.

For further details, refer to [Mixpanel API Documentation](https://developer.mixpanel.com/).

