---
layout: post
title: Instalasi Library Laravel MongoDB 
---

Dalam framework laravel, secara default laravel tidak dapat melakukan koneksi dengan database mongodb. Maka dari itu dibutuhkan sebuah library tambahan yang akan menjembatani interaksi ini. 

Library laravel mongodb yang populer adalah library  [jenssegers](https://github.com/jenssegers)/**[laravel-mongodb](https://github.com/jenssegers/laravel-mongodb)** didalam posting kali ini akan dijelaskan tentang langkah-langkah untuk melakukan instalasi library laravel mongodb ke dalam project laravel.

## Prerequisite
Pastikan anda telah membuat sebuah laravel project. Anda dapat membuat sebuah laravel project dengan menggunakan perintah 

```bash
composer create-project --prefer-dist laravel/laravel blog
```
atau dengan menggunakan script

```bash
laravel new blog
```

Pada script diatas, kata  ``blog`` adalah nama project yang akan di buat. Silahkan ganti nama project sesuai dengan apa yang Anda inginkan. 

Silahkan baca referensinya https://laravel.com/docs/5.7/installation

## Library Installation

Lakukan instalasi library dengan menggunakan script composer berikut 

```bash
composer require jenssegers/mongodb
```

pada ``config/app.php`` tambahkan service provider berikut
```php
Jenssegers\Mongodb\MongodbServiceProvider::class,
```

lalu lakukan penambahan mongodb driver connection pada ``config/database.php``

```php
'mongodb' => [
 'driver'   => 'mongodb',
 'host'     => env('DB_HOST', 'localhost'),
 'port'     => env('DB_PORT', 27017),
 'database' => env('DB_DATABASE'),
 'username' => env('DB_USERNAME'),
 'password' => env('DB_PASSWORD'),
 'options'  => [
 'database' => 'admin'
 ]
],
```
dan terakhir Anda dapat mengganti default database pada file ``config/database.php`` dengan **mongodb**

## Usage Tutorial

Untuk mencoba apakah laravel project laravel kita sudah dapat mengakses mongodb database silahkan membuat script sederhana seperti contoh berikut

contoh script pada model  
```php
<?php
namespace App\Models;

use Jenssegers\Mongodb\Eloquent\Model as Eloquent;
use Jenssegers\Mongodb\Eloquent\HybridRelations;

class News extends Eloquent
{
 protected $table = 'news';
 use HybridRelations;
 public $timestamps = true;

 protected $fillable = [
 'tipe_berita',
 'judul',
 'status',
 'deskripsi_singkat',
 'deskripsi_berita',
 'gambar',
 'event_id'
 ];
}
```

Didalam model ini pastikan script

```php
use Illuminate\Database\Eloquent\Model;
```

telah di ganti dengan 
```php
use Jenssegers\Mongodb\Eloquent\Model as Eloquent;
```

Contoh script pada controller

```php
<?php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Controllers\Controller;
use App\Models\News;

class HomeController extends Controller
{
	public function index() {
		 $news = News::all();
		 dd($news);
	}
}
```

Yap sekian tutorial cara menglakukan instalasi laravel mongodb. 

Good Luck!
Irianto