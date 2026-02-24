# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. For example, `~~CRM` might mean HubSpot, Salesforce, or any other CRM with an MCP server.

Plugins are **tool-agnostic** — they describe workflows in terms of categories (SEO, email marketing, CRM, etc.) rather than specific products. The `.mcp.json` pre-configures specific MCP servers, but any MCP server in that category works.

## Connectors for this plugin

| Category | Placeholder | Included servers | Other options |
|----------|-------------|-----------------|---------------|
| Chat | `~~chat` | Slack | Microsoft Teams |
| Design | `~~design` | Canva, Figma | Adobe Creative Cloud |
| CRM | `~~CRM` | HubSpot | Salesforce, Pipedrive, Zoho |
| Product analytics | `~~product analytics` | Amplitude | Mixpanel, Google Analytics |
| Knowledge base | `~~knowledge base` | Notion | Confluence, Guru |
| SEO | `~~SEO` | Ahrefs, Similarweb | Semrush, Moz |
| Email marketing | `~~email marketing` | Klaviyo | Mailchimp, Brevo, Customer.io, SendGrid |
| Calendar | `~~calendar` | Google Calendar | Outlook Calendar |
| Email | `~~email` | Gmail | Outlook |
| Payments | `~~payments` | Stripe | — |
| Project management | `~~project management` | Asana | Linear, Jira, Monday.com |
| CMS | `~~CMS` | Webflow | WordPress, HubSpot CMS |

## Categories without HTTP connectors (Claude Code only)

The following categories require local npx/stdio MCP servers. They work in Claude Code but not in Cowork. See `.mcp.json.example` for configuration.

| Category | Available via npx | When HTTP becomes available |
|----------|------------------|---------------------------|
| Advertising | Google Ads, Meta Ads, LinkedIn Ads, TikTok Ads | Connect via Connectors panel when available |
| Analytics | Google Analytics, Google Search Console | Connect via Connectors panel when available |
| Social media | Buffer, Twitter/X, LinkedIn | Connect via Connectors panel when available |
| SMS/Messaging | Twilio | Connect via Connectors panel when available |
| Translation | DeepL, Sarvam AI | Connect via Connectors panel when available |
| Database | Supabase, PostgreSQL | Connect via Connectors panel when available |

## Advanced configuration (Claude Code)

For Claude Code CLI users who want the full 67-server configuration with npx/stdio transports, rename the example file:

```bash
cp .mcp.json.example .mcp.json
```

This replaces the HTTP-only configuration with the full set of local MCP servers. Requires Node.js, npx, and the appropriate API keys configured as environment variables.
