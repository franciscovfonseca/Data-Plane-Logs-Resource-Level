<br>

<h1 align="center">Data Plane Logs (Resource Level)</h1>

<br>

<p align="center">
<img width="800" src="https://github.com/user-attachments/assets/12379f2a-d3fb-4095-bc75-e41de1bfbe3e" alt="Banner"/>
<br />

<br />

This is the Final Lab where we are working on **Ingesting Logs** into our **Log Analytics Workspace**.

1. In this Lab we're going to finish things up by **Enabling Logging** for our **Storage Account** and forwarding it to the LAW.

2. We're going to Create a **Key Vault** ➜ and we'll **Enable Logging** for this and send the Logs to our LAW.

3. And as usual we're going to **Query** things and get a sense for what different Queries may look like.

<br>

<br>

>   <details close> 
>   
> **<summary> 📝 Explanation</summary>**
> 
> <br>
> 
> This Lab is for bringing in Logs from the **Data Plane** (AKA the actual **Resources themselves**) into our Log Analytics Workspace.
> 
> <br>
>   
> Just as a Reminder for this graphic:
> 
> - We previously did Azure Tenant Level ➜ which is like the AAD Logs
> 
> - We did Activity Log ➜ which is Subscription Level (AKA the Management Plane)
> 
> - And now we're doing the actual Resource themselves:
> 
> ![azure portal](https://github.com/user-attachments/assets/b322d695-fb20-4325-8918-d497235949a9)
> 
> We already configured the Virtual Machines ➜ so we're just going to do our **Azure Storage Account** and **Key Vault** in this Lab.
> 
>   </details>

<br>

<br>

<details close> 
<summary> <h2> 1️⃣ Configure Logging for Azure Storage</h2> </summary>
<br>

> The first thing we're going to do is **Configure Logging** for our **Storage Account** that already exists in our Environment.
>
> We made a Storage Acount for our NSG flow Logs earlier, but the Logs are not enabled for it yet.
> 
> We'll do this by **Enabling Diagnostic Settings for Blob Storage**.

<br>

Inside the **Azure Portal** ➜ search for our **Storage Account** ```sacyberlab999```

![azure portal](https://github.com/user-attachments/assets/cb28fc29-6358-4720-8ab7-b0134b8c653d)

Then We'll scroll down and click on the **Diagnostic settings** blade:

![azure portal](https://github.com/user-attachments/assets/2e5c3d6c-7fb5-4061-87eb-cfe7b2ca1bc0)

And we're going to Configure a Diagnostic Setting for the Blob Storage.

>   <details close> 
>   
> **<summary> 💡</summary>**
> 
> <br>
> 
> Basically, uploading files to the Storage Account, a text file for example, changing a text file or deleting it ➜ these actions will be logged here.
> 
> And this is the Data Plane for the Storage Account
> 
>   </details>

Click on **blob**:

![azure portal](https://github.com/user-attachments/assets/82aa469c-4f87-4d73-927a-8717a5b74985)

And then we'll ➕ **Add diagnostic setting**:

![azure portal](https://github.com/user-attachments/assets/12375231-1a9e-44aa-b4ee-cc7f1d9751ee)

- We can set up the **"Diagnostic setting name"** as ```ds-storage-account```

- For the **Logs’ Category Groups** ➜ select ☑️ **audit**

- **"Destination details"** ➜ check ☑️ **Send to Log analytics workspace** ➜ select ```LAW-Cyber-Lab-01```
    - ⚠️ Again ➜ Make sure it’s going to the correct one ➜ not the *DefaultWorkspace*

- Click 💾 Save

![azure portal](https://github.com/user-attachments/assets/d7eb8f87-c213-4a39-a71d-0ab06bbc7381)

The next thing we're going to do is Create an Azure Key Vault and Set Up Diagnostic Settings for it as well to send Logs into our LAW.

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2> 2️⃣ Configure Logging for Key Vault</h2> </summary>
<br>

> We're now going to Create a **Key Vault Instance**.
>
> We'll Configure Logging for our Key Vault by **Enabling Diagnostic Settings**.
> 
> Then we're going to **Add a Secret** to the Key Vault with a made up Password
>
> And finally we'll observe the Key in Key Vault

<br>

Back to the **Azure Portal** ➜ search for **Key Vault** ➜ and click on the **Create key vault** button

![azure portal](https://github.com/user-attachments/assets/d0145ab6-e373-4a20-be1f-b813a645ace2)

- Select our **Resource group** ```RG-Cyber-Lab```

- For the **Key vault name** ➜ ⚠️ it has to be globally unique ➜ for example: ```akv-cyber-lab-9999```

- Put it in the same **Region** as everything else ➜ ```East US 2```

Click **Next**

![azure portal](https://github.com/user-attachments/assets/9e5d7174-3256-4c49-8908-02c86878c0e2)

Under the **"Access configuration"** tab:

- For **Permission model** ➜ change it to ◉ **Vault access policy**

Click **Review + create**

![azure portal](https://github.com/user-attachments/assets/f097a391-fd88-4b75-b2e5-a8fdc7201444)

<br>

<h2></h2>

<br>

The next thing we're going to do is Create an Enterprise Secret

Open our **Key Vault** ```akv-cyber-lab-9999```

![azure portal](https://github.com/user-attachments/assets/8ea1c952-da65-4e57-a305-df1df588fd92)

Click on the **Secrets** blade ➜ and then ➕ **Generate/Import** to Create a New Secret:

![azure portal](https://github.com/user-attachments/assets/d42e94e1-6ea0-4cbf-8bee-fb93be1f8529)

- You can **Name** the Secret ```Tenant-Global-Admin-Password``` for example:
    - ⚠️ This isn't the actual Password itself ➜ this is just the **Name** of the Password

- The actual Password is the **Secret value** ➜ for the sake of the lab we'll make it ```Cyberlab123!```

Then just click **Create**

![azure portal](https://github.com/user-attachments/assets/4544b371-32aa-4614-9e48-33696fefdba6)

✅ We can confirm that the Secret was Successfully Created:

![azure portal](https://github.com/user-attachments/assets/8a8863ec-e412-4169-82a1-f932f9fd5f2d)

<br>

<h2></h2>

<br>

We're now going to Enable **Diagnostic Settings** for **Key vault**

Inside our **Key Vault** ➜ click on the **Diagnostic settings** blade ➜ and then ➕ **Add diagnostic setting**:

![azure portal](https://github.com/user-attachments/assets/680148fa-d114-41c9-82cc-96efec60bfc0)

- We can name it ```ds-akv```

- For the **Logs’ Category Groups** ➜ select ☑️ **audit**

- **"Destination details"** ➜ check ☑️ **Send to Log analytics workspace** ➜ select ```LAW-Cyber-Lab-01```

- Click 💾 Save

![azure portal](https://github.com/user-attachments/assets/1d8ba2c5-a3ed-4ac8-8ec5-6ff716c0ba97)

So now the Key Vault Logs should be forwarding to our Log Analytics Workspace.

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2> 3️⃣ Generate some Logs for Storage Account & Key Vault</h2> </summary>
<br>

> The next step is to **Generate some Logs** for the **Blob Storage**.
>
> We'll **Upload a Text File** to the Blob Storage Account ➜ and that should **Create Log**s that we can actually **Query and Observe**.
> 

<br>

We'll go back to the **Azure Portal** ➜ open our **Storage Account**:

![azure portal](https://github.com/user-attachments/assets/91c92fdf-0306-40ff-8feb-136306bda1c7)

Click on the **Containers** blade ➜ and ➕ **Container** to create a new Container

- Name it ```test``` ➜ and click **Create**

![azure portal](https://github.com/user-attachments/assets/d245af47-b331-4d21-a3f0-59b837a86f8d)

<br>

>   <details close> 
>   
> **<summary> 💡</summary>**
> 
> For all intents and purposes here: you can think of Containers as a top-level folder inside of your Storage Account.
> 
>   </details>

So we created a Container called ```test```:

![azure portal](https://github.com/user-attachments/assets/8113a37e-9a23-4664-8b23-d0ebdb6c1a7e)

And inside of our new Container ➜ we'll ↑ **Upload** a random Text File from our Computer:

![azure portal](https://github.com/user-attachments/assets/9ccf4aa6-ff38-4ab9-8605-86df702acaef)

✅ The act of **Uploading a Blob File** into our **Storage Account** is going to **Create Data Plane Logs** that our **Diagnosting Setting** (which we created earlier) should send to our LAW.

<br>

<h2></h2>

<br>

> We're now going to **Generate some Logs** for the **Key Vault**.
>
> To do so we will **Observe the Secret** inside of the Key Vault.
> 

<br>

We'll **Create another Secret**:

- **Name** the Secret ```Super-Secret-Password-1``` for example:

- For the **Secret value** ➜ we can make it ```Cyberlab123!``` again

![azure portal](https://github.com/user-attachments/assets/580b7c15-991b-4fcb-bb33-7b1288a711f5)

Now we have 2 Password in our Key Vault:

![azure portal](https://github.com/user-attachments/assets/8b190daa-fec6-475f-ab04-7de2aeb094a9)

<br>

<h2></h2>

<br>

We can now click on the ```Super-Secret-Password-1``` Secret to observe it:

![azure portal](https://github.com/user-attachments/assets/cb3636db-2bcf-40c6-b925-b63818604ea4)

![azure portal](https://github.com/user-attachments/assets/049e7797-081c-4dd1-a329-dd559d6c73fb)

Then we'll click on the **"Show Secret Value"** Button:

![azure portal](https://github.com/user-attachments/assets/faf2cc5d-cd14-4068-bb56-5c1970ce9bf9)

And the Secret Value / Password is revealed:

![azure portal](https://github.com/user-attachments/assets/ee3f6c2f-a97a-44a0-9bd7-301ae43d5ffd)

✅ The act of going to this page and **Show the Secret** should have **Created a Log** which will be forwarded to our LAW.

<br>
  </details>

<h2></h2>

<details close> 
<summary> <h2> 4️⃣ Observe the Logs with KQL Queries</h2> </summary>
<br>

> At this point we should be able to Query the ```StorageBlobLogs``` from the **Azure Storage Account**.
> 
> And we should also be able to Query the ```AzureDiagnostics``` for the **Azure Key Vault**.

<br>

We can start out by going to our LAW and **Run the ```StorageBlobLogs``` Query** to Analyse the Blob Storage Logs:

![azure portal](https://github.com/user-attachments/assets/c4af6a8d-0f98-4916-9aef-d45901246705)

<br>

📝 **Exercise**:
 
> We can also Run some of the following **KQL Queries** to Analyze some of the Logs Generated.
> 
> This will give us an idea of **How to Query Logs** and see some **Use Cases** that we might want to implement in our **SIEM** instance.

<details close> 
<summary> <h3> Storage Account Test Logs</h3> </summary>
<br>

#### Authorization Error:

```commandline
// Authorization Error
StorageBlobLogs 
| where MetricResponseType endswith "Error" 
| where StatusText == "AuthorizationPermissionMismatch"
| order by TimeGenerated asc
```

<br>

<h2></h2>

<br>

#### Reading Blobs:

```commandline
// Reading a bunch of blobs
StorageBlobLogs
| where OperationName == "GetBlob"
```

<br>

<h2></h2>

<br>

#### Deleting Blobs:

```commandline
//Deleting a bunch of blobs (in a short time period)
StorageBlobLogs | where OperationName == "DeleteBlob"
| where TimeGenerated > ago(24h)
```

<br>

<h2></h2>

<br>

#### Putting Blobs:

```commandline
//Putting a bunch of blobs (in a short time period) 
StorageBlobLogs | where OperationName == "PutBlob"
| where TimeGenerated > ago(24h)
```

<br>

<h2></h2>

<br>

#### Copying Blobs:

```commandline
//Copying a bunch of blobs (in a short time period)
StorageBlobLogs | where OperationName == "CopyBlob"
| where TimeGenerated > ago(24h)
```

<br>

<br>

💡 Note:

> We don't have to make Alerts for all of these in Microsoft Sentinel when we do it in future Labs.
>
> But it's kind of an idea that we can Query & Alert on anything.

<br>

  </details>

<br>

<h2></h2>

<br>

<br>

As we now **Run the ```AzureDiagnostics``` Query** ➜ we can see that **Key Vault Logs** started coming into our LAW:

![azure portal](https://github.com/user-attachments/assets/42c8f80c-aa9f-4507-99f2-9894ffd68fe4)

<br>

📝 **Exercise**:
 
> Similarlly to what we did with the Storage Account Logs ➜ we can Explore some of the following **KQL Queries**
> 
> By **Creating some Passwords & Observing them** inside of our **Azure Key vault** ➜ we've already **Generated some Logs** that we can Query inside of our LAW.

<details close> 
<summary> <h3> Key Vault Test Logs</h3> </summary>
<br>

#### List out Secrets:

```commandline
// List out Secrets
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretList"
```

<br>

<h2></h2>

<br>

#### Attempt to View Non-Existent Passwords:

```commandline
// Attempt to view passwords that don't exist
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretGet"
| where ResultSignature == "Not Found"
```

<br>

<h2></h2>

<br>

#### Viewing a Password:

```commandline
// Viewing an actual existing password
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretGet"
| where ResultSignature == "OK"
```

<br>

<h2></h2>

<br>

#### Viewing a Specific Password:

```commandline
// Viewing a specific existing password
let CRITICAL_PASSWORD_NAME = "Tenant-Global-Admin-Password";
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT"
| where OperationName == "SecretGet"
| where id_s contains CRITICAL_PASSWORD_NAME
```

<br>

<h2></h2>

<br>

#### Updating a Password ➜ Success:

```commandline
// Updating a password Success
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT" 
| where OperationName == "SecretSet"
```

<br>

<h2></h2>

<br>

#### Updating a Specific Password ➜ Success:

```commandline
// Updating a specific existing password Success
let CRITICAL_PASSWORD_NAME = "Tenant-Global-Admin-Password";
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT" 
| where OperationName == "SecretSet"
| where id_s endswith CRITICAL_PASSWORD_NAME
| where TimeGenerated > ago(2h)
```

<br>

<h2></h2>

<br>

#### Failed Access Attempts:

```commandline
// Failed access attempts
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.KEYVAULT" 
| where ResultSignature == "Unauthorized"
```

<br>

<br>

💡 Note:

> We were able to get a sense for what these different Queries and what different Use Cases that might come into play.
>
> We're going to add the ```// Viewing a specific existing password``` Query to **Microsoft Sentinel** in a future Lab when we Create the **Analytics Rules** that spin-up **Alerts & Incidents** when somebody **Looks at a Critical Password**.

<br>

  </details>

<br>

  </details>

<br>

<br>

<br>

<br>

<br>

<br>


 
