# h6 Hello Django

#### Oma Host kokoonpanoni:

| Komponentti | Kuvaus | Lisätiedot |
| :---        |    :----:   |          ---: |
| Emolevy | MSI B550-A PRO | ATX, AM4 |
| Prosessori   | AMD Ryzen 9 5900X | 12-Core 3.70 GHz |
| RAM   | G.Skill  Ripjaws V |  32GB (4x8GB) DDR4 3600MHz, CL 16, 1.3  |
| Näytönohjain   | Sapphire PULSE AMD Radeon RX 7900 GRE        | 16GB     |
| Kovalevy   | Kingston 1TB        | A2000 NVMe PCIe SSD M.2      |
| Kovalevy   | Crucial 512GB        | MX100 SSD     |
| Kovalevy   | Crucial 256GB        | MX100 SSD     |
| Virtalähde   | Asus 750W TUF Gaming Gold        | ATX 80 Plus      |
| Kotelo   | Phanteks Enthoo Pro       |  Full Tower      |

Käyttöjärjestelmä: Windows 11 Pro 23H2

#### Virtuaalikone
Oracle VirtualBox 7 - Debian 12 GNU/Linux (bookworm)<br>
6 Prosessoriydintä - 4GB RAM-muistia - 60GB tallennustilaa

#### Palvelin
UpCloud<br>
Debian 12 GNU/Linux (bookworm)<br>
1 Prosessoriydin - 1GB RAM-muistia - 10GB tallennustilaa

## a) Tee yksinkertainen esimerkkiohjelma Djangolla

*27.9.2024 klo 11:30*

