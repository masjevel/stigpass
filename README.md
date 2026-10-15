# Stigpass

Planera träningspass för cykelgruppen, spara övningar och banor, och dela dagens pass med ledarna i WhatsApp eller Messenger.

Appen ligger gratis på GitHub Pages. Pass, övningar, banor och skisser sparas i Firebase och syns på både dator och telefon. Den fungerar också utan täckning.

---

## Så kommer du igång

Det tar ungefär en halvtimme. Du gör det en gång.

### Del 1 – GitHub (10 min)

1. Logga in på [github.com](https://github.com), eller skapa ett gratis konto.
2. Tryck på **+** uppe till höger och välj **New repository**.
   - Repository name: `stigpass`
   - Välj **Public**
   - Lämna resten som det är och tryck **Create repository**.
3. Tryck på länken **uploading an existing file**.
4. Packa upp `stigpass-app.zip` på datorn och öppna mappen. Markera **allt** som ligger i den (filerna och mapparna `fonts` och `icons`) och dra in det i webbläsarfönstret.
   Syns inte filen `.nojekyll` gör det inget.
5. Tryck **Commit changes** längst ner.
6. Gå till **Settings → Pages**. Under *Build and deployment*: välj **Deploy from a branch**, branch **main** och mapp **/ (root)**. Tryck **Save**.
7. Vänta 1–2 minuter och ladda om sidan. Överst står adressen, till exempel
   `https://dittnamn.github.io/stigpass/`.
   Öppna den. Du ska se *”Appen är inte kopplad till Firebase ännu”*. Då är del 1 klar.

### Del 2 – Firebase (15 min)

8. Gå till [console.firebase.google.com](https://console.firebase.google.com) och logga in med ditt Google-konto.
9. Tryck **Create a project** (eller *Get started*).
   - Namn: `stigpass`
   - **Stäng av Google Analytics** när du får frågan. Appen ska inte ha någon spårning.
   - Tryck **Create project**.
10. **Inloggning:** i menyn till vänster, välj **Build → Authentication → Get started**.
    - Under *Sign-in method*: välj **Google**, slå på **Enable**, välj din e-post som *support email* och tryck **Save**.
    - Tryck **Add new provider → Email/Password**, slå på det första reglaget och tryck **Save**.
11. **Godkänn din adress:** fortfarande i Authentication, gå till fliken **Settings → Authorized domains → Add domain**.
    Skriv `dittnamn.github.io`, alltså utan `https://` och utan `/stigpass`. Tryck **Add**.
12. **Databas:** välj **Build → Firestore Database → Create database**.
    - Får du välja *edition*: välj **Standard**.
    - **Location:** välj en plats i Europa, till exempel **europe-north1 (Finland)**. Det går inte att ändra senare.
    - Välj **Start in production mode** och tryck **Create**.
13. **Lås databasen:** öppna fliken **Rules** i Firestore.
    - Ta bort allt som står där.
    - Öppna filen `firestore.rules` (den finns i din GitHub-mapp), kopiera allt och klistra in.
    - Byt `DIN-EPOST@gmail.com` mot din egen e-postadress, med små bokstäver.
    - Tryck **Publish**.
14. **Hämta nycklarna:** tryck på kugghjulet uppe till vänster → **Project settings**. Scrolla ner till *Your apps* och tryck på webb-ikonen **`</>`**.
    - App nickname: `Stigpass`. Kryssa **inte** i *Firebase Hosting*.
    - Tryck **Register app**. Nu visas en kodruta med `const firebaseConfig = { … }`. Låt den vara öppen.

### Del 3 – Koppla ihop (5 min)

15. På GitHub: öppna filen **config.js** i ditt repository och tryck på pennan (**Edit**).
16. Fyll i värdena från Firebase-rutan mellan citattecknen, rad för rad: `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId` och `appId`.
    Fyll också i ditt namn under `owner` och en e-postadress under `contact`. De visas i *Om appen och integritet*.
17. Tryck **Commit changes**. Vänta 1–2 minuter.
18. Öppna appens adress och tryck **Logga in med Google**.

Nycklarna i `config.js` är inte hemliga. Det är reglerna från steg 13 som skyddar din data.

### Del 4 – Flytta in dina pass

19. Inloggad på datorn: tryck på gubben uppe till höger → **Importera från fil** → välj `stigpass-data.json`.
    **Ladda inte upp den filen till GitHub.** Där blir allt offentligt.

### Del 5 – På telefonen

20. Öppna appens adress i **Safari** (iPhone) eller **Chrome** (Android) och logga in.
21. iPhone: tryck på **Dela** → **Lägg till på hemskärmen**.
    Android: tryck på **⋮** → **Installera app** eller **Lägg till på startskärmen**.

---

## Bra att veta

**Låta en kompis prova.** Öppna Firestore → **Rules** och lägg till kompisens e-postadress i listan, med ett kommatecken efter raden innan:

```
'din-epost@gmail.com',
'kompis@gmail.com'
```

Tryck **Publish**. Kompisen får ett eget, tomt utrymme och ser inte dina pass.

**Säkerhetskopia.** Under Konto → **Spara säkerhetskopia** får du en fil med allt. Spara den någonstans ibland.

**Uppdatera appen.** Får du nya filer: GitHub → **Add file → Upload files**, dra in dem och tryck **Commit changes**. Filer med samma namn ersätts. Ladda inte upp `config.js` igen, då försvinner dina nycklar.

**Kostnad.** Firebase gratisnivå (Spark) räcker gott för det här. Du behöver inte lägga in något kort.

## Om något inte fungerar

| Det står | Gör så här |
|---|---|
| *Appen är inte kopplad till Firebase ännu* | `config.js` är tom eller inte sparad. Gör steg 15–17. |
| *Inställningarna i config.js går inte att läsa* | Ett citattecken eller kommatecken har försvunnit i `config.js`. Jämför med Firebase-rutan. |
| *Den här webbadressen är inte godkänd i Firebase* | Gör steg 11. |
| *Kontot … har inte tillgång till appen ännu* | E-postadressen i reglerna stämmer inte med kontot du loggar in med. Kontrollera steg 13 och tryck **Publish**. |
| *Webbläsaren stoppade inloggningsfönstret* | Tillåt popup-fönster för sidan och försök igen. |
| Gamla versionen visas efter en uppdatering | Stäng appen helt och öppna den igen. |
