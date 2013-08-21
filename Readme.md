
## Install


```
pip install pesapal
pip install requests
```

## Example


```
import pesapal
import requests

consumer_key ='consumer_key'
consumer_secret = 'consumer_secret'
testing = False

### make client
client = pesapal.PesaPal(consumer_key, consumer_secret, testing)

### post a direct order

request_data = {
  'Amount': '',
  'Description': '',
  'Type': '',
  'Reference': '',
  'PhoneNumber': ''
}
post_params = {
  'oauth_callback': 'www.example.com/post_payment_page'
}
pesapal_request = client.postDirectOrder(post_params, request_data)
# get url to display as an iframe
print pesapal_request.to_url()

### get order status

params = {
  'pesapal_merchant_reference': '000',
  'pesapal_transaction_tracking_id': '000'
}
pesapal_request = client.queryPaymentStatus(params)
url = pesapal_request.to_url()
print url

r = requests.get(pesapal_request.to_url())
print r.text

### get order status by ref

params = {
  'pesapal_merchant_reference': '000'
}
pesapal_request = client.queryPaymentStatusByMerchantRef(params)
print pesapal_request.to_url()
r = requests.get(pesapal_request.to_url())
print r.text

### get detailed order status

params = {
  'pesapal_merchant_reference': '000',
  'pesapal_transaction_tracking_id': '000'
}
pesapal_request = client.queryPaymentDetails(params)
print pesapal_request.to_url()
r = requests.get(pesapal_request.to_url())
print r.text
```

## Api

### PesaPal(consumer_key, consumer_secret, testing)
  
  pass testing as true to use http://demo2.pesapal.com/api/ instead of https://www.pesapal.com/api/

### PesaPal#postDirectOrder(options)
  
  returns an oauth object

  options is a dictionary containing:

  - Amount
  - Description
  - Type
  - Reference
  - Email or/and PhoneNumber
  - Currency ( optional )
  - FirstName ( optional )
  - LastName ( optional )
  - LineItems ( optional )

### PesaPal#queryPaymentStatus(options)

  returns an oauth object

  options is a dictionary containing:

  - pesapal_merchant_reference
  - pesapal_transaction_tracking_id

### PesaPal#queryPaymentStatusByMerchantRef(options)

  returns an oauth object

  options is a dictionary containing:
  
  - pesapal_merchant_reference

### PesaPal#queryPaymentDetails(options)

  returns an oauth object

  options is a dictionary containing:

  - pesapal_merchant_reference
  - pesapal_transaction_tracking_id

## Test

    $ make deps test

## License

MIT
