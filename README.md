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

> The first thing we're going to do is configure Logging for our storage account that already exists in our Environment.
> 
> We'll do this by Enabling Diagnostic Settings for Blob storage
> 
> This will allow us to Collect All Logs & Metrics (metrics will record Auth Failures) and send it to our LAW instance.

<br>










<br>

<br>

<br>

<br>

<br>

<br>



We can go back to the **Azure Portal** ➜ search for **Monitor** ➜ and click on the **Activity log** blade

![azure portal](https://github.com/user-attachments/assets/d48d3fb9-7a66-48f1-9850-65ef7de0f74c)

Then we'll click on **⚙️ Export Activity Logs**:

![azure portal](https://github.com/user-attachments/assets/0c017a70-1461-4366-accc-9e462c55fd64)

And we're going to ➕ **Add diagnostic setting** to create another Diagnostic Setting:

![azure portal](https://github.com/user-attachments/assets/5f82762f-19c3-4a7d-a86f-707d9e1e2ad0)

- The **"Diagnostic setting name"** can be ```ds-azure-activity```

- For the **Logs’ Categories** ➜ we can select ☑️ all the options

- **"Destination details"** ➜ check ☑️ **Send to Log analytics workspace** ➜ select ```LAW-Cyber-Lab-01```
    - ⚠️ Again ➜ Make sure it’s going to the correct one ➜ not the *DefaultWorkspace*

- Click 💾 Save

![azure portal](https://github.com/user-attachments/assets/58331ef8-98d2-4f45-a20f-69883d0adc21)

✅ We can click back on **Diagnostic settings** and confirm that ```ds-azure-activity``` was successfully created:

![azure portal](https://github.com/user-attachments/assets/33e5eae0-9adf-4307-9e90-2ed120801e91)

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2> 2️⃣ Configure Logging for Key Vault</h2> </summary>
<br>




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

 
