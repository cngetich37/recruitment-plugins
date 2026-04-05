# PreValidationaccountCreate Plugin

This repository contains a Dynamics 365 / Dataverse plugin for validating account creation requests. The main logic is implemented in the `PreValidationaccountCreate` class, which is designed to run during the PreValidation stage of the account entity's create operation.

## Features
- **Account Name Validation:** Ensures that the `name` field is provided when creating a new account. If missing or empty, the plugin throws an error and prevents the record from being created.
- **Phone Number Validation:** If a phone number (`telephone1`) is provided, the plugin checks that it is exactly 10 digits. If not, an error is thrown and the record is not created.
- **Custom Error Messages:** Validation errors are returned as user-friendly messages, guiding users to correct their input.

## Technologies Used
- C# 7.3
- .NET Framework 4.6.2
- Microsoft.Xrm.Sdk (Dynamics 365 / Dataverse SDK)

## How It Works
The plugin is registered on the `account` entity for the `Create` message in the PreValidation stage. When a new account is created:
- The plugin checks if the `name` attribute is present and not empty.
- If a `telephone1` value is provided, it must be a 10-digit number.
- If validation fails, an `InvalidPluginExecutionException` is thrown with a descriptive message.

## Deployment
1. Build the project in Visual Studio to generate the plugin DLL.
2. Register the assembly and step using the Plugin Registration Tool or XrmToolBox.
3. Deploy to your Dynamics 365 or Dataverse environment as an unmanaged solution.

## Example
- Attempting to create an account without a name will result in: `Account name is required.`
- Entering a phone number that is not 10 digits will result in: `Phone number must be 10 digits.`

## Customization
You can extend the plugin by adding more validation logic inside the `ExecuteCdsPlugin` method.

## License
This project is provided as-is without any warranty. See the repository for license details.
