# Push Notifications in Power Apps (Canvas Apps) with SharePoint List

In this exercise, you'll learn how to send **push notifications** to mobile users in a Power Apps canvas app when a new item is added to a **SharePoint list**. We will use **Power Automate** to trigger the push notifications.

---

## Prerequisites

Before you start, ensure you have the following:
1. **SharePoint**: A SharePoint list set up (e.g., **Tasks**, **Orders**, **Contacts**, etc.).
2. **Power Apps**: The **Power Apps** mobile app installed on your device.
3. **Power Automate**: Access to **Power Automate** to create the automation flow for notifications.
4. **Power Automate License**: Ensure you have the necessary licensing for Power Automate to use push notifications.

---

## Step 1: Create a Canvas App in Power Apps

1. **Open Power Apps Studio**:
   - Go to [Power Apps Studio](https://make.powerapps.com) and sign in.
   - Select **Apps** from the left navigation pane.
   - Create a new **Canvas App** with the layout of your choice (either **Tablet** or **Phone**).

2. **Connect Your App to a SharePoint List**:
   - In the app editor, go to the **Data** pane on the left.
   - Click **Add Data** and select **SharePoint**.
   - Choose the **SharePoint list** you want to monitor for new items (e.g., **Tasks**, **Orders**, **Contacts**, or a custom list).

3. **Create a Simple Interface (Optional)**:
   - Add a **Gallery** control to display the list items from the SharePoint list.
   - Set the **Items** property of the gallery to show items from your SharePoint list:
     ```powerapps
     Items = SharePointListName // Replace 'SharePointListName' with the actual name of your list
     ```

4. **Save and Publish the App**:
   - Save the app and publish it so that mobile users can access it on the **Power Apps mobile app**.

---

## Step 2: Create a Power Automate Flow for Push Notifications

1. **Open Power Automate**:
   - Go to [Power Automate](https://flow.microsoft.com) and sign in.

2. **Create a New Automated Flow**:
   - Click **Create** and choose **Automated Flow**.
   - Name the flow (e.g., "Send Push Notification on New SharePoint Item").
   - Select **SharePoint** as the trigger and choose the **When an item is created** trigger.

3. **Configure the SharePoint Trigger**:
   - In the **Site Address**, select the SharePoint site that contains the list.
   - In the **List Name**, select the SharePoint list you want to monitor (e.g., **Tasks**, **Orders**, **Contacts**).

4. **Add an Action to Send a Push Notification**:
   - After configuring the trigger, click **New Step**.
   - Search for **Power Apps Notification** and select the **Send a push notification** action.

5. **Configure the Push Notification**:
   - Set the **Notification Title** and **Notification Body** to provide relevant information about the newly added item.
   
   Example:
   - **Notification Title**: `"New Task Added!"` or `"New Order Created!"`
   - **Notification Body**: `"A new task, titled '" & Title & "' has been added to the task list."`
   
   Use **dynamic content** from the SharePoint list (like `Title`, `Description`, etc.) in the notification body.

6. **Send the Notification to Power Apps Users**:
   - In the **Recipient User** field, enter the emails of the users who should receive the notification.
   - You can specify users directly or choose dynamic content based on user roles or fields.

7. **Save and Test the Flow**:
   - Save the flow and test it by adding a new item to the SharePoint list. Check if the specified users receive the push notification on their mobile devices.

---

## Step 3: Test Push Notifications

1. **Open the App on Your Mobile Device**:
   - Open the **Power Apps** mobile app on your device.
   - Sign in with the same account you used in Power Apps Studio.

2. **Add a New Item to the SharePoint List**:
   - Go to your SharePoint list and add a new item (e.g., create a new task or order).
   
3. **Receive the Push Notification**:
   - After adding the new item, you should receive a push notification on your mobile device.
   - The notification will display the **title** and **body** as configured in the Power Automate flow, notifying you about the newly added item.

---

## Step 4: Customize the Push Notification Flow (Optional)

1. **Add Conditions to the Flow**:
   - You can add conditions to the Power Automate flow to send notifications only when certain criteria are met. For example, you can send notifications only when a task is marked as "High Priority."
   - To add a condition, use the **Condition** action after the SharePoint trigger and define your logic.

2. **Notify a Specific Group of Users**:
   - Instead of notifying all users, you can specify groups based on the SharePoint list metadata or user roles. For example, notify only the **Sales Team** when a new order is created.
   - Use **dynamic content** or filters based on your SharePoint list setup.

---

## Step 5: Manage Notifications in the App (Optional)

1. **Create a Notifications Screen**:
   - Add a new screen in the Power Apps app to act as a "Notification Center" where users can see recent updates.
   - Add a **Gallery** or **Data Table** that displays relevant records from the SharePoint list that triggered the notifications.

2. **Track Notification Logs (Optional)**:
   - Store notification logs in a SharePoint list or another data source and display them in the Power Apps app to provide users with a history of their notifications.

---

## Summary

By following these steps, you will be able to:
- Trigger **push notifications** to mobile users when a new item is added to a SharePoint list.
- Use **Power Automate** to create and configure push notification flows.
- Ensure that users receive real-time updates directly through the Power Apps mobile app.

This setup is useful in many scenarios, such as task management apps, order tracking apps, or approval workflows, where users need immediate notifications when important events occur.

