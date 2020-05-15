### [&laquo; Home](README.md)
## Dokumentasi PMB H2H STIE Assholeh dengan BPD Jateng

* [Authentication](#authentication)
* [Inquiry Data Tagihan](#inquiri)
* [Pembayaran Data Tagihan](#pembayaran)
* [Reversal](#reversal)

#### Production URL
````sh
https://api.stie-assholeh.ac.id/v1
````

#### Development URL
````sh
https://api.stie-assholeh.ac.id/dev
````

## Authentication
Mendapatkan token untuk setiap permintaan ke server. Tidak dapat digunakan dengan Development URL.

#### Method
  _GET_

#### End Point
  _/token_

#### Parameters
None

#### POST request data
None

#### Contoh Request
````sh
curl -u username:password https://api.stie-assholeh.ac.id/v1/token

````

#### Contoh Response
Success response:
````json
{
  "status":"OK",
  "auth-key": "U8Ch2LigkVhdI3XwYRA"
}
````


## Inquiry Data Tagihan
Mendapatkan data tagihan calon mahasiswa

### Semua Data Tagihan
#### Method
  _GET_

#### End Point
  _/pmb_

#### HTTPHEADER
  _"Authorization:token"_

#### Parameters
None

#### Contoh Request
````php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://www.api.stie-assholeh.ac.id/dev/pmb",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "Authorization: tokenkey-get-from-auth"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

````

#### Contoh Response
Success response:
````json
{
    "status": "OK",
    "calon_mahasiswa": [
        {
            "nim": "14052011001",
            "nama": "DONI DAMARA",
            "fakultas": "",
            "jurusan": "D3 MANAJEMEN PERUSAHAAN",
            "angkatan": "2020",
            "telp": "62834542222",
            "whatsapp": "62834542222",
            "tagihan": [
                {
                    "kode_tagihan": "B1001",
                    "nama_tagihan": "Biaya Daftar Ulang",
                    "amount": 200001
                }
            ]
        },
        {
            "nim": "14052022002",
            "nama": "LINA ASTUTI",
            "fakultas": "",
            "jurusan": "D3 MANAJEMEN PERUSAHAAN",
            "angkatan": "2020",
            "telp": "62834542222",
            "whatsapp": "62834542222",
            "tagihan": [
                {
                    "kode_tagihan": "B1002",
                    "nama_tagihan": "Biaya Daftar Ulang",
                    "amount": 200002
                }
            ]
        }
    ],
    "response_code": "00",
    "response_code_desc": "NIM Ditemukan"
}
````

Failed response:
````json
{
    "status": "ERROR",
    "message": "API Key tidak ditemukan",
    "response_code": "96",
    "response_code_desc": "Unspesific Error"
}
````

### Data Tagihan Per Calon Mahasiswa
#### Method
  _GET_

#### End Point
  _/pmb/:nim_

#### HTTPHEADER
  _"Authorization:token"_

#### Parameters
None

#### Contoh Request
````php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://www.api.stie-assholeh.ac.id/dev/pmb/14052011001",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => array(
    "Authorization: tokenkey-get-from-auth"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

````

#### Contoh Response
Success response:
````json
{
    "status": "OK",
    "nim": "14052011001",
    "nama": "DONI DAMARA",
    "fakultas": "",
    "jurusan": "D3 MANAJEMEN PERUSAHAAN",
    "angkatan": "2020",
    "telp": "6.28577E+11",
    "whatsapp": "62834542222",
    "tagihan": [
        {
            "kode_tagihan": "B1001",
            "nama_tagihan": "Biaya Daftar Ulang",
            "amount": 200001
        }
    ],
    "response_code": "00",
    "response_code_desc": "NIM Ditemukan"
}
````

Failed response:
````json
{
    "status": "ERROR",
    "message": "API Key tidak ditemukan",
    "response_code": "96",
    "response_code_desc": "Unspesific Error"
}
````


## Pembayaran Tagihan
Menyimpan data pembayaran calon mahasiswa

### Semua Data Tagihan
#### Method
  _PUT_

#### End Point
  _/pmb_

#### HTTPHEADER
  _"Authorization:token"_

#### Parameters
+ `nim`: nim/ kode pendaftaran. numerik.
+ `bank`: kode bank pengirim
+ `tgl_transaksi`: tanggal transaksi. terdiri dari yyyymmdd
+ `channel`: channel pembayaran
+ `device`: device
+ `noreff`: nomor referensi pembayaran. harus unik.
+ `bayar` : jenis pembayaran, bisa lebih dari 1 jenis pembayaran
    + `kode_tagihan`: kode tagihan
    + `amount`: nominal yang dibayarkan

#### Contoh Request
````php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://www.api.stie-assholeh.ac.id/v1/pmb",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "PUT",
  CURLOPT_POSTFIELDS => "{nim: 123456789,bank: 113,tgl_transaksi: 20160722,channel: 6010,device: W099001,noreff: t4512fg78r,bayar: [{kode_tagihan: A1,amount: 3000000}, {kode_tagihan: A2,amount: 1500000}]}",
  CURLOPT_HTTPHEADER => array(
    "Authorization: tokenkey-get-from-auth",
    "Content-Type: application/x-www-form-urlencoded"
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

````

#### Contoh Response
Success response:
````json
{
    "status": "OK",
    "nim": "12013011003",
    "response_code": "00",
    "response_code_desc": "Posting Berhasil"
}
````

Failed response:
````json
{
    "status": "ERROR",
    "message": "Data tidak ditemukan",
    "response_code": "24",
    "response_code_desc": "NIM & Data Tagihan Tidak Ditemukan"
}
````
