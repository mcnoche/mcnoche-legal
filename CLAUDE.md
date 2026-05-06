# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A three-page static HTML site that serves as the **public messaging-compliance documents** for the **McKnight Notification Service** — a personal, single-recipient Twilio SMS application operated by Mike McKnight as a sole proprietor.

The pages exist primarily to satisfy Twilio 10DLC / A2P registration requirements, which mandate publicly reachable Privacy Policy and Terms pages whose URLs can be submitted with the campaign brand registration.

- `index.html` — landing page linking to the two policies
- `privacy-policy.html` — privacy policy
- `terms.html` — terms & conditions

Each file is hand-edited HTML with inline `<style>` (no shared stylesheet, no JS, no build step, no package manifest). Content is the substance of this repo; markup is incidental.

## Hosting

Served via **GitHub Pages** from the `main` branch at the repo root: <https://mcnoche.github.io/mcnoche-legal/>. Push to `main` → Pages rebuilds automatically. There is nothing to build, lint, or test locally; opening the file in a browser (`open index.html`) is sufficient for visual checks.

## Repository visibility — important exception

This repo is **public**, and that is intentional. The global "private-by-default" rule in `~/.claude/CLAUDE.md` does **not** apply here: Twilio's 10DLC review fetches these URLs anonymously, so the Pages site (and therefore the source repo, since Pages is served from `main`) must be publicly readable. Do not propose flipping this repo to private.

## Editing guidance

**Keep the three pages visually consistent.** They share an identical CSS block (font stack, `.container`, headings, `.meta`, footer). When you change one page's styling, change all three — there is no shared stylesheet to do it for you.

**Bump dates correctly when content changes.** Both policy pages carry two date lines in `.meta`:
- `Effective Date` — the date the policy first took effect; only change this if the user explicitly says so.
- `Last Updated` — bump to today's date on any substantive content edit.

The footer of `index.html` carries a single `Effective` date — leave it unless the user is intentionally re-issuing the documents.

**Don't rewrite the service description as if it's consumer-facing.** The policies deliberately describe a one-person, one-recipient, hard-configured Twilio sender (no sign-up, no third-party data, transactional only). That framing is load-bearing for the 10DLC application and for the limitation-of-liability posture; rewording it to sound like a normal SaaS privacy policy would misrepresent the service.

**Twilio 10DLC content requirements that must stay present in any rewrite of the messaging sections:**
- Explicit `STOP` opt-out instruction and `HELP` instruction
- "Message and data rates may apply"
- A statement of message frequency (current text: "Message frequency varies…")
- Identification of Twilio as the SMS delivery provider with a link to Twilio's privacy policy
- Statement that messages are transactional (not marketing/promotional)

Removing any of these can fail campaign review.

**Cross-links between pages must keep working.** `terms.html` references `privacy-policy.html`; both policy pages link back to `index.html`. If you rename a file, update the links in the other two.

## Workflow

This is a `mcnoche/` org repo, so the global "no PR required" carve-out applies — branch for significant work as usual (per the global branching rule), but **merge locally and push** instead of opening a PR. GitHub Pages rebuilds from `main` within ~1 minute, so a `git push` to `main` is effectively a deploy; eyeball the diff before pushing since these pages are externally fetched by Twilio's reviewers.
