# Exercise: Configuring Dataverse Offline Capability and Testing in Canvas App

## Objective
To configure the Dataverse offline capability in a Canvas app and test its functionality.

## Prerequisites
- Access to Power Apps Studio.
- A Dataverse environment.

---

## Steps

### 1. Create a Dataverse Table
1. Open Power Apps Studio.
2. Navigate to **Dataverse** > **Tables**.
3. Click on **New table**.
4. Name the table `Customer Orders`.
5. Add the following columns:
   - `Order ID` (Single-line text)
   - `Customer Name` (Single-line text)
   - `Order Date` (Date only)
   - `Order Status` (Choice: Pending, Shipped, Delivered)
   - `Order Total` (Currency)
6. Populate the table with sample data.


### 2. Enable Offline Capability for the Table
1. Open the properties of the `Customer Orders` table.
2. Check the box labeled **Can be taken offline**.
3. Click **Save**.


### 3. Create a Canvas App
1. In Power Apps Studio, select **Create an app**.
2. Choose **Canvas app** and select **Tablet** or **Phone** layout.
3. Select **Dataverse** as the data source and choose the `Customer Orders` table.
4. Click **Create**.


### 4. Enable Offline Mode in the Canvas App
1. Open the app in edit mode.
2. Go to **Settings** > **General**.
3. Turn on the **Can be used offline** option.
4. Save the app.


### 5. Insert an Offline Status Indicator
1. In the app, insert a label or icon to indicate the offline status.
2. Use the `Connection` signal object to determine the app's connectivity status.
3. Example formula for the label: `If(Connection.Connected, "Online", "Offline")`.


### 6. Test the Offline Capability
1. Open the app on a mobile device using Power Apps Mobile.
2. Turn off the internet connection on the device.
3. Verify that the app displays the offline status and allows data entry.
4. Reconnect to the internet and ensure that the data syncs with Dataverse.


---

## Expected Outcome
The Canvas app should function offline, allowing users to enter data and sync it with Dataverse once the connection is restored.

If you have any questions or need further assistance, let me know!
