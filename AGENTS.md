<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.

## What Lovable manages

Rules outside this block are the project's own. Change the pieces below in
Lovable, not by hand. With the [Lovable MCP](https://mcp.lovable.dev)
connected, `send_message` asks Lovable to do it; otherwise ask the user to
use the editor.

- **Database.** Do not add or edit `supabase/migrations/` or `drizzle/`.
  Ask Lovable to change the schema.
- **Generated files.** Do not edit a file whose header says it is automatically
  generated.
- **AI gateway.** Keep model calls on Lovable's gateway, and keep
  `LOVABLE_API_KEY` out of browser code.
- **Connectors.** Lovable provides native connectors. `list_connectors` shows
  which are enabled; `add_connector` only returns the dashboard link. When a
  connector is enabled, calls go through the connector gateway and need
  `LOVABLE_API_KEY`. When Lovable does not provide one, users can bring their
  own key and store it in Secrets.
- **Secrets.** Lovable manages them. Do not put secret values in the repo.
<!-- LOVABLE:END -->

## Application architecture
- Keep assessment state in React memory during this fictional-only workflow; avoid persisting personal data without an explicit authenticated storage requirement.
- Keep assessment schemas, report assembly and safety instructions in the shared assessment module so forms, AI validation and exports use one contract.
- Keep the authenticated AI endpoint protected; enable the separate public endpoint only through the shared demo switch, with identical validated server-only Gateway inference and no substituted results.
- Enforce demo quotas through an atomic service-only database reservation before inference; hash trusted ingress network metadata with HMAC, store no assessment notes, and fail closed when counters are unavailable.
- Keep the demonstration route public and use a single root authentication provider with inline social sign-in; this preserves in-memory assessment navigation without adding profile storage.
- Export edited reports client-side through jsPDF, keeping notes, own words and interpretations in separate sections.
- Replace assessments through one in-memory replacement action that clears report, analysis, review and pending method state; this prevents previous assessment content surviving a reset or example load.
