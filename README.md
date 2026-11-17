# Vizbl MCP connector

Connect Claude and other AI assistants to [Vizbl](https://vizbl.com) and run product visualization for your store from the chat: publish 3D models with AR links and QR codes, set up rugs, flooring and wall art, configure AI try-on, and get install code for Shopify, WooCommerce, BigCommerce, Wix or a custom site.

Vizbl runs a **remote** [Model Context Protocol](https://modelcontextprotocol.io) server. There is nothing to install.

| | |
| --- | --- |
| Server URL | `https://mcp.vizbl.com/mcp` |
| Transport | Streamable HTTP |
| Authorization | OAuth 2.0 with dynamic client registration |
| Account | Not needed for guides, cost estimates, 3D conversion, file hosting, AR links, QR codes, widget code and install steps. A Vizbl secret key unlocks your own library, catalog, analytics and billing. |

Full documentation: [developer.vizbl.com/docs/mcp](https://developer.vizbl.com/docs/mcp)

## Connect

**Claude (web, desktop, mobile).** Open **Settings → Connectors**, choose **Add custom connector** and paste:

```text
https://mcp.vizbl.com/mcp
```

**Claude Code.**

```bash
claude mcp add --transport http vizbl https://mcp.vizbl.com/mcp
```

**Other MCP clients.** Add a remote server with the URL above and the Streamable HTTP transport. Client registration is dynamic, so there is nothing to register with Vizbl first.

Your client opens the Vizbl consent screen. The **API key** field is optional: leave it empty to try the tools that work without an account, or paste a secret key from your Vizbl cabinet (**Settings → API keys**) to work with your own workspace. The scopes of the key decide which tools the assistant sees.

## What you can ask

| Prompt | What happens |
| --- | --- |
| *Import this chair.glb into Vizbl, name it "Oak dining chair" and give me the AR link when it is ready.* | Uploads the model, waits for processing, returns the AR link |
| *Convert this STEP file to GLB.* | Converts the file on Vizbl servers |
| *How do I add the AR button to our WooCommerce product pages?* | Returns install steps and embed code |
| *List my rugs and add a 200×300 cm size to the "Berber" one.* | Reads the rug catalog and adds the size |
| *Set up try-on for eyewear and turn it on for these three Shopify products.* | Configures the AI Try-On widget |
| *How many tokens did we spend last month?* | Reads token usage by action |

## Tools

Read and write operations are separate tools. Tools that delete, revoke or overwrite something ask for confirmation first.

**No account needed:** `get_guide`, `estimate_costs`, `convert_3d_model`, `get_job_status`, `create_public_upload_url`, `get_ar_link`, `get_qr`, `get_widget_snippet`, `generate_wallart_buttons`, `get_install_instructions`, `list_tryon_types`

**With a secret key:**

| Area | Tools |
| --- | --- |
| Library and models | `list_models`, `get_model`, `create_upload_url`, `upload_model`, `update_model`, `publish_model`, `set_model_activation`, `get_model_links`, `delete_model` |
| Rugs, flooring and rooms | `list_rugs`, `list_floorings`, `create_rug_from_photo`, `add_rug_size`, `update_rug`, `list_rooms`, `add_room`, `remove_room`, `create_image_upload_url` |
| AI Try-On | `get_tryon_widget`, `set_shopify_tryon` |
| Account and billing | `get_account`, `get_pricing`, `get_usage`, `create_checkout_link`, `list_invoices` |
| Analytics, keys, domains and team | `get_analytics`, `list_api_keys`, `create_public_key`, `revoke_key`, `get_domains`, `set_domains`, `list_members`, `invite_member`, `revoke_invite` |
| Shopify | `list_shopify_products`, `link_model_to_product`, `unlink_model`, `list_shopify_posters`, `set_poster_active`, `submit_request` |

`create_checkout_link` only returns a payment page. Payments are completed by you, never by the tool.

The current list, access levels and changes are kept in the [tools reference](https://developer.vizbl.com/docs/mcp/tools) and the [changelog](https://developer.vizbl.com/docs/mcp/changelog).

## Pricing

Vizbl is billed in tokens. New accounts get 1,000 free tokens, no card required. See [vizbl.com/pricing](https://vizbl.com/pricing).

## Privacy and limits

See [Limits & privacy](https://developer.vizbl.com/docs/mcp/limits-and-privacy).

## Other Vizbl developer tools

- iOS SDK: [vizbl-ios-sdk](https://github.com/VIZBL/vizbl-ios-sdk)
- Android SDK: [vizbl-android-sdk](https://github.com/VIZBL/vizbl-android-sdk)
- Web components (Room Viewer, Model Viewer, AI Try-On): [developer.vizbl.com](https://developer.vizbl.com)

## Support

- Questions and discussion: [Vizbl Discord](https://discord.gg/vz3T4vBr89)
- Support requests: [support.vizbl.com](https://support.vizbl.com/support/form/createTicket/MQ%253D%253D)
- Email: [info@vizbl.com](mailto:info@vizbl.com)

This repository holds the connector's description and registry metadata. The server itself is operated by Vizbl Systems, Inc.
