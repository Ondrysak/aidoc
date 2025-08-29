# AI MVP: Skenování a interpretace laboratorního výsledku

## Popis funkce a rozdělení na komponenty

**Funkce:** Cílem nové AI funkce v aplikaci *IA Doktor* je umožnit uživateli vyfotit nebo nahrát svůj laboratorní výsledek (např. výsledky krevních testů) a automaticky získat srozumitelnou interpretaci těchto hodnot. Aplikace převede nestrukturovaný obsah laboratorního reportu (obrázek/PDF s tabulkou výsledků) na strukturovaná data a následně uživateli zobrazí, které hodnoty jsou v normě, které vysoké/nízké a co to pro něj znamená. Tím se laboratorní výsledky stanou **pochopitelnými a akčně využitelnými** pro uživatele.

**Komponenty řešení:** Funkcionalitu rozdělíme do několika částí:

* **Frontend aplikace (mobilní/web)**
* **Backendové API**
* **OCR modul (optické rozpoznávání znaků)**
* **LLM modul (Large Language Model)**
* **Orchestrátor logiky**
* **Databáze a úložiště**
* **Autentizační vrstva**

---

## Výběr technologického stacku

* **Backend (API server):** Python 3.x + FastAPI
* **OCR:** Tesseract OCR (open-source) nebo Google Cloud Vision / AWS Textract (cloud)
* **LLM:** OpenAI GPT-4 (případně GPT-3.5-Turbo)
* **Front-end:** React Native / Flutter
* **Databáze:** PostgreSQL (alternativně SQLite pro MVP)
* **Cloud a infrastruktura:** Docker, AWS/Azure/Heroku
* **Další knihovny:** OpenCV, Pillow, logging, PyTest

---

## Návrh struktury repozitáře

* `README.md`
* `app/`

  * `main.py`
  * `api/`
  * `services/` (OCR, LLM, orchestrátor)
  * `db/`
  * `config.py`
* `tests/`
* `requirements.txt`
* `.env.example`
* `Dockerfile`
* `docker-compose.yml`
* CI/CD workflow
* `docs/`

---

## Architektura řešení (proces zpracování)

1. Nahrání souboru (Frontend)
2. Přijetí požadavku (Backend API)
3. Předzpracování obrazu
4. OCR extrakce textu
5. Strukturalizace dat
6. Příprava promptu pro LLM
7. Volání OpenAI API
8. Post-processing odpovědi
9. Uložení výsledků
10. Odpověď klientovi
11. Zobrazení výsledku (Frontend)

---

## Napojení na externí služby a systémy

* **OpenAI API (GPT-4)**
* **OCR služba (Tesseract, Google, AWS)**
* **Databáze (PostgreSQL)**
* **Autentizace a autorizace (JWT)**
* **Služba pro ukládání souborů (S3/Blob Storage)**
* **Monitoring a logování (Prometheus, Grafana, Sentry)**

---

## Definice API rozhraní

* **Endpoint:** `POST /api/lab-results/interpret`
* **Autentizace:** Bearer token
* **Request Payload:** multipart/form-data s polem `file`
* **Response Payload:** JSON se strukturou výsledků a summary
* **Kódy odpovědí:** 200, 400, 401, 500

---

## Vzorový prompt pro interpretaci výsledku

```plaintext
Jsi zkušený lékařský asistent, specializovaný na vysvětlování laboratorních výsledků...
```

---

## Vzorový testovací vstup a výstup

**Ukázka vstupu:**

```
Glukóza (plazma) 7.1 mmol/L (4.0 – 5.5)
Cholesterol celkový 5.2 mmol/L (do 5.0)
...
```

**Ukázka výstupu (JSON):**

```json
{
  "results": [...],
  "summary": "Hladina glukózy je zvýšená..."
}
```

---

## Deployment a CI/CD

* **Lokální prostředí:** Docker + uvicorn
* **Staging prostředí:** Heroku/Azure/AWS
* **Produkční nasazení:** orchestrátor (Kubernetes, ECS)
* **CI/CD:** GitHub Actions/GitLab CI, build, test, deploy

---

## Využití Codex (AI asistence) při vývoji

* Popis problému v komentářích
* Postupné malé úlohy
* Generování testů
* Refaktorování a dokumentace
* Použití v IDE (Copilot)
* Prompt in README
* Školení týmu

---

*Poznámka: Tento dokument slouží jako úvodní "kickstart" pro tým. Další podrobnosti se mohou upřesňovat za pochodu.*