Tähän käytän tietenkin apuna Karvisen [Django 4 Instant Customer Database Tutorial](https://terokarvinen.com/2022/django-instant-crm-tutorial/):ia.

Kirjauduin palvelimelleni ja aluksi päivitetään pakettilista ``sudo apt-get update``. 

Asennetaan virtualenv virtuaaliympäristö ``sudo apt-get -y install virtualenv``. 

Luodaan uusi kansio virtualenville, joka sisältää viimeisimmät paketit ``virtualenv --system-site-packages -p python3 env/``.

![Venvpaketit](https://github.com/user-attachments/assets/e335692f-fce8-4ace-a9d4-bf573d87c790)

Otetaan virtuaaliympäristö käyttöön ``source env/bin/activate``

![venvkayttoon](https://github.com/user-attachments/assets/dec76d2f-728a-465a-b3e8-edb49ebc6c80)

Nyt ollaan virtuaaliympäristössä, emme halua käyttää "pip":iä ilman virtualenviä, eikä sitä saa käyttää "sudo":lla. En halua antaa palvelinta muiden käyttöön, joten noudatan ohjetta tarkasti. Teen kyselyn, jotta varmistutaan, että olemme asentamassa virtuaaliympäristöön.

![whichpip](https://github.com/user-attachments/assets/4f44af41-382e-46f5-b050-df4b23999c8a)

Luon ohjeen mukaan varmuudeksi "requirements.txt." tiedoston microlla, jotta ei vahingossakaan tule kirjoitusvirheitä kun asennetaan django pip:llä. Tiedoston sisään kirjoitan "django" ja tallennan tiedoston "ctrl+s" ja poistun "ctrl+q".

![requirementstxt](https://github.com/user-attachments/assets/71d45db8-0f8f-446e-88fc-89aecd82f8a1)

Varmuuden vuoksi kopioin requirements.txt tekstin ja katson vielä ``cat requirements.txt`` komennolla, että siellä varmasti lukee oikein "django"

![catrequirements](https://github.com/user-attachments/assets/c652f279-bdc9-4267-b3e3-efec9da6b5e8)

Tämä voi tuntua hätävarjelun liioittelulta, mutta en halua ottaa ylimääräisiä riskejä.

Seuraavaksi asennetaan django pip:llä ``pip install -r requirements.txt``, hieman jännittävä toimenpide, mutta siitä selvittiin.

![djangoinstalled](https://github.com/user-attachments/assets/fd1553ab-c6d5-4673-937b-04217fa23d98)

Aloitan uuden Django projektin nimeltä "sant" ``django-admin startproject sant``

Seuraavaksi kokeillaan laittaa Django palvelin toimimaan ohjeen mukaan, menen "sant" kansioon, siellä ``.manage.py runserver``

![managerunserver](https://github.com/user-attachments/assets/6a48a957-5590-458a-925e-53254b300ecd)

Nyt on tuotantopalvelin päällä. Tätä palvelinta ei kannata päästää internetiin. Kokeillaan mennä selaimella osoitteeseen "http://127.0.0.1:8000/".

Ei toimi, tuo ``.manage.py runserver`` antoi punaisella tekstillä herjaa "You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions."              ja korjaukseksi komento ``python manage.py migrate``, joten kokeilen sitä.

![migrateisson](https://github.com/user-attachments/assets/17921ee0-3214-4359-a75c-3b49401f9cf5)

Tämän jälkeen uudestaan ``.manage.py runserver`` ja nyt ei tule virheilmoituksia.

![djangoserveron](https://github.com/user-attachments/assets/31cb9475-3821-4542-98f6-84648e9884ba)

Kokeillaan uudestaan selaimella "http://127.0.0.1:8000/". Eikä toimi vieläkään, tietenkin tämä johtuu siitä, että olen virtuaalipalvelimella, jossa ei ole muuta kuin CLI käyttöliittymä. Pitää siis tehdä kaikki uudestaan paikallisesti. ``exit`` komennolla takaisin "taulu" virtuaalikoneelle. Teen samat asiat kuin aiemmin.

![djangoversion](https://github.com/user-attachments/assets/92a4446a-936e-44fb-b830-3dadb67b8ebf)

Sama migrate herja tuli nytkin. Nyt käynnistettyäni palvelimen pääsen selaimella "http://127.0.0.1:8000/", voi taas äiti olla ylpeä pojastaan

![djangoworks](https://github.com/user-attachments/assets/dfc6bd35-1a38-4eee-b540-1e52eb0d6d87)

Hauskana yksityiskohtana huomaan, nyt kun palvelin on päällä, palvelin näyttää käyntini tuolla sivulla suoraan reaaliajassa ja herjaa, että favicon.ico:a ei voitu toimittaa, eli se pieni kuvake mikä näkyy selaimen välilehdellä

![kayntitiedotreaali](https://github.com/user-attachments/assets/de1811d5-71c5-4925-8513-45b5fe780edd)

Seuraavaksi lisätään admin url:lle "http://127.0.0.1:8000/admin/" suoraan Karvisen ohjeilla, kätevä tuo salasananluontityökalu

![historymakeadmin](https://github.com/user-attachments/assets/c39fcfa7-2972-47c3-ac5c-0d9c387a71e7)

Nyt pääsen admin-kirjautumisikkunaan osoitteella "http://127.0.0.1:8000/admin/"

![adminlogin](https://github.com/user-attachments/assets/a7db05f8-1299-4bbc-89a1-68e54cda02bf)

Jätin käyttäjänimikentän tyhjäksi, joten oletuksena käyttäjä on tässä tapauksessa "santeri", olen sisällä

![sisallaadminina](https://github.com/user-attachments/assets/6a367551-e19e-4e77-b90d-341ab1e30fcc)

Loin uuden käyttäjän "sant" kohdasta "users - add"

![santuus](https://github.com/user-attachments/assets/3e72ca96-e34a-4851-b24b-c61df5083e23)

Annoin käyttäjälle "staff", sekä "superuser"-statuksen

![superstaff](https://github.com/user-attachments/assets/a6710da3-e12b-48af-b5d6-b9926e6d7671)

Kirjauduin ulos, ja takaisin sisään, tällä kertaa "sant" nimisenä käyttäjänä

![santsissal](https://github.com/user-attachments/assets/952d81d2-7008-49f4-b8b2-e0b2c9b9ff21)

Kokeilin mennä käyttäjienhallintaan muokkaamaan oikeuksia, otin alkuperäiseltä "santeri":lta "staff"-oikeudet pois, todettakoon, että superkäyttäjän oikeudet toimivat tällä uudella käyttäjällä

![santerisstaffpois](https://github.com/user-attachments/assets/db72c9ad-0a5e-4637-b85e-6f3e2b31846b)

#### Luodaan asiakastietokanta

Luodaan "crm/" kansio CRM-sovellukselle ``./manage.py startapp crm``

Lisätään sovellus asennettuihin sovelluksiin ``micro sant/settings.py``

![crmlisatty](https://github.com/user-attachments/assets/59c60335-15c2-4d5f-a0f5-a4053802b470)

Lisätään modeleja ``micro crm/models.py``. Tiedostossa oli valmiina "from django.db import models". Lisätään sinne vielä ``class Customer(models.Model):
   name = models.CharField(max_length=300)``. Täten tietokantaan tulee "customer"-tietue "name" sarakkeella.

![crmcustodata](https://github.com/user-attachments/assets/6501c770-656d-4748-b5ab-01936d0ad724)

Nyt ajetaan samat ``./manage.py makemigrations`` ja ``./manage.py migrate``

Rekisteröidään tietokanta admin/ kansioon ``micro crm/admin.py``, ja sille lisätään tiedot ``from . import models
admin.site.register(models.Customer)``

Nyt pystytään lisäilemään asiakkaita, tosin niiden nimet ovat luokkaa "Customer object (1)"

![asiakkaatcustobject](https://github.com/user-attachments/assets/4f416d17-69f2-4c69-9e19-addcc9565139)







## b)




## Otsikko


## Lähteet

Karvinen, T. 2022. Deploy Django 4 - Production Install. Luettavissa: https://terokarvinen.com/2022/deploy-django/. Luettu 27.9.2024<br>
Karvinen, T. 2022. Django 4 Instant Customer Database Tutorial. Luettavissa: https://terokarvinen.com/2022/django-instant-crm-tutorial/. Luettu 27.9.2024<br>

---

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html<br>
Pohjana Tero Karvinen 2012: Linux kurssi, http://terokarvinen.com<br><br>
Kirjoittanut <em>Santeri Vauramo</em>, 2024
