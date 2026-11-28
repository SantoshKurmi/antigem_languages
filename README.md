# AntiGem Languages

Translations of the [AntiGem](https://github.com/Santoshkurmi/antigem) Android app, made by the people who use it.

The app itself ships only English. Every other language lives here, so the app stays small, any language can be
added or fixed at any time without a new app release, and no language gets a special place.

## Use a language

In the app: **Settings → Language → Get more languages**. The list comes from this repository. Tap **Download**, then
tap the language to show the app in it.

- When a translation you downloaded gets better here, the app shows **Update** the next time you open the Language page.
- Downloaded languages can't be edited, so an update never overwrites your changes. To change one, tap **⋮ → Duplicate**
  and edit the copy. Your copy is yours: updates don't touch it.
- A language with some texts missing still works: English shows for those texts.
- An AI agent can do all of this too, through the app's Language MCP server (`language_catalog`, `language_download`).

## Languages

<!-- languages:start -->
| Language | | Translated | By | File |
|---|---|---|---|---|
| Arabic | العربية | 100% | [AbdulAziz-Hatem](https://github.com/AbdulAziz-Hatem) | [ar](languages/ar/ar.json) |
| Chinese (Simplified) | 简体中文 | 100% | [Zmin](https://github.com/Zmin2003) | [zh-hans](languages/zh-Hans/zh-hans.json) |
| Pirate English (TEST) · Test only, not for use | Pirate Speak | 58% | [AntiGem](https://github.com/Santoshkurmi) | [en-pirate-test](languages/en/en-pirate-test.json) |
| Russian | Русский | 87% | [kuprizzz](https://github.com/Selyrith) | [ru](languages/ru/ru.json) |
| Turkish | Türkçe | 90% | [muazzezwq](https://github.com/muazzezwq) | [turkish](languages/tr/turkish.json) |
| Vietnamese | Tiếng Việt | 91% | AntiGem AI, [anhthao121](https://github.com/anhthao121) | [vi](languages/vi/vi.json) |
<!-- languages:end -->

The table and [`index.json`](index.json) are rebuilt automatically after every change.

> **Pirate English (TEST)** is a test pack, not a real translation. It's here to try downloading, updating and
> removing a language, and its texts are silly pirate speak made by swapping words. Please don't use it for real.

## Add a new language: step by step

The example adds **Chinese (Simplified)**. Replace the names and codes with your language's.

### 1. Pick the code and the file name

| | Example | Rule |
|---|---|---|
| Language code | `zh-Hans` | A [BCP 47](https://www.w3.org/International/articles/language-tags/) code: `ne`, `hi`, `pt-BR`, `zh-Hans`, `sr-Latn`. Add a region or script only when it matters. |
| Folder | `languages/zh-Hans/` | Exactly the language code, same upper and lower case. |
| File name (the pack's **id**) | `zh-hans.json` | Lowercase letters, digits and hyphens, unique in this repository. Use the code for the main pack. |
| Another pack of the same language | `zh-hans-formal.json` | The code plus a word, and set `"variant": "Formal"` inside. |

Check the [list above](#languages) first. If your language is there, improving that pack is usually better than
adding a second one (see [Update a language](#update-a-language-that-is-already-here)).

### 2. Translate

Choose one:

- **In the app (easiest).** Settings → Language → **New language**. Fill in the name in English (`Chinese (Simplified)`),
  the name in the language (`简体中文`), the code (`zh-Hans`) and the direction. Tap the language to show the app in
  it, then **⋮ → Edit texts**: the **To translate** filter shows what's left, and edits save as you type.
- **With an AI agent.** Turn on the **Language** MCP server for your agent (the agent's MCP settings → Language). In
  Settings → Language → **Translate with AI**, tap **Copy a prompt** and paste it into a chat. The app changes on screen
  while the agent works. A person who speaks the language must read the result.
- **By hand.** Copy [`en.json`](en.json) (or, in the app, English **⋮ → Save as a template**) and translate the texts
  in any editor. Delete the `notes` block. You can leave out keys you don't translate: English shows for them.

Keep every `{placeholder}` exactly as it is, and keep button labels short. All the rules are in
[CONTRIBUTING.md](CONTRIBUTING.md#rules-for-the-texts).

### 3. Add your name and details

In the app: **⋮ → Name & details**. Add a description, a variant if needed, and everyone who worked on it (name,
GitHub username, what they did). By hand, fill in the top of the file:

```json
{
  "format": "antigem-language",
  "format_version": 2,
  "code": "zh-Hans",
  "name": "Chinese (Simplified)",
  "native_name": "简体中文",
  "variant": "",
  "rtl": false,
  "description": "Everyday Simplified Chinese for the whole app.",
  "authors": [
    { "name": "Li Wei", "github": "liwei", "role": "Translation" }
  ],
  "strings": { "common.cancel": "取消", "…": "…" }
}
```

Chinese, Japanese and some other languages have only one plural form: a plural text is just
`{ "other": "{count} 个文件" }`. The app's editor shows the forms your language needs.

### 4. Send it

Choose one.

**A. With the form (no git needed).**

1. In the app: **⋮ → Send to the community → Save the file**.
2. Open **[Share a translation](../../issues/new?template=share-translation.yml)**. Fill it in, attach the file (zip it
   first if GitHub refuses a `.json` file), tick the license box and submit.
3. A maintainer adds it to the repository and credits everyone you listed.

**B. With a pull request, using git.**

1. On GitHub, **Fork** this repository.
2. Then:

   ```sh
   git clone https://github.com/YOUR-NAME/antigem_languages
   cd antigem_languages
   git checkout -b add-zh-hans
   mkdir -p languages/zh-Hans
   cp ~/Downloads/antigem-language-chinese-simplified.json languages/zh-Hans/zh-hans.json
   python3 tools/build_index.py --check languages/zh-Hans/zh-hans.json
   git add languages/zh-Hans/zh-hans.json
   git commit -m "Add Chinese (Simplified)"
   git push -u origin add-zh-hans
   ```

3. On GitHub, click **Compare & pull request**, tick the checklist (including the license) and create the pull request.

**C. With a pull request, in the browser.**

1. On GitHub, **Fork** this repository.
2. In your fork: **Add file → Create new file**. Type `languages/zh-Hans/zh-hans.json` as the name (the `/` makes the
   folders) and paste the whole file.
3. **Commit changes → Create a new branch → Propose changes**, then create the pull request.

You don't change `index.json` or the table in this README: they're rebuilt after the merge.

### 5. What happens next

1. The pull request runs the check. If something is wrong, GitHub marks the exact problems on your file
   (see [Fix check errors](#fix-check-errors)). Push a fix to the same branch and it runs again.
2. A maintainer reviews it, ideally with someone who reads the language, and merges it.
3. A workflow rebuilds `index.json`. Within a few minutes, every app lists the language under
   **Get more languages**, with your names on it.

## Update a language that is already here

1. **Get it into the app.** Download it (Get more languages → **Download**), then **⋮ → Duplicate**. Downloaded
   languages are read-only. The copy is yours to edit, and it remembers which pack it came from.
2. **Improve it.** **⋮ → Edit texts.** The **Outdated** filter shows texts whose English changed since they were
   translated, and **To translate** shows new ones.
3. **Add yourself.** **⋮ → Name & details.** Add yourself to the people and keep everyone already there.
4. **Send it.**
   - **With the form:** as in [step 4A](#4-send-it). Keep the language code and variant as they are: that's how
     your file finds the pack it updates.
   - **With a pull request:** replace the pack's existing file. Keep the same path and file name, because the app
     knows a downloaded language by its id. A new name would be a new language for everyone.

     ```sh
     git checkout -b update-zh-hans
     cp ~/Downloads/antigem-language-chinese-simplified-copy.json languages/zh-Hans/zh-hans.json
     python3 tools/build_index.py --check languages/zh-Hans/zh-hans.json
     git commit -am "Chinese (Simplified): translate the new texts"
     git push -u origin update-zh-hans
     ```

     In the file, set `"name"` back to the pack's name (a copy is named "… (copy)"). The `based_on` field can stay.

After the merge, everyone who downloaded the language sees **Update** the next time they open Settings → Language.

## Check a file yourself

You need Python 3.8 or newer, nothing else. On Windows, type `python` instead of `python3`.

```sh
python3 tools/build_index.py --check languages/zh-Hans/zh-hans.json   # one file
python3 tools/build_index.py --check                                  # every pack
```

Each file gets a line like this:

```
languages/zh-Hans/zh-hans.json           ok  6950/7262 texts, 12 outdated, 2 warnings
```

**Errors** stop a pack from being published and fail the pull request. **Warnings** are only advice.
Your editor can also check the file as you type: point it to
[`schema/antigem-language.schema.json`](schema/antigem-language.schema.json) (in VS Code, add
`"$schema": "../../schema/antigem-language.schema.json"` at the top of the file).

### Fix check errors

| The check says | Fix |
|---|---|
| `"code" is "zh" but the folder is languages/zh-Hans` | Make the folder and `"code"` the same, including upper and lower case. |
| `the file name "Zh_Hans" is the pack id: use lowercase letters, digits and hyphens` | Rename the file, e.g. `zh-hans.json`. |
| `the id "zh-hans" is taken by …` | Another pack has that file name. Pick another, e.g. `zh-hans-formal.json`. |
| `{nam} is not in the English text (English has {name})` | A placeholder was changed or translated. Copy it exactly from English. |
| `English has plural forms here, give {"one": …, "other": …}` | Write that text as an object of plural forms. `other` is always needed. |
| `English is a plain text here, not plural forms` | Write that text as a plain string. |
| `plural forms need "other"` | Add the `other` form. |
| `unknown plural form …` | Use only `zero`, `one`, `two`, `few`, `many`, `other`. |
| `"authors" is required` / `authors[0] needs a "name"` | Add at least one person with a name. |
| `authors[0].github "…" is not a GitHub username` | Use just the username, like `liwei`, without `@` or a link. |
| `not valid JSON` | A comma or quote is missing near the line it names. A JSON validator or VS Code shows where. |
| `the file starts with a byte order mark (BOM)` | Save the file as "UTF-8", not "UTF-8 with BOM". |
| `keys are not in today's English` (warning) | Texts the current app no longer has, or texts from a newer app version. They're harmless and kept. |
| `leaves out {name}` (warning) | The translation drops a value the app fills in. Usually it's better to keep it. |

## Problems

- A wrong, odd or too long text? [Report it](../../issues/new?template=translation-problem.yml).
- The file format and every field: [CONTRIBUTING.md](CONTRIBUTING.md#the-file).

## How it works

```
languages/<code>/<id>.json     one translation ("pack"): ne/ne.json, pt-BR/pt-br.json, hi/hi-latn.json …
en.json                        the app's English texts: every key a translation can have (synced from the app every day)
index.json                     the list the app reads, rebuilt by a workflow: never edit it by hand
schema/                        JSON Schema of a pack (editors use it to check your file as you type)
tools/build_index.py           checks every pack and writes index.json and the table above
```

- **Who is who:** a pack's **id** is its file name and is unique in this repository. Several packs can exist for one
  language (`hi.json`, `hi-latn.json` for Hindi in Latin letters). The **variant** field tells them apart in the app.
- **Credits:** every pack lists its `authors` (name, GitHub username, role). The app shows them on the language's
  details, with links to their GitHub profiles.
- **Checks:** every pull request runs `tools/build_index.py --check`. A text with a `{placeholder}` that isn't in the
  English text, or plain text where English has plural forms, fails the check, so a broken pack never reaches the app.
- **Updates:** when a pack changes, its SHA-256 in `index.json` changes and the app offers the update. Each download
  is checked against that SHA-256 before it's saved.
- **Outdated texts:** a pack's `sources` map records which English each text was translated from. When the English
  text changes in a newer app version, the app and the index mark that text as outdated.

## For maintainers

```sh
python3 tools/build_index.py --check   # check every pack (what pull requests run)
python3 tools/build_index.py           # check, then write index.json and the table above
```

**Adding a translation sent with the form:** add the `create-pr` label to the issue. A workflow
(`.github/workflows/share-translation.yml`) downloads the attached file and works out from it where it goes: its
`code` is the folder, and the pack here with the same code and variant is updated (its texts replace the old ones,
every author stays); otherwise it's a new `languages/<code>/<id>.json`. It checks it, opens a pull request that closes the issue and
comments the link. If the file has problems, it explains them on the issue and removes the label: add it again once
the issue has a fixed file. On the pull request, click **Approve workflows to run** (GitHub holds the check on pull
requests opened by the bot), then review it, approve it and merge it.

**Owners update their own packs:** a pack's owners (in `.github/pack-owners.json`: its creators, recorded when it's
first published, plus anyone you add there) can publish updates to it without you, unless an update changes the
code, removes authors, or drops many texts. Others who help are credited in `authors` but reviewed by you. See
[CONTRIBUTING.md](CONTRIBUTING.md#updating-your-own-pack).

**Updates made on an old copy** can't undo newer texts: `tools/pack_history.py` finds, in the pack's history, the
version an update was made from and takes only the texts its sender changed since then. Texts changed both by the
sender and in the pack since then are listed for you; an owner's update with such texts, or a pull request that
brings back older texts, waits for your review instead of being published automatically.

- `.github/workflows/check.yml` checks every pull request with `main`'s own tools. Pull requests from anyone but
  the owner may only change `languages/`.
- `.github/workflows/publish.yml` runs on every push to `main`, every day and by hand. It fetches the app's
  current `en.json`, rebuilds `index.json` and this table, and commits them when they changed.

## License

The translations are © their authors (listed in each pack's `authors`) and are licensed under the
[GNU General Public License v3.0](LICENSE) or any later version, the same license as the AntiGem app.
They translate the app's own texts, so they share its license. By sending a translation (a pull request or the
"Share a translation" form), you agree to share it under this license.
