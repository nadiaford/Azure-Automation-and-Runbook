# Azure Automation and Runbook

This guide outlines the steps to create an Azure Automation Account, manage User Identity, and test + publish a runbook.

## Steps

1. **Navigate to Automation Accounts**
   - Use the search bar or the "More Services" button to find and select "Automation Accounts."
   - Click **Create**.

![Automation Account Screenshot](https://i.imgur.com/uUAk8Pu.png "Automation Account Screenshot")


2. **Fill Out Basic Information**
   - Complete all text fields in the **Basics** tab:
     - Select your **Subscription**.
     - Create or select a **Resource Group** (e.g., "Automation-RG01").
     - Name your Automation Account (e.g., "AutomationAccount01").
     - Choose your **Region**.
   - Click **Review + Create** to skip additional options for this project.
  
![Automation Account Screenshot](https://i.imgur.com/gdhELmZ.png "Automation Account Screenshot")

3. **Access the Automation Account**
   - Once created, select the new Automation Account.
   - Navigate to the **Process Automation** dropdown menu.
   - Select **Runbooks**.

![Automation Account Screenshot](https://i.imgur.com/aWoBpne.png "Automation Account Screenshot")

4. **Create a Runbook**
   - Click **Create a runbook**.
   - Fill out required fields in the **Basics** tab:
     - Name: `SimpleBook`
     - Runbook Type: `PowerShell`
     - Runtime Version: `7.1 (preview)`
   - Click **Review + Create**, then **Create**.

![Automation Account Screenshot](https://i.imgur.com/bOBFqV7.png "Automation Account Screenshot")


5. **Edit the PowerShell Runbook**
   - Use the following code in the **Edit PowerShell Runbook** section:

     ```powershell
     # Verify the PowerShell Version
     $PSVersionTable

     # Ensures you do not inherit an AzContext in the runbook
     Disable-AzContextAutosave -Scope Process

     # Connect to Azure with system-assigned managed identity 
     $AzureContext = (Connect-AzAccount -Identity).context 

     # Set and store context
     $AzureContext = Set-AzContext -SubscriptionName $AzureContext.Subscription -DefaultProfile $AzureContext

     # To view details about this automation account
     Get-AzAutomationAccount -ResourceGroup "Automation-RG01" -Name "AutomationAccount01"
     ```
![Automation Account Screenshot](https://i.imgur.com/ZvClmjx.png "Automation Account Screenshot")

6. **Test the Runbook**
   - Click **Test Pane**.
   - Click **Start** to test the code.

![Automation Account Screenshot](https://i.imgur.com/DMkqyIq.png "Automation Account Screenshot")

7. **Publish the Runbook**
   - After a successful test, click **Publish** to upload the runbook.
  
![Automation Account Screenshot](https://i.imgur.com/MkJmILO.png "Automation Account Screenshot")

8. **Run the Published Runbook**
   - Start `SimpleRunbook`.
   - Wait for the **Status** to display "Completed."
   - Confirm the results via the **Overview** tab under **Monitoring**.
  
![Automation Account Screenshot](https://i.imgur.com/OiPoYuz.png "Automation Account Screenshot")
![Automation Account Screenshot](https://i.imgur.com/TDYcKHC.png "Automation Account Screenshot")
![Automation Account Screenshot](https://i.imgur.com/ovLY2qT.png "Automation Account Screenshot")

## Notes
- Make sure to double-check resource names and regions for your specific project requirements.
- This example uses a PowerShell runbook with system-assigned managed identity to connect to Azure.

Happy automating!


