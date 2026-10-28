# Schnellstart (Deutsch)

> Keine Rechts- oder Steuerberatung. Regeln ändern sich; prüfen Sie den aktuellen Stand bei der GİB (türkische Steuerverwaltung) und einem türkischen Steuerberater (mali müşavir).

**Grundregel:** Jeder Verkauf braucht einen fiskalischen Nachweis. Entweder druckt die Fiskalkasse (ÖKC, „yazarkasa") einen Fiskalbeleg, oder es wird eine e-Rechnung (e-Arşiv / e-Fatura) erstellt und die Kasse druckt einen Informationsbeleg (bilgi fişi). Nie beides für denselben Verkauf.

| Situation | Dokument |
|---|---|
| Ladenverkauf / Restaurant an Endkunden | ÖKC-Beleg |
| Betrag über der Rechnungsgrenze (2026: 12.000 TRY) oder Kunde verlangt Rechnung | e-Arşiv-Rechnung + Informationsbeleg |
| Käufer ist e-Fatura-Nutzer | e-Fatura |
| Onlineverkauf mit Lieferung | e-Arşiv-Rechnung |
| Tischservice, falls von der GİB verpflichtet | e-Adisyon |

**Ablauf:** Warenkorb → Zahlung (bar / Karte / Essenskarte / geteilt) → ÖKC schließt den Beleg → Belegnummer und Z-Nummer zurück an die App → speichern.

**USt (KDV):** 20 % Regelsatz, 10 % und 1 % ermäßigt (seit 10.07.2023). Jeder Artikel muss einer Abteilung/USt-Gruppe auf dem Gerät zugeordnet sein; Rundung pro USt-Gruppe wie das Gerät.

**Essenskarten:** Multinet, Pluxee (Sodexo), Edenred, Setcard, Metropol jeweils als eigene Zahlungsart führen.

**Tagesabschluss:** Keine offenen Verkäufe, an jedem Verkaufstag Z-Bericht, Abgleich nach USt-Satz und Zahlungsart.

**Häufiger Fehler:** Blindes Wiederholen nach Timeout (Doppelbeleg). Idempotenzschlüssel nutzen und zuerst den Gerätestatus abfragen.

Details: Dateien `01`–`06`, Quellen: `sources.md`.

Hilfe: KOD16 Digital Solutions, info@kod16.com.tr
