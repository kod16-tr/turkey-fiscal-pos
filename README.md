# Turkey Fiscal POS & e-Document Compliance — Agent Skill

> ⚠️ **Not legal, tax or professional advice.** This skill summarizes public rules and gives engineering patterns. Rules and yearly amounts change; confirm with the competent authority and a licensed Turkish professional before go-live.
>
> **About "[verify]" items:** a statement marked **[verify]** could not be confirmed against the official text when this version was written (for example a draft guideline, an unclear effective date or a secondary source only). Treat it as an open question, check the linked source, and open an issue or pull request if you can confirm or correct it.

An open [Agent Skill](https://agentskills.io) that teaches AI coding assistants how to build checkout, POS, ordering and e-commerce software that is compliant with Turkey's fiscal rules:

- **ÖKC / yazarkasa** fiscal devices (new-generation ÖKC, EFT-POS ÖKC, Android POS) and GİB's role
- Integration patterns: vendor REST/HTTPS, serial/USB, cloud — sale → payment → fiscal document → slip, plus void, refund and **Z report**
- **Which document when:** ÖKC receipt, e-Arşiv Fatura, e-Fatura, e-Adisyon, information slip, invoice threshold
- **VAT (KDV)** 20 / 10 / 1 %, product mapping, rounding, discounts, service charge
- **Meal cards** (Multinet, Pluxee/Sodexo, Edenred, Setcard, Metropol), split tender, external payment providers
- Common mistakes and a go-live **test checklist**
- Short summaries in **Turkish, German and Arabic**


## Who is it for?
Developers of foreign POS, e-commerce, reservation and food-ordering platforms entering Turkey, and Turkish developers who want a structured checklist.

## Contents
```
turkey-fiscal-pos/
├── SKILL.md                     # entry point (frontmatter + short workflow)
├── README.md
├── CHANGELOG.md
└── references/
    ├── 01-okc-basics.md
    ├── 02-integration-patterns.md
    ├── 03-document-types.md
    ├── 04-vat-and-pricing.md
    ├── 05-meal-cards-and-payments.md
    ├── 06-pitfalls-and-test-checklist.md
    ├── sources.md
    ├── quickstart-tr.md
    ├── quickstart-de.md
    └── quickstart-ar.md
```
Markdown, example JSON and pseudocode only — no executable scripts.

## Installation
The folder name should match the skill name: `turkey-fiscal-pos`.

### Claude Code
```bash
git clone https://github.com/kod16-tr/turkey-fiscal-pos ~/.claude/skills/turkey-fiscal-pos
```
Or per project: put the folder under `.claude/skills/turkey-fiscal-pos/` in your repository. Claude loads it automatically when a task matches the description.

### Claude.ai / Claude Desktop
Zip the `turkey-fiscal-pos` folder and upload it under **Settings → Capabilities → Skills** (plan and admin settings permitting).

### Claude API
Upload the folder as a custom skill via the Skills API and attach it to your requests. See Anthropic's Agent Skills documentation.

### ChatGPT
ChatGPT does not load `SKILL.md` folders directly in every plan. Practical option: create a **custom GPT** (or Project), paste the body of `SKILL.md` into its instructions and upload the `references/*.md` files as knowledge. If you use OpenAI Codex, which supports the Agent Skills format, place the folder in its skills directory (check current Codex docs).

### Cursor
If your Cursor version supports Agent Skills, place the folder in the project's skills directory per Cursor docs. Otherwise add a project rule (e.g. `.cursor/rules/turkey-fiscal-pos.mdc`) that contains the `SKILL.md` body and tells the agent to read files in `references/` when needed.

### VS Code (GitHub Copilot)
Recent Copilot agent mode supports Agent Skills: place the folder at `.github/skills/turkey-fiscal-pos/` in your repository (check your VS Code / Copilot version). Older versions: copy the `SKILL.md` body into `.github/copilot-instructions.md`.

## Example prompts
- "We are launching our restaurant POS in Istanbul. Which fiscal documents do we need and how do we integrate with an Android POS ÖKC?"
- "Review this checkout flow for Turkey: split payment with Multinet + credit card."
- "Our receipt total differs by 0.01 TRY from the device. Why?"

## Contributing
Issues and pull requests are welcome. Every regulatory change must include a public source link (GİB, Resmî Gazete, ministry, or a reputable professional body) and the date it takes effect. Do not submit vendor-confidential documentation.

## License
[CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) — see [`LICENSE`](LICENSE). You may share and adapt this content, including commercially, with attribution to **KOD16 Digital Solutions (KOD16 Team)**.

## Disclaimer
Provided "as is", for information only. Not legal, tax or accounting advice. Trademarks belong to their owners; mention of a brand does not imply endorsement or partnership.

---
Need help? KOD16 Digital Solutions, info@kod16.com.tr
