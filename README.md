# pesapalandroid
Pesapal Android SDK
This is the official Pesapal Plugin For Android The following steps will guide you on how to use the Plugin

Setup Merchnat 
    Before you can start processing payments through Pesapal, you need to setup a Merchant Account on pesapal.com We provide a test bed on demo.pesapal.com where you can setup a test merchant and get test credentials
    To set up the test credentials for the app, Invoke the plugins settings activity which will load a form that takes the credentials

Example for invoking the Plugins Settings Activity, 
  Note that Activity is Started for Result 
  ComponentName cn = new ComponentName(mContext, “com.pesapal.pesapalandroid.PesapalSettingsActivity”); 
  Intent intent = new Intent().setComponent(cn); intent.putExtra(“pkg”,”com.pesapal”); //your application package.
  startActivityForResult(intent,SETTINGS_ACTIVITY_REQUEST_CODE);

Once Merchant Is setup, you can then create a Payment object and pass it to the Plugins Payments Activity for Processing
NOTE: Payments returns a uniqueId, method of payment, status of payment…as a comma seperated string in that order. 
You can use the unique Id to query for the final status incase status returned initially is PENDINg 
Example for invoking Plugins Payments Activity 
Payment payment = new Payment(); 
payment.setAmount(100.00); 
payment.setDescription(“test_payment”); 
payment.setEmail(“johndoe@test.com”); 
payment.setCurrency(“KES”); 
//payment.setFirstName(“John”); 
//payment.setLastName(“Doe”); 
payment.setPhoneNumber(“0000000000”); 
ComponentName cn = new ComponentName(mContext, “com.pesapal.pesapalandroid.PesapalPayActivity”); 
Intent intent = new Intent().setComponent(cn); intent.putExtra(“payment”,payment); startActivityForResult(intent,PAYMENT_ACTIVITY_REQUEST_CODE)
