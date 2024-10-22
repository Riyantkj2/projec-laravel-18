# Foobar

Foobar is a Python library for dealing with word pluralization.

## Installation

ini contoh input laravel ke 18.
cara belajar laravel

Agar lebih mudah dan paham tentang penjelasan cara membuat form validasi laravel ini.

Seperti biasa pertama kita akan membuat 2 buah route untuk membuat form inputan, dan route yang 1 laginya untuk membuat proses validasi dari form inputan yang dikirim.

belajar_laravel/routes/web.php
```bash
Route::get('/input', 'MalasngodingController@input');
Route::post('/proses', 'MalasngodingController@proses');
```
Selanjutnya kita buat controller ‘MalasngodingController’. sesuai dengan yang sudah kita buat pada route.

Untuk membuat controller pada laravel, kita bisa membuatnya secara manual dalam folder App/Http/controllers, atau membuat controller dengan php artisan melalui terminal atau cmd.
```bash
php artisan make:controller MalasngodingController


```

![image](https://github.com/user-attachments/assets/e56259d8-3bee-40a6-9554-428d214eb4da)

Setelah selesai membuat controller, sekarang kita buat 2 buah method, sesuai dengan yang telah kita buat pada route sebelumnya.

yaitu method input dan method proses.

Buka MalasngodingController.php nya, dan tulis syntax berikut.

belajar_laravel/app/Http/controllers/MalasngodingController.php
```bash
<?php
 
namespace App\Http\Controllers;
 
use Illuminate\Http\Request;
 
class MalasngodingController extends Controller
{
    public function input()
    {
        return view('input');
    }
 
    public function proses(Request $request)
    {
        $this->validate($request,[
           'nama' => 'required|min:5|max:20',
           'pekerjaan' => 'required',
           'usia' => 'required|numeric'
        ]);
 
        return view('proses',['data' => $request]);
    }
}

```
Pada method input() kita membuat sebuah view yang menampilkan form penginputan sederhana. dimana pada form tersebut akan kita arahkan pemproses nya pada method proses() menggunakan method post. seperti yang telah kita definisikan pada route.

Akan saya jelaskan lengkapnya setelah kita membuat view. pada method input() kita menampilkan view input.blade.php.
belajar_laravel/resources/views/input.blade.php
```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Malas Ngoding - Tutorial Laravel #18 : Membuat Form Validasi Pada Laravel</title>
 
    <!-- bootstrap -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css">
</head>
<body>
 
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-lg-6">
                    <div class="card mt-5">
                        <div class="card-body">
                            <h3 class="text-center">www.malasngoding.com</h3>
                            <br/>
 
                            {{-- menampilkan error validasi --}}
                            @if (count($errors) > 0)
                            <div class="alert alert-danger">
                                <ul>
                                    @foreach ($errors->all() as $error)
                                        <li>{{ $error }}</li>
                                    @endforeach
                                </ul>
                            </div>
                            @endif
 
                            <br/>
                             <!-- form validasi -->
                            <form action="/proses" method="post">
                                {{ csrf_field() }}
 
                                <div class="form-group">
                                    <label for="nama">Nama</label>
                                    <input class="form-control" type="text" name="nama" value="{{ old('nama') }}">
                                </div>
                                <div class="form-group">
                                    <label for="pekerjaan">Pekerjaan</label>
                                    <input class="form-control" type="text" name="pekerjaan" value="{{ old('pekerjaan') }}">
                                </div>
                                <div class="form-group">
                                    <label for="usia">Usia</label>
                                    <input class="form-control" type="text" name="usia" value="{{ old('usia') }}">
                                </div>
                                <div class="form-group">
                                    <input class="btn btn-primary" type="submit" value="Proses">
                                </div>
                            </form>
 
                        </div>
                    </div>
                </div>
            </div>
        </div>
   
</body>
</html>
```
kemudian pada form nama, kita buat juga validasi jumlah minimal karakter yang di input. dan jumlah maksimal. di sini kita menetapkan form nama minimal harus 5 karakter (min:5), dan maksimal 20 karakter (max:20).

Jika validasi berhasil, atau jika yang di input sesuai dengan pengaturan yang sudah kita tetapkan dalam fungsi validate() tadi, maka kita passing data yang di input oleh user ke view proses.blade.php.

belajar_laravel/resources/proses.blade.php
```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Malas Ngoding - Tutorial Laravel #18 : Membuat Form Validasi Pada Laravel</title>
    
    <!-- bootstrap -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css">
</head>
 
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-lg-6">
                <div class="card mt-5">
                    <div class="card-body">
                        <h3>www.malasngoding.com</h3>
                        <h3 class="my-4">Data Yang Di Input : </h3>
 
                        <table class="table table-bordered table-striped">
                            <tr>
                                <td style="width:150px">Nama</td>
                                <td>{{ $data->nama }}</td>
                            </tr>
                            <tr>
                                <td>Pekerjaan</td>
                                <td>{{ $data->pekerjaan }}</td>
                            </tr>
                            <tr>
                                <td>Usia</td>
                                <td>{{ $data->usia }}</td>
                            </tr>
                        </table>
 
                        <a href="/input" class="btn btn-primary">Kembali</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
 
</body>
</html>
```
Coba kita lihat hasilnya.

Jalankan project laravel kita.
```bash
php artisan serve
```
## ini contoh proses laravel ke 18![Screenshot (37)](https://github.com/user-attachments/assets/1f1b1cd6-25d1-4917-8f46-18ae1cc952a1)


![Screenshot (38)](https://github.com/user-attachments/assets/ee835812-f132-4ac4-86be-89ff30eb9b0a)



