# 🍽️ Recipe App API

Modern bir yemek tarifi yönetim sistemi — Django REST Framework ile geliştirilmiş, Docker ile konteynerize edilmiş ve production-ready!

---

## 🚀 Proje Hakkında

**Recipe App API**, kullanıcıların yemek tariflerini oluşturup yönetebileceği, modern Python geliştirme pratikleriyle yazılmış bir RESTful API'dir. Geliştiriciler için ölçeklenebilir, güvenli ve genişletilebilir bir altyapı sunar. CI/CD pipeline'ı ve kapsamlı API dokümantasyonu ile tam anlamıyla production ortamına hazırdır.

---

## ✨ Özellikler

- ✅ **RESTful API:** Modern REST API standartlarına uygun endpoint'ler  
- 🔐 **Authentication & Authorization:** Güvenli kullanıcı kimlik doğrulama sistemi  
- 🍲 **Recipe Management:** Tarif oluşturma, düzenleme, silme ve listeleme  
- 🧂 **Ingredient Management:** Malzeme yönetimi  
- 🏷️ **Tag System:** Tarifleri etiketleyerek kategorize etme  
- 🖼️ **Image Upload:** Tarif görselleri yükleme  
- 👤 **User Profiles:** Kullanıcı profil yönetimi  
- 🐳 **Docker Support:** Tam Docker desteği ile kolay deployment  
- ⚙️ **CI/CD:** GitHub Actions ile otomatik test ve deployment süreci  
- 📖 **API Documentation:** Swagger/OpenAPI ile detaylı API dokümantasyonu  

---

## 🛠️ Kullanılan Teknolojiler

- **Python 3.9+**
- **Django 4.x**
- **Django REST Framework**
- **PostgreSQL** (Docker içinde sağlanır)
- **Docker & Docker Compose**
- **Nginx** (Reverse Proxy)
- **GitHub Actions** (CI/CD Pipeline)
- **Swagger / OpenAPI** (API dokümantasyonu)

---

## 📋 Gereksinimler

Aşağıdaki araçların sisteminizde kurulu olması gerekir:

- **Python 3.9+**
- **Docker & Docker Compose**
- (PostgreSQL, Docker ile birlikte otomatik olarak sağlanır)

---

## 🚧 Kurulum

Projeyi başlatmak için aşağıdaki adımları takip edebilirsiniz:

```bash
git clone https://github.com/kullanici_adi/recipe-app-api.git
cd recipe-app-api
docker-compose up --build
