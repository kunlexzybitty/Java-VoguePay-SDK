# Java-VoguePay-SDK
Java library for VoguePay

<p>Installation Process</p>
Import jar file to your project

<p>Then include it in your project source code</p>
<div>
    <pre>
    import com.kunlexzy.voguepaysdk.*;
    </pre>
</div>

<div>
    <p>There are 3 operations available</p>
    <pre>
    1. Hosted Payment (Payment link)
    2. Direct Payment (whitelabel)
    3. Query Transaction
    </pre>
</div>

<div>
Using the Java Library
<div>
    <h3>Hosted Payment (Payment link)</h3>
    <a href="https://voguepay.com/documentation#section-six" rel="nofollow">Demo card details</a> and <a href="https://voguepay.com/documentation" rel="nofollow">Documentation</a>
</div>
<pre>
  
    //Create voguepay instance with voguepay details
        Voguepay voguepayObj=new Voguepay("MERCHANTID","USERNAME","EMAIL");
        voguepayObj.setCommandAPIToken("5W4HPqyhfTDgna78jnPdTnAh22"); //Generate one in account settings
        voguepayObj.setPublicKeyPath("c://key.txt"); //Generate one in account settings and save to a file on your system, ensure its readable
        voguepayObj.setMode("live"); //demo or live mode
        
        Customer customerObj = new Customer();
        customerObj.Name="Fries Segun";
        customerObj.Address="33a abba johnson";
        customerObj.CountryISO3="NGA";
        customerObj.Email="customer@gmail.com";
        customerObj.Phone="04444";
        customerObj.State="Lagos";
        customerObj.City="Ikeja";
        customerObj.ZipCode="23401";
        voguepayObj.setCustomer(customerObj);
       
        
        voguepayObj.memo="Payment for shoes";
        voguepayObj.amount=20;
        voguepayObj.storeID="5a3644ba2c"; //Optional
        voguepayObj.currencyISO3="USD";
        voguepayObj.reference="23444"; //Replace with your unique reference for this transaction
      
        voguepayObj.callbackUrl="https://domain.com/callback";
        voguepayObj.successUrl="https://domain.com/success";
        voguepayObj.failUrl="https://domain.com/fail";
        
        System.out.println(voguepayObj.GeneratePayLink());
        

    
</pre>

<div>
Sample Responses
</div>
<pre>
{"status": "ERROR","message": "Unable to process command"}

  
  {"status": true,"message": "Redirection required","URL": "https://voguepay.com/pay/bnlink/1560713945-x0"}
</pre>



<div>
    <h3>Direct Payment (whitelabel)</h3>
    <a href="https://voguepay.com/documentation#section-six" rel="nofollow">Demo card details</a> and <a href="https://voguepay.com/whitelabel" rel="nofollow">Documentation</a>
</div>
<pre>
   //Create voguepay merchant instance
   Merchant merchantinfo = new Merchant();
   merchantinfo.MerchantID = "6359-0000000";
   merchantinfo.Username = "username";
   merchantinfo.Email = "sample@gmail.com";
   merchantinfo.CommandAPIToken = "ZnHzcbxKVbvF5d3J5JvZqZe587Rna";
   merchantinfo.PublicKeyFile = @"C:\Users\Rock\public.txt"; //URL path to saved public key
    
    //Create voguepay instance (Parameters "live" or "demo", default is demo)
    Voguepay voguepay = new Voguepay("live");
    voguepay.Init(merchantinfo);

    //Create customer instance
    Customerinfo customer = new Customerinfo();
    customer.Name = "Sam Great";
    customer.Phone = "20339922";
    customer.Email = "sample@yahoo.com";
    customer.City = "Allen";
    customer.Country = "NGA";
    customer.State = "Ikeja";
    customer.ZipCode = "23401";
    customer.Address = "3 Drive view estate";


    DirectPayment directpayment = new DirectPayment();
    directpayment.version = 2;
    directpayment.Amount = 100.22;
    directpayment.Currency = "USD";
    directpayment.Reference = "MY_UNIQUE_REF";
    directpayment.Memo = "Sample payment";
    directpayment.RedirectURL="https://sample.com/redirect";
    directpayment.ReferralURL="https://sample.com/referral";
    directpayment.ResponseURL="https://sample.com/notify/";
    directpayment.StoreID = "5a33c3933ca"; //optional

    directpayment.CardName = "Steve";
    directpayment.CardPan = "5389830123937029";
    directpayment.CardExpiryMonth = 5;
    directpayment.CardExpiryYear = 21;
    directpayment.CardCVV = 170;


    directpayment.ServerPublicIP= "192.333.44.33";
    directpayment.ServerWebsiteURL= "www.google.com";
    directpayment.CustomerReferringIP= "10.22.333.33";
    directpayment.CustomerReferringWebsite= "www.shades.com";

    directpayment.DescriptorCompanyName= "Sparks";
    directpayment.DescriptorCountryAddress= "Sparks Street";
    directpayment.DescriptorCityAddress= "Califonia";
    directpayment.DescriptorCountryAddress= "USA"; //country or 3 letter ISO
   // directpayment.CardToken = "5a344439203";
  //  directpayment.CardTokenize =true;
  
    string jsonResult = voguepay.Pay(directpayment, customer);
