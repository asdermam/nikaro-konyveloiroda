# Nikaro Könyvelőiroda — build log

Demó weboldal a workflow (AI WORKFLOW vault) szerint. Lead #4.

## Step 1 — Kontextus
- **Cég:** Nikaro Könyvelőiroda (könyvelőiroda)
- **Cím:** 2113 Erdőkertes, Sándor utca 35.
- **Telefon:** 06 30 281 6620 · **E-mail:** nikaroteam@gmail.com
- **Szolgáltatások:** teljes körű könyvelés, bérszámfejtés, adótanácsadás, hatóságokkal való kapcsolattartás — Bt / Kft / egyéni vállalkozók
- **Pozicionálás:** precizitás, naprakészség, több éves tapasztalat, megbízhatóság
- Forrás: https://kertesivallalkozasok.hu/item/nikaro-konyveloiroda/

## Step 2 — ChatGPT prompt + dizájn kutatás
A ChatGPT (browser) által adott tartalmi/strukturális terv (ezt a TARTALOMHOZ használjuk; a kódot és a vizuális dizájnt Claude készíti, ChatGPT in-code dizájnt NEM adunk):

Szekciók: Hero → Probléma/fájdalompont → Szolgáltatások → Kinek ajánljuk → Miért a Nikaro → Helyi jelenlét (Erdőkertes) → Folyamat → Bizalmi üzenet → GYIK → Záró CTA → Kapcsolat (űrlap) → Footer.
Hangnem: magyar, magázódó, prémium de visszafogott, professzionális, nyugodt, bizalomépítő; kerülni a túlzó ígéreteket ("garantált adómegtakarítás" stb.); helyette "precíz munkavégzés", "naprakész szakmai háttér", "átlátható együttműködés". Fő CTA: "Ajánlatot kérek" / "Telefonos kapcsolatfelvétel".

Dizájn kutatás (awwwards / finance): prémium, szerkesztőségi (editorial) megjelenés serif tipográfiával (pl. Avalon Accounting — meleg krém + bold serif), nem a szokásos "vállalati kék". Ezt követve NEM generikus.

**Választott dizájn irány (Claude sajátja):** meleg krém/papír + mély fenyőzöld + visszafogott sárgaréz akcent; serif display (Fraunces) + tiszta grotesque body + mono a "főkönyvi" tabuláris számokhoz. Nyugodt, precíz, bizalomkeltő.

**Stack:** React + Tailwind (Vite), egyetlen önálló HTML-be bundle-ölve (vite-plugin-singlefile) a publikáláshoz. Tesztelés: Playwright MCP.

## Step 3 — Build & test

**Build:** Vite + React 18 + Tailwind v4, `vite-plugin-singlefile` → egyetlen `dist/index.html` (~204 kB, minden inline). Fontok: Fraunces (serif display), Hanken Grotesk (body), IBM Plex Mono (labelek/számok). Paletta: krém papír + fenyőzöld + sárgaréz.

Szekciók: Header (sticky + mobil menü) · Hero (serif H1 + kép + „Amit kap" kártya + kontakt sáv) · Probléma · Szolgáltatások (4 kártya) · Miért minket (fenyőzöld, 4 bizalmi pont + CTA kártya) · Kinek ajánljuk · Folyamat (4 lépés) · GYIK (React accordion) · Kapcsolat (fenyőzöld, űrlap mailto-val) · Footer.

**Tesztelés (Playwright MCP, `http://localhost:5173` a build-elt fájlon):**
- Console: 0 hiba, 0 figyelmeztetés (a kezdeti favicon 404-et javítottuk — inline SVG favicon).
- Reszponzivitás: 375 / 390 (mobil) és 1440 (desktop) — a layout minden töréspontnál rendben, tartalom hiánytalan.
- Interakciók: GYIK accordion nyit/zár (grid-rows-[0fr]↔[1fr]) ✓ ; mobil menü nyílik/záródik, 6 link ✓.
- Hero kép betölt (könyvelés-releváns), gradient fallback ha nem.

**Javítások:** favicon 404 → inline SVG favicon hozzáadva, újrabuild → 0 console hiba.

## Step 4 — Publikálás (GitHub)
_(következik)_
