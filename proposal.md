
# Ceph docs rebuild

*A proposal to the Ceph documentation team. Emmanuel Ameh, September 2026. Draft for review.*

## Where I am after six months

Since April, I have worked auditing the docs, filing what was wrong, fixing the dangerous and the obvious, and learning how the project reviews and ships. That was the right first step, and it is not finished, but it is not a strategy. It fixes pages; it does not change or improve how our docs are consumed.

Where that stands today:

- 65 defects found and filed
- 30 fixed or in review
- 43 pull requests merged
- 34 still open

I will keep working the remaining 34 in the background, about a day a week, folded into whichever section is being rebuilt. The rest of this document is about what I want to do instead of more of that.

## What I am proposing

Stop treating the docs as pages to fix. Rebuild them, top to bottom, around what the reader is trying to do, in modular pages that can be reused, checked, and read by machines as easily as by people.

Some context on where we start. All of this was checked against `main` on 2 September 2026 (commit `d78578929f9`) and against the live site.

- The docs are organised by daemon and module. There are 26 entries in the sidebar, eleven of them single pages, arranged the way Ceph is built rather than the way it is used. The landing page has no map of its own and points first-time users at the developer guide.
- The procedures a new user meets first (installing packages, creating a pool for a service, creating a client user) appear on five to seven pages each, and they have drifted. Two of the seven client-user copies leave out a capability the canonical page says is required.
- No page carries metadata. Nothing records which release a page applies to or when it was last true.
- An AI assistant asking about Ceph gets HTML by default, with no index and no metadata to cite. Read the Docs can already serve a Markdown version of each page, but nothing points to it.

Three changes fix that.

## 1. A new architecture: seven doors, one shape

The top level becomes seven doors, ordered by the reader's journey. Inside every storage service the same five parts appear in the same order, so once you have learned one section you can find your way around all of them.

Today's top level, 26 sidebar entries on `main`, by component:

> start, install, cephadm, rados, cephfs, rbd, radosgw, csi, mgr, mgr/dashboard, monitoring, api, architecture, Developer Guide, dev/internals, governance, Technical Charter, foundation, ceph-volume, crimson, releases/general, releases, security, hardware-monitoring, Glossary, Tracing

What I propose instead. "Pages today" is how many existing pages map to each door.

| Door | Pages today | What it holds |
|---|---:|---|
| 1. Start here | 13 | What Ceph is, the architecture in brief, choosing a deployment and a release, quick starts |
| 2. Deploy | 21 | cephadm first, Rook and CSI on Kubernetes, requirements, Windows clients, and one upgrade hub for steps that are spread over five places today |
| 3. Operate | 72 | Day-two cluster operations: pools, CRUSH, monitoring, dashboard, security, manager modules, maintenance |
| 4. Storage services | 190 | Block (RBD, NVMe-oF, legacy iSCSI), File (CephFS, NFS, SMB), Object (RGW), Kubernetes (CSI), each in the same shape |
| 5. Troubleshoot | 11 | One hub keyed by symptom, over the seven troubleshooting pages and 96 health-check codes that exist today, plus the pages that are missing for Block, NVMe-oF, SMB and CSI |
| 6. Reference | 141 | Configuration options, CLI and man pages, APIs, release notes. 36 percent of options and the full command tree are generated from source today; the rest should follow |
| 7. Develop and contribute | 168 | Developer guide, internals, docs guide, governance, foundation, technical charter |

The shape inside every service: **Learn, Set up, Operate, Troubleshoot, Reference.**

Nothing gets deleted. All 616 pages already have a home in the seven doors (see the [door map](door-map/), which goes page by page). Pages are mapped into the new navigation first and moved behind redirects later. About 90 of the 616 need rewriting; the other 526 need metadata and a new home only.

The tree half does this already. The CephFS index groups its pages into concepts, administration, mounting and troubleshooting, but hides the headings. The RADOS section is split into configuration, operations, troubleshooting and APIs. The new CSI chapter uses one page shape for all four backends. This change makes that visible everywhere and finishes it.

Others have done this. Kubernetes organises its docs as Getting started, Concepts, Tasks, Tutorials, Reference and Contribute. The Diataxis model, whose four types Django's documentation is organised around, has been adopted by Canonical, Cloudflare and Gatsby.

## 2. Modular pages: three types, one template

Every page becomes one of three types and follows one template.

- **Concept.** Explains one idea the reader needs before acting. No commands, no steps.
- **Procedure.** One task, numbered steps, one command per step, the output you should see, and how to verify it worked.
- **Reference.** Facts to look up rather than remember: options, commands, limits. Generated from source where possible.

A procedure page, using "Create an erasure-coded pool" as the example:

