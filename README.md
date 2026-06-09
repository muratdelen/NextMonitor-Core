# NextMonitor-Core

**NextMonitor-Core**, NextLife platformu için açık kaynak gözlemlenebilirlik altyapısıdır.

Bu repo sıfırdan yazılmış bir monitoring uygulaması değildir. Prometheus, Grafana, Loki, Promtail, OpenTelemetry Collector ve Uptime Kuma gibi açık kaynak araçları NextLife mimarisine uygun şekilde hazır kurmak için kullanılır.

## Amaç

NextLife servislerini tek merkezden izlemek:

- Servislerin ayakta olup olmadığını takip etmek
- Spring Boot Actuator metriklerini toplamak
- Docker ve uygulama loglarını merkezi hale getirmek
- Dashboard üretmek
- Trace, metric ve log akışını standartlaştırmak
- Servis kesintileri için uyarı altyapısı hazırlamak

## Kullanılan açık kaynak bileşenler

| Bileşen | Amaç |
|---|---|
| Prometheus | Metric toplama ve alarm kuralı çalıştırma |
| Grafana | Dashboard ve görselleştirme |
| Loki | Log saklama ve sorgulama |
| Promtail | Logları Loki'ye gönderme |
| OpenTelemetry Collector | Trace, metric ve log standardizasyonu |
| Uptime Kuma | Servis erişilebilirlik kontrolü |

## Hızlı başlatma

```bash
cp .env.example .env
docker compose -f docker-compose.monitor.yml up -d
```

## Varsayılan erişim adresleri

| Servis | Adres |
|---|---|
| Grafana | http://localhost:3000 |
| Prometheus | http://localhost:9090 |
| Uptime Kuma | http://localhost:3001 |
| Loki | http://localhost:3100 |
| OpenTelemetry Collector HTTP | http://localhost:4318 |

## Varsayılan Grafana bilgileri

```text
Kullanıcı: admin
Şifre: nextmonitor_admin
```

Production ortamında bu şifre `.env` dosyasından değiştirilmelidir.

## NextLife servislerinin izlenmesi

Spring Boot servislerinde Actuator açık olmalıdır:

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info,prometheus,metrics
  endpoint:
    health:
      show-details: always
  prometheus:
    metrics:
      export:
        enabled: true
```

Prometheus servislerden şu endpointi okur:

```text
/actuator/prometheus
```

## NextLife entegrasyon hedefleri

İlk takip edilecek servisler:

- next-gateway
- next-core-service
- next-role-service
- next-log-service
- next-data-service
- next-flow-service
- next-admin-ui
- nextid-core
- nextapproval-core
- nextsearch-core
- next-minio

## Production notu

Bu dosya ilk aşamada development ve test ortamı için hazırlanmıştır. Production ortamında:

- Grafana şifresi değiştirilmelidir.
- Public portlar reverse proxy arkasına alınmalıdır.
- Loki ve Prometheus volume yedekleme planına dahil edilmelidir.
- Alertmanager veya kurum içi bildirim sistemi eklenmelidir.
- TLS/HTTPS yapılandırması yapılmalıdır.

## Lisans notu

Bu repo NextLife yapılandırma dosyalarını içerir. Kullanılan üçüncü parti açık kaynak yazılımların lisansları `LICENSE-NOTICES.md` dosyasında ayrıca belirtilmiştir.
