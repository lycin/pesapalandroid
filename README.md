# Introduction
This is the official Pesapal Plugin For Android, developed by Pesapal

Integrating Pesapal is now as easy as plug and play. 

# Requirement
You need Merchant Oauth Keys from Pesapal for the API. 

On Demo Pesapal, you can get these credentials on the dashboard when you are logged in

On Pesapal Live, you email these information from the dashboard when you are logged in

Once you are live, we require you to setup the following Instant Payment Notification URL under `IPN Settings in your Merchant dashboard`

> http://sdk.pesapal.com/ipn

# Installation
## Gradle
compile 'com.pesapal.android:pesapalandroid:1.0.5'
## Maven
```
<dependency>
  <groupId>com.pesapal.android</groupId>
  <artifactId>pesapalandroid</artifactId>
  <version>1.0.5</version>
  <type>pom</type>
</dependency>
```

# How it works
- Install the plugin
- Setup Merchant Credentials by calling the plugins Settings Activity. See an example below
- On Successful setup, A merchant unique ID is returned. Add a Meta Data in your manifest as follows 
  ```
  <meta-data android:name="string"
           android:resource="com.pesapal.pesapalandroid.MERCHANT_ID"
           android:value="ID Returned Above" />```
- On Unsuccessful setup, the settings activity returns to the calling activity with the error message that you can access as `String error = data.getStringExtra("error");`
- To make a payment, pass a payments object to the Plugins Payments Activity. See example below. 
- On successful payment, The plugin returns a payments string to the calling activity, that you should capture on `onActivityResult`. The payment string is comma separated that contains a unique payment ID, method of payment, `e.g MPESA`,status of the payment `e.g COMPLETED, PENDING, FAILED`, and amount processed 
- The only failure returned from the payments activity to the calling activity is Result Cancelled.
- To check the final status on Pesapal for Pending payments, Query the plugins check status function, passing the unique payment ID. See example

# Testing
We provide a test bed at [Demo Pesapal](https://demo.pesapal.com/), where you can get demo credentials for testing.

To test, set Demo on The Plugins Settings Page

# Going Live
- Your journey starts here [Pesapal, Business Account] (https://www.pesapal.com/business)
- Create a business account
- Sign your contract with Pesapal. You may transact before a contract but do note that you will have a very low amount limit for a transaction, and you will not be able to withdraw your money
- Got the contract?, good. If your merchant credentials have not been emailed yet, Log into your account on Pesapal, send yourself a copy

# Examples

## Settings
Start the Settings activity. Note that you are passing the package name to the Settings Activity
- On Success, return Unique Merchant ID for setup in your manifest. 
- On failed, returns error message to be captured on ActivityResult

```

ComponentName cn = new ComponentName(this, "com.pesapal.pesapalandroid.PesapalSettingsActivity");

Intent intent = new Intent().setComponent(cn);

intent.putExtra("pkg","your package name");

startActivityForResult(intent,SETTINGS_ACTIVITY_REQUEST_CODE);
```

## Payment
- Create a payment object
- Pass the payment object as an extra to the Libraries Payments Activity
- Refer to How it works on how to capture the payments result

```

Payment payment = new Payment();

payment.setAmount(100.00);

payment.setAccount("just extra info, e.g dstv account number, order id");

payment.setDescription("test_payment");

payment.setEmail("xxx@xxx.com");

payment.setCurrency("KES");

payment.setFirstName("Jane");

payment.setLastName("Doe");

payment.setPhoneNumber("07XXXXXXXX");

ComponentName cn = new ComponentName(this, "com.pesapal.pesapalandroid.PesapalPayActivity");

Intent intent = new Intent().setComponent(cn);

intent.putExtra("payment",payment);

startActivityForResult(intent,PAYMENT_ACTIVITY_REQUEST_CODE);
                
```

## Check Status
- Use the Payment ID returned from Payments activity to get status
- This is a network operation and therefore should be run in the background

`String status = Payment.checkStatus("f9e8f92d-c0fa-423d-8e53-d889955e1e4c");`





