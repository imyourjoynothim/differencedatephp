# Selisih Tanggal PHP

Cara yang dipake untuk menghitung selisih waktu


## Penggunaan

Biasanya penggunaan format selisih tanggal ini dipake untuk :

- Durasi waktu
- Menghitung biaya berdasarkan durasi
- Waktu login
- Log aktivitas


## Selisih Menghitung 2 waktu (Format Jam)

```php
if ($raw->endDate == null) { //jika tidak ada waktu berakhir maka...
    $result = "-"; //akan strip
} else { //jika ada waktu berakhir maka
    $checkin = explode(":", $raw->startDate);
    $checkout = explode(":", $raw->endDate);
    $hours = $checkout[0] - $checkin[0];
    $minutes = $checkout[1] - $checkin[1];
    $second = $checkout[2];

    if (
        $checkin <= "12:00:00" && 
        $checkout >= "13:00:00"
    ) {
        $a = 1; // jika waktu selisih lebih dari jam 12 maka akan bertambah angka 1 || Contoh 13:00
    } else {
        $a = 0; // jika waktu selisih kurang dari jam 12 maka angkanya akan 0 || Contoh 03:00 
    }
    $minutes = strval(count($minutes)) < 2 ? '0' + $minutes : $minutes;
    if ($minutes < 0) {
        $hours--;
        $minutes = 60 + $minutes;
    }
    $hours = strval(count($hours)) < 2 ? '0' + $hours : $hours;

    $result = $hours - $a . ":" . $minutes . ":" . $second;

    //hasil output :
    02:59:59
}
```


## Selisih Menghitung 2 waktu (Format Tanggal)

```php
$startDate = strtotime($request->start_date);
$endDate = strtotime($request->end_date);
$datediff = $endDate - $startDate;

$result = round($datediff / (60 * 60 * 24));

//hasil output :
234 => Bisa dikasih output lain biar menampilkan hasil lengkapnya
```

## Selisih Menghitung 2 waktu (Format Tanggal)

```php
$startDate = new DateTime($request->start_date);
$endDate = new DateTime($request->end_date);
$datediff = $startDate->diff($endDate);

echo 'Selisih: '.$difference->y.' tahun, ' 
                   .$difference->m.' bulan, ' 
                   .$difference->d.' hari';

print_r($datediff);

//hasil output :
Selisih: 0 years, 1 months, 2 days
```