</pre>

<div>
Sample Responses
</div>
<pre>
{
  "merchant_ref":"MY_UNIQUE_REF",
  "field":"Card Year",
  "message":"Card provided has expired",
  "status":"ERROR",
  "response":"WL002",
  "salt":"5d06a1811caec",
  "hash":"421caed76f402bf27656297a1f03e62303d1e55d478e9bf5882b77561db47808ad765fc91cd1ed576524adb0ec091f7a07d349a70adce342efd6a72f34e55b10",
  "username":"username"
}
 
  
  { 
    "merchant_ref":"MY_UNIQUE_REF",
    "status":"OK",
    "response":"WL3D",
    "message":"3D Authorization required",
    "reference":"5d069f1d3ed98",
    "redirect_url":"https://voguepay.com/?p=vpgate&ref=czoxMzoiNWQwNjlmMWQzZWQ5OCI7",
    "salt":"5d069f1d399e5",
    "hash":"7d3d2e64dcba9f95bfc705721f9367923139ab752d01a453456ee0bf5a15f9bd069f14c8c9faac018f4cd1dc57760d37b17820f13586da95070ec1dd5268b8b1",
    username":"username"
 }
</pre>

<div>
    <h3>Query Transaction</h3>
     <a href="https://voguepay.com/documentation#section-five" rel="nofollow">Documentation</a>
</div>
<pre>
   //Create voguepay merchant instance
    Merchant merchantinfo = new Merchant();
    merchantinfo.MerchantID = "6359-0000000";
    merchantinfo.Username = "username";
    merchantinfo.Email = "sample@gmail.com";
    merchantinfo.CommandAPIToken = "ZnHzcbxKVbvF5d3J5JvZqZe587Rna";
    
    //Create voguepay instance (Parameters "live" or "demo", default is demo)
    Voguepay voguepay = new Voguepay("live");
    voguepay.Init(merchantinfo);
    
    //Query Transaction
    Transaction transaction = new Transaction();
    transaction.TransactionID= "5d041a2843bd8";
    string jsonResult = voguepay.Query(transaction);
</pre>

<div>
Sample Responses
</div>
<pre>

{
    "status":"OK",
    "response":"OK",
    "transaction":
        {
            "ERROR":"UNRECOGNISED TRANSACTION ID.",
            "process_duration":0.054308
        },
    "salt":"5d06a664aa71e",
    "hash":"b5c7e52c6db1191ccb04d365d15eaf2ae3a0efa027921839f778ee44207b300ce2f1848e330e9029245b16d6df84d4e0e99df892d1a9501f68cf55ba1cfb1dad",
    "username":"username"
 }


{
    "status":"OK",
    "response":"OK",
    "transaction":
       {
           "cur":"$",
           "transaction_id":"5d541a2813bd8",
           "email":"sample@yahoo.com",
           "total_amount":"100.2200",
           "total":"100.22",
           "merchant_ref":"MY_UNIQUE_REF",
           "memo":"Sample payment",
           "status":"Approved",
           "date":"2019-06-14 23:05:28",
           "method":"17",
           "referrer":"",
           "total_credited_to_merchant":"98.72",
           "extra_charges_by_merchant":"0",
           "charges_paid_by_merchant":"1.5",
           "fund_maturity":"2019-06-16",
           "buyer_phone":"07020339922",
           "response_code":"00",
           "response_message":"Transaction Approved",
           "masked_pan":"539983-7069-mastercard",
           "merchant_id":"6359-0000000",
           "total_paid_by_buyer":"100.22",
           "process_duration":0.021649
         },
       "salt":"5d06a4efb50fa",
       "hash":"c974dd9f6a75d1ec8d3cbcb015b0495bd4193c5b75153a43d9d1cc0b9e1cca9951836cfc111be26bc09131e70138258cc366b0961838716f5cc369818d577563",
       "username":"username"
   }
</pre>


