## Dokumentasi H2H STIE Assholeh dengan BPD Jateng

[Authentication](#authentication)
[Inquiry Data Tagihan](#inquiri)
[Pembayaran Data Tagihan](#pembayaran)
[Reversal](#reversal)

#### Production URL
+ [https://api.stie-assholeh.ac.id/v1]

#### Development URL
+ [https://api.stie-assholeh.ac.id/dev]


## Authentication

### Authenticate
Mendapatkan token untuk setiap permintaan ke server. Tidak dapat digunakan dengan Development URL.

+ Use `POST` http method.

##### End Point
+ [/token]()

##### Parameters
None

##### POST request data
None

##### Example Request
````sh
curl -u billy:Highs3creT https://api.bukalapak.com/v2/authenticate.json -X POST

````

##### Example Response
Success response:
````json
{
  "status":"OK",
  "user_id": "157324",
  "token": "U8Ch2LigkVhdI3XwYRA",
  "message":null
}
````

Failed response
````json
{
  "status":"ERROR",
  "user_id":"null",
  "message":"Invalid password"
}
````