| Part | Content |
|---|---|
| Metadata | type: procedure. applies to: Squid, Tentacle. reviewed: 2026-09. owner: rados |
| Before you start | Cluster health, permissions, an EC profile chosen |
| Steps | Numbered. One command each, with the output you should see |
| Verify | The command that proves it worked |
| If it fails | The two or three most common failures and what they mean |
| Related | The concept behind it, the reference for every option |

Repeated procedures get written once, in a shared snippet directory, and included where needed, with per-page substitutions for things like the pool or user name, so they cannot drift apart. Today the whole tree uses three `include` directives and one substitution. The first conversions pay for themselves: creating a pool for RBD images is written out six times inside the Block section alone, and only one of those copies verifies the result.

The template is the contract that keeps the tree consistent, and it is also what makes the pages machine-readable.

Others have done this too. Red Hat's modular documentation model (concept, procedure and reference modules, assembled into user stories) is what the downstream Red Hat Ceph Storage guides already use, with Prerequisites, Procedure and Verification headings. IBM Storage Ceph uses the same shape under DITA labels.

## 3. Agent-ready: docs that machines can read, cite and trust

More and more readers put their Ceph questions to an AI assistant, and those assistants fetch docs.ceph.com. Today they get HTML by default, with no index and no metadata to cite. A Markdown rendering and the raw source already exist on the site; nothing points to them, and no page says which release it applies to. The rebuild publishes the docs in the forms agents consume, and lets the template's metadata travel with every page. Most of this is build configuration on top of changes 1 and 2. The source stays reStructuredText: the Markdown copies and the `llms.txt` index are generated by the build, the same way the HTML is today, so nobody writes or maintains them by hand. docs.ceph.com is hosted on Read the Docs, which serves these files from the site root once the build emits them.

| What agents need | Today | After the rebuild |
|---|---|---|
| An index of the docs | `llms.txt` and `llms-full.txt` return 404 at the root and under every version; the sitemap lists ten version roots and no pages | `llms.txt` and `llms-full.txt` emitted by the build (sphinx-llm, the extension Read the Docs recommends) and served at the root from `latest` |
| A generated plain-text copy of each page | Two forms exist but nothing advertises them: raw source under `_sources`, and a Markdown rendering Read the Docs returns when asked for `text/markdown`. No `.md` URLs, no link from any page, no front matter | A Markdown rendering of every page, produced by the build at a stable `.md` URL, listed in `llms.txt`, carrying title, release and review metadata. The `.rst` source is untouched |
| Page metadata | 0 of 612 live pages carry content metadata: no description, canonical URL, applies-to release, review date or owner | Type, applies-to releases, last reviewed and owner on every page; canonical URLs set in the build |
| Machine-readable reference | The build already reads the option YAML and command tables to render HTML; 36 percent of options reach a page and the full command list sits on one hidden page | Every option and command rendered, and published as JSON next to the pages, from the same sources |
| Stable, citable anchors | 318 of 612 pages have no named anchor; section ids change whenever a title changes | Every page and every procedure carries a named label, enforced by a build check |
| Direct query | A Read the Docs search API and a Sphinx inventory exist, discoverable only if you already know about them; no MCP server | Stretch goal: a Ceph docs MCP server over the Markdown and JSON outputs, usable by agents and by the dashboard |

For the record: `llms.txt` is served by Anthropic, Cloudflare, GitHub and AWS, and by 87 of the top 1,000 sites (8.7 percent, Tranco list, June 2026). Cloudflare and Cash App serve a Markdown copy of every page. Read the Docs serves `llms.txt` from the site root of the default version once the build emits it.

## When you would see what

Each step ends with something visible on docs.ceph.com. The source stays reStructuredText throughout. The dates are proposals; I would like to confirm them with the team.

### Step 1, Sep to Oct 2026: The new front door

Change the front of the site. Move nothing.

- Rewrite the landing page: seven visible entry points with a sentence each, instead of a feature list and a hidden table of contents.
- Add seven door pages. Each lists the existing pages that belong to it, where they live today. Sphinx lets an index point at any page, so nothing moves.
- Regroup the service indexes (RBD, CephFS, RGW, CSI) under five headings: Learn, Set up, Operate, Troubleshoot, Reference. CephFS already has these groups, hidden in comments.
- Add the Troubleshoot page: links to the seven troubleshooting pages that exist and to the health-checks page.
- Two small fixes: give the generated command reference a title and a home under Reference; put the block quick start under Start here.
- One build change: add the sphinx-llm extension so each build also emits the llms.txt index and a Markdown rendering of every page. The .rst source is untouched.
- Agree the page template with the team, on paper. No pages are converted yet.

