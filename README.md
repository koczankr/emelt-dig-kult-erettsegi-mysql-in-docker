# Emelt szintű digitális kultúra érettségi - MySQL és PHPMyAdmin Docker környezet kialakítása

## Áttekintés

Ez a repository egy olyan Docker Compose konfigurációt tartalmaz, amely egy **MariaDB** adatbázis és egy **PHPMyAdmin** adminisztrációs felület futtatását teszi lehetővé. A cél egy könnyen használható környezet biztosítása az emelt szintű digitális kultúra érettségi gyakorlati feladataihoz.

## Követelmények

- Docker telepítése szükséges a használathoz.
- További szükséges komponensek:
  - Docker Compose (általában a Dockerrel együtt települ).

## Telepítés

### Docker és Docker Compose telepítése

1. Töltsd le a Docker Desktopot a hivatalos weboldalról: [https://www.docker.com](https://www.docker.com).
2. Telepítsd a Docker Desktopot a rendszeredre.
3. Ellenőrizd, hogy a Docker és Docker Compose telepítve vannak:
   ```bash
   docker --version
   docker-compose --version
   ```

### Projekt elindítása

1. Klónozd a repository-t a gépedre:
   ```bash
   git clone https://github.com/koczankr/emelt-dig-kult-erettsegi-mysql-in-docker.git
   cd emelt-dig-kult-erettsegi-mysql-in-docker
   ```

2. Indítsd el a szolgáltatásokat:
   ```bash
   docker-compose up -d
   ```

3. Nyisd meg a PHPMyAdmin felületet a böngészőben:
   [http://localhost:8080](http://localhost:8080)

   - **Felhasználónév:** `root`
   - **Jelszó:** az `MYSQL_ROOT_PASSWORD` értéke, alapértelmezés szerint `rootpassword`.

## Használat az órák között

Az órák után **ne töröld a konténereket**, hanem csak állítsd le őket, hogy az adatok megmaradjanak, és a következő órára gyorsan újraindíthatók legyenek.

- **Konténerek leállítása**:
   ```bash
   docker-compose stop
   ```

- **Konténerek újraindítása**:
   ```bash
   docker-compose start
   ```

Ezek a parancsok megőrzik az adatokat, és a következő órán azonnal használhatóvá teszik a környezetet.

## Konfiguráció

A `docker-compose.yml` fájlban a következő komponensek vannak meghatározva:

### MariaDB (db)

- Kép: `mariadb:10`
- Port: `3306`
- Alapértelmezett adatbázis: `testdb`
- Felhasználó: `user`
- Jelszó: `userpassword`
- Root jelszó: `rootpassword`

### PHPMyAdmin

- Kép: `phpmyadmin:5.2`
- Port: `8080`

## Adatok hibaelhárítás céljából

A MariaDB adatai a Docker volume-ban kerülnek tárolásra. Normál üzemhez, vagyis az órák tartásához és a felkészüléshez, fájlszintű hozzáférés nem szükséges. Ha azonban valamilyen hiba esetén szükséges lenne az adatok ellenőrzése vagy mentése, a következő lépésekkel férhetsz hozzá:

1. Ellenőrizd a volume helyét:
   ```bash
   docker volume inspect db_data
   ```

2. Ha szükséges, másold ki az adatokat a helyi fájlrendszerbe:
   ```bash
   docker cp mariadb:/var/lib/mysql ./mysql-backup
   ```

## További információ

Ez a környezet kifejezetten az emelt szintű digitális kultúra érettségi feladataihoz lett kialakítva, és használható oktatási vagy gyakorlási célokra.

Kóczán Krisztián