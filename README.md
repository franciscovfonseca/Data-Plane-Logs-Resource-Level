<br>

<h1 align="center">Data Plane Logs (Resource Level)</h1>

<br>

<p align="center">
<img width="800" src="https://github.com/user-attachments/assets/28983c6e-9754-4276-a3e9-c0426baa1b4f" alt="Banner"/>
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
> ![azure portal](https://github.com/user-attachments/assets/2727e56c-f7ee-478b-99f3-ecbabe939fd6)
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

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Then We'll scroll down and click on the **Diagnostic settings** blade:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

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

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

And then we'll ➕ **Add diagnostic setting**:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

- We can set up the **"Diagnostic setting name"** as ```ds-storage-account```

- For the **Logs’ Category Groups** ➜ select ☑️ **audit**

- **"Destination details"** ➜ check ☑️ **Send to Log analytics workspace** ➜ select ```LAW-Cyber-Lab-01```
    - ⚠️ Again ➜ Make sure it’s going to the correct one ➜ not the *DefaultWorkspace*

- Click 💾 Save

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

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

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

- Select our **Resource group** ```RG-Cyber-Lab```

- For the **Key vault name** ➜ ⚠️ it has to be globally unique ➜ for example: ```akv-cyber-lab-9999```

- Put it in the same **Region** as everything else ➜ ```East US 2```

Click **Next**

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Under the **"Access configuration"** tab:

- For **Permission model** ➜ change it to ◉ **Vault access policy**

Click **Review + create**

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

<br>

<h2></h2>

<br>

The next thing we're going to do is Create an Enterprise Secret

Open our **Key Vault** ```akv-cyber-lab-9999```

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Click on the **Secrets** blade ➜ and then ➕ **Generate/Import** to Create a New Secret:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

- You can **Name** the Secret ```Tenant-Global-Admin-Password``` for example:
    - ⚠️ This isn't the actual Password itself ➜ this is just the **Name** of the Password

- The actual Password is the **Secret value** ➜ for the sake of the lab we'll make it ```Cyberlab123!```

Then just click **Create**

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

✅ We can confirm that the Secret was Successfully Created:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

<br>

<h2></h2>

<br>

We're now going to Enable **Diagnostic Settings** for **Key vault**

Inside our **Key Vault** ➜ click on the **Diagnostic settings** blade ➜ and then ➕ **Add diagnostic setting**:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

- We can name it ```ds-akv```

- For the **Logs’ Category Groups** ➜ select ☑️ **audit**

- **"Destination details"** ➜ check ☑️ **Send to Log analytics workspace** ➜ select ```LAW-Cyber-Lab-01```

- Click 💾 Save

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

So now the Key Vault Logs should be forwarding to our Log Analytics Workspace.

<br>

<h2></h2>

<br>

We're going to Create another Secret:

- **Name** the Secret ```Super-Secret-Password-1``` for example:

- For the **Secret value** ➜ we can make it ```Cyberlab123!``` again

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Now we have 2 Password in our Key Vault:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

<br>

<h2></h2>

<br>

We can now click on the ```Super-Secret-Password-1``` Secret to observe it:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Then we'll click on the **"Show Secret Value"** Button:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

And the Secret Value / Password is revealed:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

✅ The act of going to this page and **Show the Secret** should have **Created a Log** which will be forwarded to our LAW.

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

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Click on the **Containers** blade ➜ and ➕ **Container** to create a new Container

- Name it ```test``` ➜ and click **Create**

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

<br>

>   <details close> 
>   
> **<summary> 💡</summary>**
> 
> For all intents and purposes here: you can think of Containers as a top-level folder inside of your Storage Account.
> 
>   </details>

So we created a Container called ```test```:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

And inside of our new Container ➜ we'll ↑ **Upload** a random Text File from our Computer:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

✅ The act of uploading a Blob File into our Storage Account is going to Create Data Plane Logs that our Diagnosting Setting that we created earlier should send to Log Analytics Workspace.

<br>

<h2></h2>

<br>

> We're now going to **Generate some Logs** for the **Key Vault**.
>
> To do so we will **Observe the Secret** inside of the Key Vault.
> 

<br>

We're going to Create another Secret:

- **Name** the Secret ```Super-Secret-Password-1``` for example:

- For the **Secret value** ➜ we can make it ```Cyberlab123!``` again

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Now we have 2 Password in our Key Vault:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

We can now click on the ```Super-Secret-Password-1``` Secret to observe it:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Then we'll click on the **"Show Secret Value"** Button:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

And the Secret Value / Password is revealed:

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

✅ The act of going to this page and **Show the Secret** should have **Created a Log** which will be forwarded to our LAW.


































In this next section of the Lab we're going to:

1. Create a new **Resource Group** called ```Scratch-Resource-Group```

2. Then we'll also create another **Resource Group** called ```Critical-Infrastructure-Wastewater```

3. After that, we'll **Delete** both of these **Resource Groups**

4. And finnally, we're going to do some **Queries against the Logs those actions Generated**

<br>

<h2></h2>

<br>

<h3> ❶ Create a new Resource Group named “Scratch-Resource-Group”</h3>
<br>

Back inside the **Azure Portal** ➜ search for **Resource Groups** ➜ and click on ➕ **Create**

![azure portal](https://github.com/user-attachments/assets/527a9345-c31a-4967-a183-6708ce63971e)

- We'll name the first Resource Group ```Scratch-Resource-Group```

- For the **Region** ➜ select ```(US) East US 2```

- Then click **Review + Create**

![azure portal](https://github.com/user-attachments/assets/8d53d3f3-1d7b-4ac3-a708-dc582de32745)

<br>

<h2></h2>

<br>

<h3> ❷ Create another new Resource Group named “Critical-Infrastructure-Wastewater”</h3>
<br>

For the Next Resource Group we'll follow the same steps as for the previous one.

- We'll name this second Resource Group ```Critical-Infrastructure-Wastewater```

- Again ➜ for the **Region** ➜ select ```(US) East US 2```

- Then click **Review + Create**

![azure portal](https://github.com/user-attachments/assets/b1bce04f-448e-449e-80c1-857f0ebe65cd)

<br>

✅ We can confirm that both of our new **Resource Groups** were created:

![azure portal](https://github.com/user-attachments/assets/eabe69da-449d-4f87-bb79-95222453cdd9)

<br>

<h2></h2>

<br>

<h3> ❸ Delete both of the new Resource Groups</h3>
<br>

Back to the **Azure Portal** ➜ go to our **Resource groups** ➜ click on ```Scratch-Resource-Group```

![azure portal](https://github.com/user-attachments/assets/9fb59564-ee3c-4be8-b963-53c3cb14c5d1)

We'll click on 🗑️ **Delete resource group**

![azure portal](https://github.com/user-attachments/assets/32a92fd7-cb93-4d80-99da-896200ab2742)

And then we'll Delete the Resource Group:

![azure portal](https://github.com/user-attachments/assets/49c16239-3b2b-4dd5-9ec8-60bec5fd79a7)

<br>

<h2></h2>

<br>

<br>

We'll do the exact same thing to **Delete** the ```Critical-Infrastructure-Wastewater``` Resource Group:

![azure portal](https://github.com/user-attachments/assets/764971d7-4ea6-49b8-8fe1-e2863557ee3f)

<br>

<h2></h2>

<br>

<h3> ❹ Query for the Deletion of Critical Resource Groups</h3>
<br>

We'll now copy the following **KQL Query** and paste into our **Log Analytics Workspace** to Inspect the **Delete Logs** we just Generated:

<br>

```commandline
// Deletion activities within a certain timespan:
AzureActivity
| where OperationNameValue endswith "DELETE"
| where ActivityStatusValue == "Success"
| where TimeGenerated > ago(30m)
| order by TimeGenerated
```

<br>

>   <details close> 
>   
> **<summary> 📝 KQL Query Explanation</summary>**
> 
>     <br>
>     
> This will return all of the Resource Groups that were successfully Deleted in Azure in the last 30 minutes.
>
> <br>
>     
> 💡 Note:
> 
> - If you wanna make an Alert for some reason for when someone deletes any specific Resource ➜ this KQL Query is something that you can use.
> 
> - Or also if you just want to manually Query in Log Analytics Workspace ➜ like we're doing here
> 
>   </details>

<br>

<br>

✅ We can confirm that the ***Delete Resource Group Activity Logs*** are properly being Generated & Forwarded to our LAW:

![azure portal](https://github.com/user-attachments/assets/4aab996a-dcf1-415f-967a-5168ef1738b9)

<br>

<h2></h2>

  </details>

<br>

<br>

<br>

<br>

# Summary

<br>

That wraps it up for this Lab.

<br>

As a Recap:

1. We just **Enabled the Azure Activity Log** ➜ which is the **Management Plane**.

<br>

>   <details close> 
> 
> **<summary> In other words:</summary>**
> 
> - Just clicking around and doing stuff on the Portal ➜ instead of the Logs just remaining in the **Azure Monitor Activity Log** ➜ we are forwarding them to the LAW.
> 
>   </details>

<br>

2. We also practiced **Querying** some of those Logs from the **AzureActivity** Table inside of the Log Analytics Workspace.

<br>

>   <details close> 
>   
> **<summary> 💡</summary>**
> 
> Ultimately ➜ after we Ingest all of the Logs into the Log Analytics Workspace:
>     
> - We're going to use **Microsoft Sentinel** to do Automated Queries and Spin-up Alerts based on different Logs that it finds.<br>
> 
>   </details>

<br>

In the Next Lab we're going to **Enable Diagnostic Settings and Logging & Monitoring** for the stuff at the actual **Resource Level**.

- So we're going to set up Logging for our **Storage Account**.

- And we're going to create a **Key Vault** ➜ and then set up Logging for that too.


<br />

<br />

<br />  

<br /> 

<br />

<br />  

<br /> 

<br />

<br />

 
