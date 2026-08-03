# Security Policy

## Supported versions

Only the latest release of `frameforge-mcp` and the bundled Figma plugin receives security fixes. If you're on an older version, update before reporting; the issue may already be fixed.

## Reporting a vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

Use [GitHub private vulnerability reporting](https://github.com/imtiyaazsalie/frameforge/security/advisories/new) instead: go to the [Security tab](https://github.com/imtiyaazsalie/frameforge/security) and click **Report a vulnerability**. The report stays private between you and the maintainer until a fix is released.

Include reproduction steps, the affected tool or component, and your Frameforge version (the `frameforge-mcp` version from your MCP client config, plus the plugin build if relevant).

What to expect:

- **Acknowledgement within 3 days.** Frameforge is maintained by one person, so allow a little slack across time zones and weekends.
- An assessment of impact and affected versions, and a fix timeline proportional to severity.
- **Coordinated disclosure.** Keep the report private until a fix is released. We'll agree on a publication date with you and aim to publish an advisory within 90 days of triage, sooner for severe issues.
- Credit in the published advisory and release notes, unless you'd rather stay anonymous.

## Architecture and trust boundaries

Frameforge runs entirely on your machine; there is no Frameforge cloud service.

- **Where it runs.** Your MCP client launches the `frameforge-mcp` server locally and talks to it over stdio. The server relays to the Figma plugin over a WebSocket bound to `127.0.0.1` (port 3055), so it isn't reachable from your network.
- **Who can talk to it.** Binding to loopback is not by itself a boundary: a web page you visit can open a WebSocket to a local port or send it a form-style POST without any same-origin check, and DNS rebinding can make a page's own domain resolve to `127.0.0.1`. Frameforge gates every request, WebSocket upgrades included, on the two headers a page cannot forge:
  - **`Host`** must name loopback (`localhost`, `127.0.0.1`, `[::1]`). A rebound request still carries the attacker's domain here, which is what makes this the check that stops rebinding, including on `GET`, where the browser considers itself same-origin, sends no `Origin`, and would otherwise be able to read the reply.
  - **`Origin`** must be absent (a follower process or the plugin host, neither of which is a browser) or the plugin's sandboxed origin. The leader's HTTP endpoints (`/rpc`, `/ping`, `/abdicate`) are stricter still: they refuse any request carrying an `Origin` and require a media type outside the set a page can send without a CORS preflight.

  If some environment's plugin host is ever refused, `FRAMEFORGE_ALLOW_ANY_ORIGIN=1` lifts the origin gate; report it rather than leaving it set. It does not lift the host gate. What none of this defends against is another program already running as you on the same machine; see the note on a compromised machine below.

- **What it can access.** The plugin runs in Figma's plugin sandbox and uses the official public Plugin API, the same API every Community plugin uses. It can only touch the Figma file you have open; it cannot reach your other files, your account, or your org's data, because the Plugin API doesn't expose them.
- **What leaves your machine.** Nothing. Frameforge sends no telemetry. Design data flows only between the plugin, the local relay, and your MCP client.
- **File writes.** Export tools (screenshots, PDF, video, image fills) write only to the paths your agent explicitly passes in the tool call; the server never writes anywhere it wasn't asked to.

## Scope

**In scope:** anything that lets an attacker cross the boundaries above, including when the trigger is a malicious Figma document or prompt-injected tool input. If Frameforge's handling of untrusted input lets an attacker escalate beyond what this document describes, we want to know.

**Out of scope; report these where they belong:**

- **Vulnerabilities in dependencies.** Report them to the upstream maintainers (or via the [npm contact form](https://www.npmjs.com/support)); open a regular issue here if Frameforge needs to bump a patched release.
- **Bugs in Figma itself** (the desktop app, the Plugin API sandbox): report to [Figma](https://www.figma.com/security/).
- **Bugs in your MCP client** (Claude Code, Cursor, etc.): report to that project.
- **Prompt injection against the AI agent itself.** An agent following bad instructions embedded in a design file is a limitation of LLM-based tooling, not a Frameforge vulnerability, unless Frameforge's handling of that input breaks the boundaries above, which _is_ in scope.
- **An already-compromised machine.** Malware running with your user privileges can do everything Frameforge can and more; that isn't a boundary Frameforge can defend.

Thanks for helping keep Frameforge and its users safe.
