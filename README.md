# Kaffekompaniet

Grupparbete: en CMS-lösning i Umbraco 17 för Kaffekompaniet, ett lokalt kafferosteri med butik. CMS-inställningar delas mellan gruppen med uSync.

## Kör projektet

1. Installera [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) och kontrollera att versionen börjar på 10:

   ```bash
   dotnet --version
   ```

2. Klona repot och starta projektet:

   ```bash
   git clone <repo-url>
   cd kaffekompaniet/Kaffekompaniet
   dotnet run
   ```

3. Öppna adressen som terminalen skriver ut (t.ex. `https://localhost:44xxx`). Håll terminalen öppen medan du arbetar.

4. Första gången: fyll i installationsguiden med ditt eget administratörskonto och välj **SQLite** som databas.

5. Logga in i backoffice på `/umbraco`.
