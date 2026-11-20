# Q-TRACE

Q-TRACE is an open web tool for documenting the early development of a trait questionnaire: for each of eight stages you record what you decided and why, and for each item where it came from, what evidence was collected about it, and which decision followed. It calculates the content validity indices (I-CVI and S-CVI/Ave) from uploaded expert ratings and exports the whole development record as a readable report and as a data file. The tool accompanies the paper *Behind the Scales: Q-TRACE, an Open Protocol for Documenting Early Decisions in Trait Questionnaires*, which describes the eight stages, their checklists, and their default rules.

## Use

Open the tool in a browser and choose **New project**, **Open project (import file)**, or **Load example**. The example is a small fictional project with two facets and six items.

- **Stages 1–8.** Each stage has a short explanation, a checklist, the default rule with its source, a choice (rule followed / deviation / not applicable), a justification field, and links to guidance and tools.
- **Item table.** Every item has an ID, a facet, a source, and versions. Editing the wording creates a new version; evidence and decisions are linked to the item version. A decision can apply to several items at once, and a return to an earlier stage is recorded as a decision.
- **Expert ratings (Stage 6).** Upload a CSV file with the columns `expert_id, expert_type, item_id, item_version, relevance, comment`, where `expert_type` is `domain` or `population` and `relevance` is 1–4. Ratings of 3 and 4 count as relevant. I-CVI = number of experts rating 3 or 4 ÷ number of experts who rated the item; S-CVI/Ave = the mean of the I-CVIs. Items below .78 are flagged, and the tool warns when there are fewer than six experts. See [`example-expert-ratings.csv`](example-expert-ratings.csv).
- **Export and import.** *Export report* gives an HTML report that can be printed or saved as a PDF. *Export data file* gives one JSON file with the whole project; *Import* opens it again. Archive the data file in an open repository (e.g., Zenodo, OSF, Open Test Archive).

## Privacy

There is no server, no login, and no database. All project data are stored locally in the browser (`localStorage`) and are not sent anywhere; the page makes no network requests after it has loaded, and a Content Security Policy blocks them. The tool does not run language models: for overlap checks it refers to public tools and records their outcome.

## Run locally

The tool is a single file. Open `index.html` in a browser, or serve the folder with any static web server. There is no build step and there are no dependencies.

## Data format

The data file is JSON: `{ "format": "q-trace", "version": 1, "exportedAt": "…", "project": { … } }`. The project holds the project details, facets, the status and justification per stage, all versions of the construct definition, the items with their versions, the evidence, the decisions, the uploaded expert ratings, and the final versions.

## License

MIT, see [LICENSE](LICENSE).
