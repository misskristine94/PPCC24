# Exercise: Configuring Dataverse Offline Capability and Testing in Canvas App (Part 1)

## Objective
To configure the Dataverse offline capability in a Canvas app and test its functionality.

## Prerequisites
- Access to Power Apps Studio.
- A Dataverse environment.
- Basic understanding of creating and editing Canvas apps.

---

## Steps

### 1. Create a Dataverse Table
1. Open **Power Apps Studio**.
2. In the left-hand navigation pane, click on **Dataverse**.
3. Click on **Tables**.
4. Click on the **New table** button at the top.
5. In the **Display name** field, enter `Customer Orders`.
6. Click on **Create**.
7. In the table designer, click on **+ Add column**.
8. Add the following columns:
   - **Order ID**:
     - **Display name**: Order ID
     - **Data type**: Text
     - Click **Done**.
   - **Customer Name**:
     - **Display name**: Customer Name
     - **Data type**: Text
     - Click **Done**.
   - **Order Date**:
     - **Display name**: Order Date
     - **Data type**: Date Only
     - Click **Done**.
   - **Order Status**:
     - **Display name**: Order Status
     - **Data type**: Choice
     - Click on **+ New choice**.
     - Enter the following choices: Pending, Shipped, Delivered.
     - Click **Save**.
     - Click **Done**.
   - **Order Total**:
     - **Display name**: Order Total
     - **Data type**: Currency
     - Click **Done**.
9. Click on **Save table**.

### 2. Enable Offline Capability for the Table
1. In the table designer, click on the **Settings** tab.
2. Scroll down to the **Offline** section.
3. Check the box labeled **Can be taken offline**.
4. Click **Save**.


### 3. Create a Canvas App
1. In Power Apps Studio, click on **Create** in the left-hand navigation pane.
2. Select **Canvas app**.
3. Choose **Tablet** or **Phone** layout.
4. Click on **Create**.
5. In the app designer, click on **Data** in the left-hand navigation pane.
6. Click on **+ Add data**.
7. Select **Dataverse**.
8. Search for and select the `Customer Orders` table.
9. Click **Connect**.


### 4. Enable Offline Mode in the Canvas App
1. In the app designer, click on **Settings** in the top-right corner.
2. Click on **General**.
3. Scroll down to the **Offline** section.
4. Turn on the **Can be used offline** option.
5. Click **Save**.

### 5. Insert an Offline Status Indicator
1. In the app designer, click on **Insert** in the left-hand navigation pane.
2. Select **Label** or **Icon**.
3. Place the label or icon on the screen.
4. With the label or icon selected, go to the **Properties** pane on the right.
5. Set the **Text** property (for a label) or **OnSelect** property (for an icon) to the following formula:
   ```plaintext
   If(Connection.Connected, "Online", "Offline")



### 6. Test the Offline Capability
1. Open the app on a mobile device using Power Apps Mobile.
2. Turn off the internet connection on the device.
3. Verify that the app displays the offline status and allows data entry.
4. Reconnect to the internet and ensure that the data syncs with Dataverse.


---

## Expected Outcome
The Canvas app should function offline and sync it with Dataverse once the connection is restored.

If you have any questions or need further assistance, let me know!


## Part 2: Testing Dataverse by Submitting a Form

### Steps

#### 1. Add a Form to the Canvas App
1. Open **Power Apps Studio**.
2. Open the Canvas app you created in Part 1.
3. In the left-hand navigation pane, click on **Insert**.
4. Select **Forms** and then **Edit Form**.
5. Place the form on the screen.
6. In the **Properties** pane on the right, set the **Data source** to `Customer Orders`.
7. Set the **Item** property to `Defaults(CustomerOrders)`.

!Add Form

#### 2. Customize the Form Fields
1. With the form selected, click on **Edit fields** in the **Properties** pane.
2. Click on **+ Add field**.
3. Select the following fields and click **Add**:
   - `Order ID`
   - `Customer Name`
   - `Order Date`
   - `Order Status`
   - `Order Total`
4. Click **Done**.

!Customize Form Fields

#### 3. Add a Submit Button
1. In the left-hand navigation pane, click on **Insert**.
2. Select **Button**.
3. Place the button below the form.
4. Set the **Text** property of the button to `Submit`.
5. Set the **OnSelect** property of the button to the following formula:
   ```plaintext
   SubmitForm(EditForm1)

#### 4. Test the Form Submission
Save and publish the app.
Open the app on a mobile device using Power Apps Mobile.
Fill out the form with sample data.
Click the Submit button.
Verify that the data is saved locally when offline.
Reconnect to the internet and ensure that the data syncs with Dataverse.
!Test Form Submission

#### 5. Verify Data Synchronization
Open Power Apps Studio.
Navigate to Dataverse > Tables.
Open the Customer Orders table.
Verify that the submitted data appears in the table.





