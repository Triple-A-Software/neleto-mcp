# Neleto MCP tools

57 tools in 9 groups, as exposed by the server on a current Neleto instance. Full parameter reference: https://neleto.io/docs/developer/mcp/tools

IDs: pages, layouts, components, posts and events use integers. Files use UUID strings.

## Pages (6)

| Tool | What it does |
|---|---|
| `page_list` | List pages |
| `page_get` | Load a page with its layout, elements and translated content |
| `page_create` | Create a page with title, route, meta tags, template and elements |
| `page_update` | Update a page. Replaces the whole record, so load it with `page_get` first |
| `page_duplicate` | Copy a page to a new route and title |
| `page_delete` | Soft-delete a page |

## Layouts (5)

| Tool | What it does |
|---|---|
| `layout_list` | List layouts that can be assigned to pages |
| `layout_get` | Load a layout with its element tree |
| `layout_create` | Create a layout shell with shared elements such as nav and footer |
| `layout_update` | Update a layout. Replaces the whole record |
| `layout_delete` | Soft-delete a layout |

## Components (7)

| Tool | What it does |
|---|---|
| `component_list` | List components as a short summary |
| `component_search` | Find components by their form label |
| `component_get` | Load a full component definition |
| `component_used_by_elements` | List the elements that use a component |
| `component_create` | Create a component: template, CSS, JS and the editor form |
| `component_update` | Update a component. Replaces the whole record |
| `component_delete` | Delete a component and its element instances |

## Template checks (3)

| Tool | What it does |
|---|---|
| `lsp_check_page` | Check a page template for errors and warnings |
| `lsp_check_layout` | Check a layout template |
| `lsp_check_component` | Check a component template and its form |

Run these before publishing template changes. They use the same language server as the admin editor.

## Blog posts (6)

| Tool | What it does |
|---|---|
| `post_list` | List posts |
| `post_search` | Search posts by title, description or content |
| `post_get` | Load a post |
| `post_create` | Create a post (rich text, HTML allowed) |
| `post_update` | Update a post |
| `post_delete` | Delete a post |

## Events (8)

| Tool | What it does |
|---|---|
| `event_list` | List events |
| `event_today` | Events happening today |
| `event_upcoming` | Upcoming events |
| `event_search` | Search events by title, description or content |
| `event_get` | Load an event |
| `event_create` | Create an event with start and end date |
| `event_update` | Update an event |
| `event_delete` | Delete an event |

## Files (15)

| Tool | What it does |
|---|---|
| `file_list` | List files and folders |
| `file_search` | Search files by title, description, path, status or MIME type |
| `file_get` | Load a file record, including its `serveUrl` |
| `file_create` | Create a folder, an empty file or a remote file entry |
| `file_update` | Update file metadata or the content of a text file |
| `file_move` | Move or copy files into another folder |
| `file_rename` | Rename a file or folder |
| `file_delete` | Delete files or folders |
| `file_upload` | Upload from a URL (`sourceUrl`, preferred) or inline base64 |
| `file_upload_multipart` | Upload in one call, split into checksummed parts |
| `file_upload_url` | Get a one-time URL for an out-of-band HTTPS PUT |
| `file_upload_begin` | Start a chunked upload |
| `file_upload_chunk` | Send one chunk |
| `file_upload_commit` | Finish a chunked upload and verify the SHA-256 |
| `file_upload_abort` | Cancel a chunked upload |

Images can also be ingested inline: in page and layout element data, put `{ "sourceUrl": "https://…" }` where a file ID is expected. The server fetches and stores the file during the same save.

## Web files (5)

Static files served at the site root, such as `robots.txt` or `llms.txt`.

| Tool | What it does |
|---|---|
| `web_file_list` | List web files |
| `web_file_get` | Load a web file by path |
| `web_file_create` | Create a web file at `/<path>` |
| `web_file_update` | Update a web file |
| `web_file_delete` | Delete a web file |

## Settings (2)

| Tool | What it does |
|---|---|
| `settings_get` | Load site settings, including the live `publicBaseUrl` and `adminUrl` |
| `settings_update` | Change settings such as languages, default statuses, caching and meta tags. Only the fields you send are changed |