**You will see:** docs.ceph.com opens on seven clear ways in, the sidebar follows them, every existing URL still works, and agents get an index and a plain-text copy of every page.

### Step 2, Nov to Dec 2026: First service rebuilt

Rebuild one section completely, as the model for the rest.

- Block (RBD, 41 pages) is the proposal: the smallest and calmest section, and it has no troubleshooting page today.
- Land named anchors on every RBD page first, so links keep working when pages split. 34 of the 41 have none today.
- Rewrite the nine core pages (commands, snapshots, mirroring, live migration, encryption, the two caches, Windows, the index) into about thirty modular pages on the template: one task per page, with metadata and a verify step.
- Write the Troubleshoot part from nothing: three to five symptom-led pages.
- Re-home the 28 client and gateway pages with metadata only. iSCSI stays behind its maintenance banner; the Kubernetes and Nomad pages move to the CSI door.
- Single-source the repeated procedures inside Block. "Create a pool for RBD images" is written out six times today.
- Add redirects for the pages that split, and review the result with the RBD reviewer.

**You will see:** one complete section in the new form, side by side with the old, and a conversion checklist other people can follow.

### Step 3, Q1 2027: The rest of the services and Operate

Repeat for the other user-facing sections.

- File (CephFS, 57 pages) goes first, because its index already has the shape. It proves the regroup path rather than the rewrite path.
- Object (RGW, 76 pages) leads on generated reference: half of it is API and option reference, and its flat index of about fifty entries gets the five headings.
- Cluster operations (72 pages) is already split by directory; each subdirectory becomes the matching door part.
- Deploy (cephadm and install, 42 pages): the duplicated install and upgrade procedures finally merge, and one upgrade hub replaces five places.
- Generated option reference grows from 36 percent toward all 2,166 options, one options file at a time.
- Conversions run from the step 2 checklist and are filed as tracker items, so other contributors can pick them up.

**You will see:** the user-facing tree fully in the new shape.

### Step 4, Q2 2027: Finish and lock it in

Finish, retire the old navigation, add checks so it stays this way.

- Developer docs (154 pages) consolidated into one track. The twenty or so operator pages hiding in dev/ move to their user doors.
- Old navigation retired on main. Release branches keep theirs until end of life, so redirects apply to latest.
- Build checks: every page has metadata and a named anchor, procedure pages carry the template's parts, and placeholders or broken cross-references fail the build.
- Configuration options and commands published as JSON next to the pages, from the same sources the HTML uses.
- A Ceph docs MCP server, if the stretch goal is approved.
- The first docs health report: open defects, option coverage, pages missing metadata, review latency.

**You will see:** a rebuilt docs.ceph.com, and checks that keep it that way.

In the background throughout: the 34 open register items close as each section is rebuilt, about a day a week. The cleanup never stops, but it no longer sets the agenda.

## What I need from the team

1. **Approve the direction.** The seven doors and the three page types. The [door map](door-map/) assigns all 616 pages to their new homes and lists the twenty or so judgment calls (manager modules, NFS and SMB, man pages, iSCSI) where I would like the team's view.
2. **Pick the first service.** Block (RBD) is my proposal: the smallest and calmest section (41 pages, 33 doc commits since 2025, five open doc issues), with a visible gap to close, since it has no troubleshooting page. CephFS follows. cephadm is the alternative, as a Deploy-door pilot, if that matters more to you.
3. **One reviewer per section.** A named subsystem reviewer for each door as it is rebuilt, so conversions get reviewed in days rather than months.
4. **Two weeks on the template.** Comments on the page template by mid-September; then it is frozen for the first rebuild and revised only after Block ships.

---

Figures verified 2 September 2026 against tracker.ceph.com, ceph/ceph `main` at commit `d78578929f9`, ceph/ceph.io, and the live docs.ceph.com site.

Sources: [Red Hat modular documentation reference guide](https://redhat-documentation.github.io/modular-docs/); [Red Hat Ceph Storage 8 installation guide](https://docs.redhat.com/en/documentation/red_hat_ceph_storage/8/html-single/installation_guide/index); [Canonical on Diataxis](https://canonical.com/blog/diataxis-a-new-foundation-for-canonical-documentation); [Diataxis](https://diataxis.fr/); [Kubernetes documentation](https://kubernetes.io/docs/home/); [Read the Docs llms.txt support](https://docs.readthedocs.com/platform/latest/reference/llms-txt.html); [sphinx-llm](https://github.com/NVIDIA/sphinx-llm); [llms.txt adoption, June 2026](https://www.rankability.com/data/llms-txt-adoption/); [Cloudflare, Markdown for agents](https://blog.cloudflare.com/markdown-for-agents/).
