# 🍽️ Recipe App API

[![Checks](https://github.com/FreZYa/recipe-app-api/actions/workflows/checks.yml/badge.svg)](https://github.com/FreZYa/recipe-app-api/actions/workflows/checks.yml)

Django REST Framework ile yazılmış bir yemek tarifi API'si. Kullanıcılar tarif, malzeme ve etiket oluşturup yönetebilir, tariflere görsel yükleyebilir. Proje Docker ile çalışır, testleri ve lint kontrolleri GitHub Actions'ta koşar, production için Nginx + uWSGI kurulumu vardır.

## Özellikler

- **Kullanıcı yönetimi:** e-posta ile kayıt, token tabanlı kimlik doğrulama, profil güncelleme
- **Tarifler:** oluşturma, listeleme, güncelleme, silme; etiket ve malzemeye göre filtreleme
- **Malzeme ve etiketler:** tarif oluştururken iç içe (nested) oluşturma
- **Görsel yükleme:** tariflere resim ekleme
- **API dokümantasyonu:** drf-spectacular ile OpenAPI şeması ve Swagger UI
- **Testler:** model, API ve yönetim komutları için Django test suite'i
- **Production kurulumu:** Nginx reverse proxy + uWSGI, ayrı `docker-compose-deploy.yml`

## Teknolojiler

| | |
|---|---|
| Dil | Python 3.9 |
| Framework | Django 3.2, Django REST Framework 3.12 |
| Veritabanı | PostgreSQL 13 |
| Dokümantasyon | drf-spectacular (OpenAPI 3) |
| Altyapı | Docker, Docker Compose, Nginx, uWSGI |
| CI | GitHub Actions (test + flake8) |

## Kurulum (geliştirme)

Gereksinim: Docker ve Docker Compose.

```bash
git clone https://github.com/FreZYa/recipe-app-api.git
cd recipe-app-api
docker compose up --build
```

API `http://localhost:8000` adresinde çalışır.

| Adres | İçerik |
|---|---|
| `/api/docs/` | Swagger UI |
| `/api/schema` | OpenAPI şeması |
| `/api/health-check/` | Sağlık kontrolü |
| `/admin/` | Django admin |

Admin kullanıcısı oluşturmak için:

```bash
docker compose run --rm app sh -c "python manage.py createsuperuser"
```

## Testler ve lint

```bash
docker compose run --rm app sh -c "python manage.py wait_for_db && python manage.py test"
docker compose run --rm app sh -c "flake8"
```

## Production'a alma

1. `.env.sample` dosyasını `.env` olarak kopyalayın ve değerleri doldurun (`DJANGO_SECRET_KEY`, veritabanı bilgileri, `DJANGO_ALLOWED_HOSTS`).
2. Çalıştırın:

```bash
docker compose -f docker-compose-deploy.yml up -d --build
```

Uygulama Nginx üzerinden 80 numaralı portta yayınlanır. Statik dosyalar ve yüklenen görseller ayrı bir volume'da tutulur.

## API uçları

| Method | Endpoint | Açıklama |
|---|---|---|
| POST | `/api/user/create/` | Kullanıcı kaydı |
| POST | `/api/user/token/` | Token alma |
| GET, PUT, PATCH | `/api/user/me/` | Profil |
| GET, POST | `/api/recipe/recipes/` | Tarif listesi / oluşturma |
| GET, PUT, PATCH, DELETE | `/api/recipe/recipes/{id}/` | Tarif detayı |
| POST | `/api/recipe/recipes/{id}/upload-image/` | Tarif görseli yükleme |
| GET | `/api/recipe/tags/` | Etiket listesi |
| PUT, PATCH, DELETE | `/api/recipe/tags/{id}/` | Etiket güncelleme / silme |
| GET | `/api/recipe/ingredients/` | Malzeme listesi |
| PUT, PATCH, DELETE | `/api/recipe/ingredients/{id}/` | Malzeme güncelleme / silme |

Tarifler etiket ve malzemeye göre filtrelenebilir: `/api/recipe/recipes/?tags=1,2&ingredients=3`. Etiketler ve malzemeler tarif oluşturulurken iç içe gönderilerek yaratılır.

Tüm uçların güncel ve ayrıntılı listesi için `/api/docs/` adresine bakın.
