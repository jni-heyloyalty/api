# Update custom field last login on member

!! warning we are using Guzzle http client version 3.8 </br>
Guzzle is constant changing the way you instatiate the object, so be sure to look at the guzzle documentation.</br>
In this example we are showing how you can update your own "last login" custom date field, if you need to keep track of things.<br/>
Remember you can set the date format when you create or edit a list, if you what to set hours, minutes and seconds, just set the format as YYYY-mm-dd H.i:s
this wil give you a format of 1970-12-31 12:00:00

```
 <?php
        use GuzzleHttp\Client;
        
        define('API_KEY', 'xxxxxxxxxxxxxxxxxxx');
        define('API_SECRET', 'xxxxxxxxxxxxxxxxxxxxxxxxxxxx');
        
        $client = new Client();
        
        $host = 'https://api.heyloyalty.com';
        
        $requestTimestamp = gmdate("D, d M Y H:i:s") . ' GMT';
        
        $requestSignature = base64_encode(hash_hmac('sha256', $requestTimestamp, API_SECRET));
        
        $request = $client->put($host.'/loyalty/v1/lists/1/members/ad7b7fb6-5f0b-457a-82f9-0ea186ead40e/?email=johndoe@mail.com&firstname=John&lastlogin=1970-01-01');
        
        $request->setAuth(API_KEY, $requestSignature);
        
        $request->addHeader('X-Request-Timestamp', $requestTimestamp);
        
        $response = $request->send()->json();
        
        var_dump($response);
    ?>
```
