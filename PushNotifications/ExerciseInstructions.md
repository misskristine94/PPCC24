# Push Notifications in Power Apps (Canvas Apps) with SharePoint List

In this exercise, you'll learn how to send **push notifications** to mobile users in a Power Apps canvas app when a new item is added to a **SharePoint list**. We will use **Power Automate** to trigger the push notifications when a new record is added. Additionally, we'll cover how to create the SharePoint list and submit records from Power Apps.

---

## Prerequisites

Before you start, ensure you have the following:
1. **SharePoint**: Access to SharePoint Online to create lists.
2. **Power Apps**: The **Power Apps** mobile app installed on your device.
3. **Power Automate**: Access to **Power Automate** to create the notifications.


---

## Step 1: Create a SharePoint List

### 1. Create a SharePoint List
1. **Go to SharePoint**:
   - Navigate to your **SharePoint site** where you want to create the list.
   - Click the **Settings Gear** in the top-right corner, then select **Site contents**.

2. **Create a New List**:
   - In **Site contents**, click the **New** dropdown and select **List**.
   - Choose **Blank list** and name it (e.g., **Tasks**, **Orders**, **Contacts**).
   - Optionally, add a description and click **Create**.

3. **Add Columns to the List**:
   - After creating the list, add columns for the data you want to capture. For example, for a **Tasks** list, you might add the following columns:
     - **Title** (Single line of text) – Default column
     - **Description** (Multiple lines of text)
     - **Due Date** (Date and Time)
     - **Priority** (Choice: High, Medium, Low)

4. **Save the List**:
   - Your list is now ready to use. You can manually add items or connect it to Power Apps for submitting records.

---

## Step 2: Create a Canvas App in Power Apps

### 1. Open Power Apps Studio
   - Go to [Power Apps Studio](https://make.powerapps.com) and sign in.
   - Select **Apps** from the left navigation pane.
   - Create a new **Canvas App**.

### 2. Connect Your App to the SharePoint List
   - In the app editor, go to the **Data** pane on the left.
   - Click **Add Data** and select **SharePoint**.
   - Choose the **SharePoint list** you created earlier (e.g., **Tasks**, **Orders**, **Contacts**).

### 3. Add a Form to Submit New Items to the SharePoint List (optional - you can add records directly to the list if you want to skip this step :) )
   - **Insert an Edit Form**:
     - Go to **Insert** > **Forms** > **Edit Form** to add a form to the screen.
     - Set the **DataSource** property of the form to the SharePoint list you connected:
       ```powerapps
       DataSource = SharePointListName // Replace 'SharePointListName' with your actual list name
       ```

   - **Configure the Form**:
     - Set the form's **Item** property to `Defaults(SharePointListName)` to allow adding new records:
       ```powerapps
       Item = Defaults(SharePointListName)
       ```
     - In the form’s fields, make sure the necessary columns (e.g., **Title**, **Description**, **Due Date**, etc.) are selected for input.

### 4. Add a Button to Submit the Form
   - **Insert a Button**:
     - Go to **Insert** > **Button** and add a button below the form. Set the button text to "Submit".
     - Set the **OnSelect** property of the button to submit the form:
       ```powerapps
       OnSelect = SubmitForm(EditForm1) // Assuming your form is named EditForm1
       ```

   - **Optional: Add Notifications**:
     - You can notify the user that the record has been successfully submitted using the `Notify` function. Add the following to the button’s **OnSelect** property, after the `SubmitForm` action:
       ```powerapps
       OnSelect = SubmitForm(EditForm1); Notify("Record submitted successfully", NotificationType.Success)
       ```

### 5. Save and Publish the App
   - Save the app and publish it so that mobile users can access it on the **Power Apps mobile app**.

---

## Step 3: Create a Power Automate Flow for Push Notifications

### 1. Open Power Automate
   - Go to [Power Automate](https://flow.microsoft.com) and sign in.

### 2. Create a New Automated Flow
   - Click **Create** and choose **Automated Flow**.
   - Name the flow (e.g., "Send Push Notification on New SharePoint Item").
   - Select **SharePoint** as the trigger and choose the **When an item is created** trigger.

### 3. Configure the SharePoint Trigger
   - In the **Site Address**, select the SharePoint site that contains the list.
   - In the **List Name**, select the SharePoint list you want to monitor (e.g., **Tasks**, **Orders**, **Contacts**).

### 4. Add an Action to Send a Push Notification
   - After configuring the trigger, click **New Step**.
   - Search for **Power Apps Notification** and select the **Send push notification (V2)** action.
![Alt text](https://github.com/user-attachments/assets/453dfcdf-9b0f-452a-ad4c-d092f920960c)


### 5. Configure the Push Notification
- Set the **Mobile App** to **Power Apps**,
- Set the **Your App** to the app that will trigger notifications,
- Set the **Recipients Item - 1** to **Created by Email** 
   - Set the **Message** to whatever message you'd like to display in the push notification eg. **New form submitted**
   - Set the **Open App** to **No**
   - 
   Use **dynamic content** from the SharePoint list (like `Title`, `Description`, etc.) in the notification body.

### 6. Send the Notification to Power Apps Users
   - In the **Recipient User** field, enter the emails of the users who should receive the notification.
   - You can specify users directly or choose dynamic content based on user roles or fields.

### 7. Save and Test the Flow
   - Save the flow and test it by adding a new item to the SharePoint list. Check if the specified users receive the push notification on their mobile devices.

---

## Step 4: Test Push Notifications

### 1. Open the app on your Mobile Device
   - Open the **Power Apps** mobile app on your device.
   - Sign in with the same account you used in Power Apps Studio.

### 2. Add a new item using the Power Apps Form
   - Use the form in the Power Apps app to submit a new item to the SharePoint list (e.g., create a new task or order).

### 3. Receive the Push Notification
   - After submitting the new item, you should receive a push notification on your mobile device.
   - The notification will display the **title** and **body** as configured in the Power Automate flow, notifying you about the newly added item.

---

## Step 5: Customize the Push Notification Flow (Optional)

### 1. Add Conditions to the Flow
   - You can add conditions to the Power Automate flow to send notifications only when certain criteria are met. For example, you can send notifications only when a task is marked as "High Priority."
   - To add a condition, use the **Condition** action after the SharePoint trigger and define your logic.

### 2. Notify a Specific Group of Users
   - Instead of notifying all users, you can specify groups based on the SharePoint list metadata or user roles. For example, notify only the **Sales Team** when a new order is created.
   - Use **dynamic content** or filters based on your SharePoint list setup.

---

## Summary

By following these steps, you will be able to:
- Create and connect a **SharePoint list** to Power Apps.
- Submit new records to the SharePoint list using a form in Power Apps.
- Trigger **push notifications** to mobile users when a new item is added to a SharePoint list using **Power Automate**.

This setup is useful in scenarios such as task management apps, order tracking apps, or approval workflows where users need immediate notifications when important events occur.
