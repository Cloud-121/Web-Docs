# MeshCore Region Codes

## What is region coding?

The goal of region coding isn’t to stop you from talking to people farther away. It’s to keep conversations from being repeated in places where they don’t need to go.
Every time a repeater retransmits a message, that transmission uses airtime. Keeping unnecessary rebroadcasts out of an area means less traffic competing with the people using that part of the network. That’s the practical benefit we’re aiming for.

*MeshCore calls this a region scope.*

When you send a scoped message, a small code travels with the packet. A compatible repeater checks that code against the regions it’s configured to allow. If the scope is allowed, the repeater can forward the message. Otherwise, it doesn’t pass that flood message onward.

## Find your repeater's region codes

Choose where the **repeater is installed**. This tool supports all approved regions in the source map. It allows matching coordinated and political regions, including larger regional scopes and any matching MeshMapper codes supplied by the source. It also includes the community's known MeshMapper codes for Pensacola, Lafayette, Gulf Coast Louisiana, and Gulfport–Biloxi. It does not block or remove any existing regions.

<div id="region-picker">
  <p data-status role="status" aria-live="polite">Loading region data…</p>
  <div data-map role="region" aria-label="Repeater region map"></div>
  <p data-map-note></p>
  <form>
    <fieldset disabled>
      <legend>Or enter the repeater's coordinates</legend>
      <label>Latitude<input name="latitude" type="number" min="-90" max="90" step="any" placeholder="29.9511" required></label>
      <label>Longitude<input name="longitude" type="number" min="-180" max="180" step="any" placeholder="-90.0715" required></label>
      <button type="submit">Find region codes</button>
    </fieldset>
  </form>
  <p data-timestamp></p>
  <p>Boundaries and region identities: <a href="https://regions.caboosey.net">Caboosey region map</a> · <a href="https://regions.caboosey.net/regions/index.json">Source index</a></p>
  <div data-result></div>
  <p data-copy-status role="status" aria-live="polite"></p>
  <noscript>Enable JavaScript to use the map and command generator. See the manual instructions below.</noscript>
</div>

Use MeshCore repeater firmware that supports `region def`. Open your repeater's **Command Line** as admin, run the generated `region def` command, and review the returned region tree. Then run `region save` to persist the changes. Usually this is just two commands; longer lists are split into batches to stay within the CLI's 160-character limit. The `|*` separators keep regions at the global root rather than nesting them. If any command fails, stop before saving: earlier entries may already have been applied. The generated sequence has not yet been verified on a physical repeater.

Existing entries for the listed codes are updated under the global root. Unscoped (`*`) permissions, home/default scope, radio settings, and unrelated region entries are left unchanged. A region's name does not automatically include other region codes; each matching code is explicitly allowed. The map describes coordination boundaries, not radio coverage.

If the tool is unavailable, consult the [source region map](https://regions.caboosey.net) and your local coordinator. The additional community MeshMapper mappings are: PNS → `gc-fl-pns-mm`, LFT → `gc-la-lft-mm`, MSY → `gc-la-msy-mm`, GPT → `us-ms-gpt-mm`. Elsewhere, the tool uses the API's matching codes without inventing a MeshMapper code.

For older firmware that supports region management but does not recognize `region def`, run `region put CODE *` followed by `region allowf CODE` for every code in the tool's **Allow** list. Run `region save` after all commands succeed. Check each entry with `region get CODE`: allowed entries should show `F`.

See the [official MeshCore region command reference](https://docs.meshcore.io/cli_commands/#region-management-v110) for details.
