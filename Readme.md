# Konfigurasi Routing Static

Setelah seluruh device dikonfigurasi, perlu ditambahkan Tabel Routing di masing-masing Router. Tabel Routing ini menunjuk ke jaringan (network) yang tidak terhubung langsung dengan router tersebut. Seperti yang telah disebutkan sebelumnya, Tabel Routing Static dibuat oleh Administrator secara manual, artinya tabel routing tersebut perlu di-update jika ada perubahan konfigurasi jaringan ataupun terjadi penambahan perangkat router dalam jaringan.

![App Screenshot](/Image/0.png)

### Topologi di Packet Tracer

![App Screenshot](/Image/Rangkaian.png)

Note: Untuk konfigurasi alamat ip pada setiap interface di device router, ikuti tutorial sebelumnya, setelah hal tersebut dilakukan silahkan konfigurasi routing static pada setiap router dengan command di bawah ini.

Router_I

```bash
ROUTER_I (config)#ip route 192.168.20.0 255.255.255.0 10.10.10.2
ROUTER_I (config)#ip route 10.20.10.0 255.255.255.252 10.10.10.2
ROUTER_I (config)#ip route 192.168.40.0 255.255.255.0 10.10.10.2
```

![App Screenshot](/Image/1.png)

Router_II

```bash
ROUTER_II (config)#ip route 192.168.2.0 255.255.255.0 10.10.10.1
ROUTER_II (config)#ip route 192.168.40.0 255.255.255.0 10.20.10.2
```

![App Screenshot](/Image/2.png)

Router_III

```bash
ROUTER_III (config)#ip route 192.168.2.0 255.255.255.0 10.20.10.1
ROUTER_III (config)#ip route 10.10.10.0 255.255.255.252 10.20.10.1
ROUTER_III (config)#ip route 192.168.20.0 255.255.255.0 10.20.10.1
```

![App Screenshot](/Image/3.png)

## Verifikasi Static Routing

![App Screenshot](/Image/4.png)

Pada setiap router, dapat dilihat konfigurasi routing static dengan ditanda oleh "S"

## Konfigurasi Default Route

"Default route" adalah tipe rute statik khusus. Sebuah "default route" adalah rute yang digunakan ketika rute dari sumber/source ke tujuan tidak dikenali atau ketika tidak terdapat informasi yang cukup dalam tabel routing ke network tujuan.

![App Screenshot](/Image/10.png)

Router_III

```bash
ROUTER_III (config)#ip route 0.0.0.0 0.0.0.0 10.20.10.1
```

Router_II

```bash
ROUTER_II (config)#ip route 0.0.0.0 0.0.0.0 10.10.10.1
ROUTER_II (config)#ip route 0.0.0.0 0.0.0.0 10.20.10.1
```

Router_I

```bash
ROUTER_I (config)#ip route 0.0.0.0 0.0.0.0 10.10.10.2
```

| Perintah     | Keterangan                                                                             |
| ------------ | -------------------------------------------------------------------------------------- |
| `ip route`   | Menyatakan rute statik                                                                 |
| `0.0.0.0`    | Rute ke "nonexistent subnet". (dengan special mask, Ini menunjukkan "default network") |
| `0.0.0.0`    | Special mask mengindikasikan "default route"                                           |
| `10.10.10.1` | Alamat IP Router I.                                                                    |
| `10.20.10.1` | Alamat IP Router III.                                                                  |
| `10.10.10.2` | Alamat IP Router II.                                                                   |

## Dynamic Routing - RIPv1 & RIPv2 (Routing Information Protocol)

Routing Information Protocol (RIP) adalah sebuah routing protokol distance- vector, interior gateway (IGP), yang digunakan oleh router untuk bertukar informasi routing. RIP menggunakan hop count sebagai metric routing. RIP mencegah routing loops dengan menerapkan batas jumlah hop yang diizinkan dalam jalur dari sumber ke tujuan. Jumlah maksimum hop yang diizinkan untuk RIP adalah 15. Batasan hop tersebut bagaimanapun juga membatasi ukuran jaringan yang dapat didukung oleh RIP. RIP versi 2 (RIPv2) merupakan pengembangan dari RIP.

## Konfigurasi Routing Dinamic RIPv2

RIPv2 sebenarnya merupakan sebuah peningkatan dari RIPv1. berikut perbedaan
antara keduanya:

1. RIPv1 adalah Classful routing protocol, dan RIPv2 Classless routing protocol
2. Dalam RIPv1 subnet mask TIDAK termasuk dalam pembaruan perutean dan dalam RIPv2 subnet mask disertakan dalam pembaruan perutean.
3. RIPv2 multicast seluruh table routing ke semua router yang berdekatan di alamat 224.0.0.0, berbeda dengan RIPv1 yang menggunakan broadcast (255.255.255.255)

![App Screenshot](/Image/11.png)

### Topologi di Packet Tracer

![App Screenshot](/Image/12.png)

NOTE: Sebelum memulai konfigurasi routing, silahkan konfigurasi terlebih dahulu alamat IP pada setiap interface pada masing - masing router.

Router_I

```bash
ROUTER_I(config)#router rip
ROUTER_I(config-router)#version 2
ROUTER_I(config-router)#network 192.168.2.0
ROUTER_I(config-router)#network 10.10.10.0
```

![App Screenshot](/Image/13.png)

Router_II

```bash
ROUTER_III(config)#router rip
ROUTER_III(config-router)#version 2
ROUTER_III(config-router)#network 192.168.40.0
ROUTER_III(config-router)#network 10.20.10.0
```

![App Screenshot](/Image/14.png)

ROUTER_III

```bash
ROUTER_III(config)#router rip
ROUTER_III(config-router)#version 2
ROUTER_III(config-router)#network 192.168.40.0
ROUTER_III(config-router)#network 10.20.10.0
```

![App Screenshot](/Image/15.png)

## Verifikasi Dynamic Routing - RIPv2

![App Screenshot](/Image/16.png)

Pada setiap router, dapat dilihat konfigurasi routing RIPv2 dengan ditandai oleh `R`
