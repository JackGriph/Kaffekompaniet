# Kaffekompaniet

Grupparbete: CMS-lösning i Umbraco för ett lokalt kafferosteri med butik.

| Del | Version |
|---|---|
| Umbraco CMS | 17.7.1 (LTS) |
| uSync | 17.4.3 |
| .NET SDK | 10 |
| Databas | SQLite (lokal, en per person, committas inte) |

## Kom igång första gången

Målet är ett körande Umbraco-projekt där du är inloggad som administratör. Projektet är redan skapat (med `dotnet new umbraco --name Kaffekompaniet`), så du behöver bara klona och starta det.

**Steg 1. Installera .NET SDK.** Umbraco 17 kräver .NET 10 SDK. Ladda ner det från [Microsofts nedladdningssida](https://dotnet.microsoft.com/download/dotnet/10.0) och kontrollera versionen:

```bash
dotnet --version
```

Utskriften ska börja på 10.

**Steg 2. Klona repot.**

```bash
git clone <repo-url>
```

**Steg 3. Starta projektet.**

```bash
cd kaffekompaniet/Kaffekompaniet
dotnet run
```

Terminalen skriver ut en lokal webbadress, t.ex. `https://localhost:44xxx`. Öppna den i webbläsaren. Håll terminalen öppen så länge du arbetar, för stänger du den stannar webbplatsen.

**Steg 4. Kör installationsguiden.** Fyll i namn, e-postadress och lösenord för ditt eget administratörskonto. Välj **SQLite** som databas och slutför guiden. Databasen hamnar i `umbraco/Data/` och committas inte, så alla har en egen.

**Steg 5. Logga in i backoffice.** Guiden loggar in dig automatiskt. Annars öppnar du `/umbraco` på din lokala adress och loggar in med kontot du skapade. När sajten startar importerar uSync automatiskt dokumenttyper, datatyper och mallar från mappen `uSync/`.

Du kan också starta från VS Code med **Run and Debug → Starta Kaffekompaniet** (tillägget **C# Dev Kit** behövs).

## Projektstruktur

```
kaffekompaniet/
└── Kaffekompaniet/        ← Umbraco-projektet
    ├── uSync/v17/         ← CMS-inställningar som filer (committas)
    ├── Views/             ← Razor-mallar
    ├── wwwroot/           ← CSS, JS, bilder (inte media)
    └── umbraco/Data/      ← lokal databas (ignoreras av git)
```

## uSync-inställningar

I `appsettings.json`:

- `ImportOnFirstBoot: true`: en ny installation importerar allt från `uSync/` direkt.
- `ImportAtStartup: "Settings"`: varje start importerar andras ändringar av dokumenttyper, datatyper, mallar m.m.
- `ExportOnSave: "Settings"`: när du sparar en dokumenttyp/datatyp/mall i backoffice skrivs filen i `uSync/` automatiskt.

Du kan alltid exportera eller importera manuellt under **Settings → uSync** i backoffice.

**Viktigt:** gratisversionen av uSync synkar **inte** användare och användargrupper. Rollerna (Ansvarig, Redaktör, Skribent) behöver därför skapas för hand i varje installation enligt en gemensam beskrivning i gruppdokumentet. Det går även att använda uSync.Complete (betalversion).

Innehåll (sidor och media) exporteras inte automatiskt, men kan exporteras manuellt i uSync (**Everything → Export**) och committas av den som äger innehållet.

## Rutin per arbetspass

1. Hämta `main` och skapa en gren:
   ```bash
   git checkout main && git pull && git checkout -b feature/<namn>
   ```
2. Starta sajten (`dotnet run`) så att uSync importerar andras ändringar.
3. Gör dina ändringar.
4. Kontrollera att uSync har exporterat (eller exportera manuellt).
5. Kontrollera `git diff`, committa, pusha och öppna en pull request.
6. Efter merge: alla hämtar `main` och startar om sajten.

## Regler

- Exportera alltid före commit och importera alltid efter pull.
- Två personer ändrar inte samma dokumenttyp samtidigt.
- Små PR:er, merga ofta. `main` är skyddad, någon annan granskar.
- Inga lösenord i repot. Testkonton för varje roll skrivs i gruppdokumentet.
- Personliga inställningar (t.ex. annan databas) läggs i `appsettings.Local.json`, som inte committas.
