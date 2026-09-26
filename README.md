# ERP MCP Server

**Connect 16 ERPs to Claude, ChatGPT and Copilot through one MCP server.** Powered by [AnythingMCP](https://github.com/HelpCode-ai/anythingmcp).

ERP MCP Server connects 16 ERP systems to Claude, ChatGPT, Copilot and Cursor through one MCP endpoint: 138 tools in total. Pick the systems you run, add their credentials, and each becomes a set of MCP tools. It runs on AnythingMCP Cloud or self-hosted with Docker, with encrypted credentials and an audit log.

**Last verified:** 2026-09-26 against the systems marked verified in the table (each one's own verification is linked from its row).  
**Adapter synced:** <!-- synced -->2026-09-26

Maintained by [helpcode.ai](https://helpcode.ai), the team that builds and maintains [AnythingMCP](https://github.com/HelpCode-ai/anythingmcp).

## Systems

| System | Region | Tools | Auth | Verified live | Cloud | Dedicated repo |
|---|---|---|---|---|---|---|
| SAP Business One | DE | 12 | Login session | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=sap-business-one) | [sap-business-one-mcp-server](https://github.com/HelpCode-ai/sap-business-one-mcp-server) |
| SAP S/4HANA Cloud | Global | 15 | OAuth 2.0 | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=sap-s4hana-cloud) | – |
| Odoo | Global | 11 | API token | yes, 2026-09-26 | [install](https://cloud.anythingmcp.com/connectors/store?install=odoo) | [odoo-mcp-server](https://github.com/keysersoft/odoo-mcp-server) |
| Microsoft Dynamics NAV | DE | 6 | User + password | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=dynamics-nav) | – |
| ERPNext | Global | 11 | API key | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=erpnext) | – |
| Dolibarr | FR | 10 | API key | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=dolibarr) | – |
| JTL-Wawi † | DE | 9 | API token | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=jtl-wawi) | – |
| Xentral ERP | DE | 7 | User + password | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=xentral) | [xentral-mcp-server](https://github.com/kochfreiburg/xentral-mcp-server) |
| weclapp Cloud ERP | DE | 11 | API key | yes, 2026-09-26 | [install](https://cloud.anythingmcp.com/connectors/store?install=weclapp) | [weclapp-mcp-server](https://github.com/kochfreiburg/weclapp-mcp-server) |
| Sage 100 (DE) † | DE | 6 | User + password | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=sage-100) | – |
| Haufe X360 † | DE | 7 | Login session | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=haufe-x360) | – |
| ScopeVisio Cloud ERP | DE | 6 | API token | not yet | [install](https://cloud.anythingmcp.com/connectors/store?install=scopevisio) | – |
| AFAS Profit † | NL | 6 | API key | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=afas-profit) | – |
| Zucchetti † | IT | 6 | User + password | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=zucchetti) | – |
| TeamSystem † | IT | 6 | OAuth 2.0 | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=teamsystem) | – |
| Axonaut † | FR | 9 | API key | no † | [install](https://cloud.anythingmcp.com/connectors/store?install=axonaut) | – |

"Verified live" means someone ran the connector against a real system; its own repository says how and when. "Not yet" means it follows the vendor's API documentation and has not been confirmed there; reports are welcome.

† Built from the vendor's published API documentation and not yet exercised against a live system. Reports and fixes are welcome.

## Your ERP isn't listed?

Connect it through what it already exposes: its REST/OData API ([openapi-to-mcp](https://github.com/HelpCode-ai/openapi-to-mcp)), its SOAP services ([soap-to-mcp](https://github.com/HelpCode-ai/soap-to-mcp)) or its SQL database, read-only ([sql-to-mcp](https://github.com/HelpCode-ai/sql-to-mcp)). That covers custom and on-premises builds that no catalog adapter will ever know.

## Self-hosted (Docker)

```bash
git clone https://github.com/HelpCode-ai/erp-mcp-server.git && cd erp-mcp-server
./scripts/install.sh   # installs every system whose credentials are set in .env
```

## Connect Claude, ChatGPT, Copilot or Cursor

- **Claude (claude.ai, Desktop, mobile):** *Customize → Connectors → Add custom connector*, paste your MCP server URL and sign in. Claude connects from Anthropic's cloud, so the URL must be public HTTPS: your AnythingMCP Cloud URL, or your own instance behind TLS.
- **Claude Code:**

  ```bash
  claude mcp add --transport http erp-mcp-server http://localhost:4000/mcp --header "X-API-Key: <MCP_API_KEY>"
  ```
- **Cursor** (`.cursor/mcp.json`) and **VS Code / GitHub Copilot** (`.vscode/mcp.json`, key `servers` instead of `mcpServers`, plus `"type": "http"`):

  ```json
  { "mcpServers": { "erp-mcp-server": { "url": "http://localhost:4000/mcp", "headers": { "X-API-Key": "<MCP_API_KEY>" } } } }
  ```
- **ChatGPT:** add the public HTTPS URL as a connector (app) in ChatGPT's settings. A `localhost` URL does not work there.

## Tools

<!-- tools:start (generated from adapter/*.json, do not edit) -->
#### SAP Business One (12)

| Tool | What it does | Access |
|---|---|---|
| `b1_list_business_partners` | List business partners (customers, suppliers, leads). | read |
| `b1_get_business_partner` | Get one business partner by CardCode. | read |
| `b1_list_items` | List inventory items (articles). | read |
| `b1_get_item` | Get one item by ItemCode. | read |
| `b1_list_orders` | List sales orders. | read |
| `b1_get_order` | Get one sales order by DocEntry (integer primary key). | read |
| `b1_create_order` | Create a new sales order. | write |
| `b1_list_invoices` | List A/R invoices. | read |
| `b1_get_invoice` | Get one A/R invoice by DocEntry. | read |
| `b1_list_quotations` | List sales quotations. | read |
| `b1_list_delivery_notes` | List delivery notes (outgoing goods movements). | read |
| `b1_get_company_info` | Sanity check: returns company metadata (admin info). | read |

#### SAP S/4HANA Cloud (15)

| Tool | What it does | Access |
|---|---|---|
| `s4_list_business_partners` | List business partners (combined customers + suppliers) from API_BUSINESS_PARTNER. | read |
| `s4_get_business_partner` | Get one business partner by its 10-character ID. | read |
| `s4_list_customers` | List customer master records (subset of business partners). | read |
| `s4_list_suppliers` | List supplier master records (subset of business partners). | read |
| `s4_list_sales_orders` | List sales orders (headers). | read |
| `s4_get_sales_order` | Get one sales order by its 10-char number. | read |
| `s4_list_sales_order_items` | List the items (line entries) of a given sales order. | read |
| `s4_list_purchase_orders` | List purchase orders (headers). | read |
| `s4_get_purchase_order` | Get one purchase order by its 10-char number. | read |
| `s4_list_billing_documents` | List billing documents (customer invoices, credit memos). | read |
| `s4_list_outbound_deliveries` | List outbound delivery headers (goods leaving the warehouse). | read |
| `s4_list_journal_entries` | List journal entry items (general ledger postings). | read |
| `s4_list_products` | List materials / products (item master). | read |
| `s4_get_product` | Get one product/material by its ID. | read |
| `s4_list_purchase_requisitions` | List purchase requisition items (pre-PO demand requests). | read |

#### Odoo (11)

| Tool | What it does | Access |
|---|---|---|
| `odoo_search_read` | Search and read any Odoo model in one call. | read |
| `odoo_read` | Read specific records of a model by their ids — the follow-up call when a search has returned ids and you now want the detail of a few of them. | read |
| `odoo_search_count` | Count the records of a model matching a domain, without transferring them. | read |
| `odoo_fields_get` | Describe a model's fields: name, type, label, whether it is required or readonly, and the related model for relational fields. | read |
| `odoo_list_partners` | List partners — Odoo's customers, suppliers and contacts — with name, e-mail, phone, city and country. | read |
| `odoo_list_sale_orders` | List sales orders with their customer, date, state and total. | read |
| `odoo_list_invoices` | List customer invoices and vendor bills with their partner, date, due date, state and residual amount — the answer to 'what is still unpaid'. | read |
| `odoo_list_products` | List products with their internal reference, sale price, cost, product type and unit of measure. | read |
| `odoo_create` | Create a record in any Odoo model. | write |
| `odoo_write` | Update existing records in any Odoo model. | write |
| `odoo_call_method` | Call an arbitrary public method on an Odoo model — the escape hatch for workflow actions such as action_confirm on a sale order or action_post on an invoice. | write |

#### Microsoft Dynamics NAV (6)

| Tool | What it does | Access |
|---|---|---|
| `dynamics_nav_list_services` | List the published web services available on this company — the entity set names every other tool needs. | read |
| `dynamics_nav_query` | Query any published entity set with OData v4. | read |
| `dynamics_nav_get_by_key` | Read one record by its OData key. | read |
| `dynamics_nav_get_metadata` | Read the OData $metadata document: every published entity type, its properties and their data types. | read |
| `dynamics_nav_create_record` | Create a record in a published entity set. | write |
| `dynamics_nav_update_record` | Update one record by key. | write |

#### ERPNext (11)

| Tool | What it does | Access |
|---|---|---|
| `erpnext_get_logged_user` | Read which user the API key belongs to. | read |
| `erpnext_list_documents` | List documents of any DocType with Frappe filters. | read |
| `erpnext_get_document` | Read one document of any DocType in full by its name (ERPNext's primary key), including its child tables. | read |
| `erpnext_count_documents` | Count the documents of a DocType matching a filter, without transferring them. | read |
| `erpnext_get_doctype_meta` | Describe a DocType: every field with its type, label, options and whether it is required. | read |
| `erpnext_list_customers` | List customers with their name, group, territory, currency and default payment terms. | read |
| `erpnext_list_sales_orders` | List sales orders with their customer, date, delivery date, status and grand total. | read |
| `erpnext_list_sales_invoices` | List sales invoices with their customer, posting date, due date, status and outstanding amount — the answer to 'what is still unpaid'. | read |
| `erpnext_list_items` | List items from the catalogue with their code, name, group, stock UOM and default rate. | read |
| `erpnext_list_stock_balance` | Read per-warehouse stock: actual, reserved and projected quantity per item. | read |
| `erpnext_create_document` | Create a document of any DocType. | write |

#### Dolibarr (10)

| Tool | What it does | Access |
|---|---|---|
| `dolibarr_get_status` | Read the Dolibarr version and API status of this installation. | read |
| `dolibarr_list_thirdparties` | List third parties — Dolibarr's customers, suppliers and prospects — with their name, VAT number, address and customer/supplier flags. | read |
| `dolibarr_get_thirdparty` | Read one third party in full: addresses, tax identifiers, payment terms, assigned sales representative and account balances. | read |
| `dolibarr_list_invoices` | List customer invoices with their reference, date, third party, totals and status. | read |
| `dolibarr_get_invoice` | Read one customer invoice in full: every line with quantity, unit price, discount and VAT, the totals, and the payments applied against it. | read |
| `dolibarr_list_orders` | List customer orders with their reference, date, third party, total and status, for the pipeline between proposal and invoice. | read |
| `dolibarr_list_proposals` | List commercial proposals (devis) with their reference, date, third party, total and whether they have been signed. | read |
| `dolibarr_list_supplier_invoices` | List supplier invoices with their reference, date, supplier, total and payment status — the payables side of the ledger. | read |
| `dolibarr_list_products` | List products and services with their reference, label, sale and cost price, VAT rate and stock quantity. | read |
| `dolibarr_get_product_stock` | Read the per-warehouse stock of one product — the answer an availability question actually needs, rather than the cached total on the product record. | read |

#### JTL-Wawi (9)

| Tool | What it does | Access |
|---|---|---|
| `jtl_wawi_list_warehouses` | List the warehouses (Lager) configured in JTL-Wawi with their id, name and type. | read |
| `jtl_wawi_list_items` | List articles from the item master with their SKU, name, prices, EAN and manufacturer. | read |
| `jtl_wawi_get_item` | Read one article in full: its SKU, descriptions, dimensions, prices, categories and supplier links. | read |
| `jtl_wawi_get_item_stock` | Read the per-warehouse stock of one article: quantity on hand, reserved, and available. | read |
| `jtl_wawi_list_customers` | List customers with their customer number, company, contact name, address and customer group. | read |
| `jtl_wawi_get_customer` | Read one customer in full: billing and delivery addresses, payment and shipping defaults, and the customer group they belong to. | read |
| `jtl_wawi_list_sales_orders` | List sales orders with their order number, customer, date, payment and shipping status and total. | read |
| `jtl_wawi_get_sales_order` | Read one sales order in full: its line items with SKU, quantity and price, the addresses, and the payment and shipping state. | read |
| `jtl_wawi_list_shipments` | List shipments with their tracking number, carrier, date and the sales order they belong to — the answer to 'has it gone out yet'. | read |

#### Xentral ERP (7)

| Tool | What it does | Access |
|---|---|---|
| `xentral_list_articles` | List articles (products) from Xentral. | read |
| `xentral_get_article` | Retrieve a single article by its Xentral internal id. | read |
| `xentral_list_customers` | List customers (Kunden). | read |
| `xentral_get_customer` | Retrieve a single customer by id, including contact persons, delivery addresses, bank details, and credit limit. | read |
| `xentral_list_sales_orders` | List sales orders (Auftraege). | read |
| `xentral_list_invoices` | List outgoing invoices (Rechnungen). | read |
| `xentral_get_stock` | Retrieve current stock levels across all warehouses for a given article. | read |

#### weclapp Cloud ERP (11)

| Tool | What it does | Access |
|---|---|---|
| `weclapp_list_customers` | List parties (customers/suppliers/contacts) from weclapp ERP. | read |
| `weclapp_get_customer` | Get a specific party (customer/supplier/contact) by ID. | read |
| `weclapp_list_sales_orders` | List sales orders from weclapp ERP. | read |
| `weclapp_list_invoices` | List sales invoices from weclapp ERP. | read |
| `weclapp_list_articles` | List articles (products) from weclapp ERP. | read |
| `weclapp_get_article` | Get a specific article (product) by ID, including stock, pricing, and warehouse data. | read |
| `weclapp_list_quotations` | List sales quotations (Angebote) from weclapp ERP. | read |
| `weclapp_get_quotation` | Get a single sales quotation (Angebot) by ID, including positions, amounts and status. | read |
| `weclapp_list_recurring_invoices` | List recurring invoices (wiederkehrende Rechnungen / Abo-Rechnungen) from weclapp ERP — the templates that periodically generate sales invoices. | read |
| `weclapp_get_recurring_invoice` | Get a single recurring invoice (wiederkehrende Rechnung) by ID, including its interval, next execution date and template positions. | read |
| `weclapp_list_opportunities` | List sales opportunities (Verkaufschancen) from weclapp CRM. | read |

#### Sage 100 (DE) (6)

| Tool | What it does | Access |
|---|---|---|
| `sage_100_get_metadata` | Read the OData $metadata document: every entity set this installation publishes and the fields on each. | read |
| `sage_100_query` | Query any published entity set with OData. | read |
| `sage_100_get_by_key` | Read one record from an entity set by its OData key, with the navigation properties you name expanded. | read |
| `sage_100_list_addresses` | List addresses (Adressen) — Sage 100's customers and suppliers — with their number, matchcode, name and city. | read |
| `sage_100_list_items` | List items (Artikel) from the article master with their number, description, unit and price. | read |
| `sage_100_list_documents` | List sales and purchase documents (Belege) with their type, number, date, address and total. | read |

#### Haufe X360 (7)

| Tool | What it does | Access |
|---|---|---|
| `haufe_x360_list_customers` | List customers with their id, name, status, class and balance. | read |
| `haufe_x360_get_customer` | Read one customer by their customer id, with addresses, contacts, payment terms and credit settings. | read |
| `haufe_x360_list_sales_orders` | List sales orders with their number, type, customer, date, status and total. | read |
| `haufe_x360_list_stock_items` | List stock items with their inventory id, description, item class, base unit and default price. | read |
| `haufe_x360_list_invoices` | List A/R invoices with their reference number, customer, date, due date, status and balance — the answer to 'what is still open'. | read |
| `haufe_x360_list_shipments` | List shipments with their number, customer, status, shipment date and the sales order they fulfil. | read |
| `haufe_x360_list_vendors` | List vendors with their id, name, status, class and balance, for the purchasing side of the ledger. | read |

#### ScopeVisio Cloud ERP (6)

| Tool | What it does | Access |
|---|---|---|
| `scopevisio_list_contacts` | List contacts (customers, suppliers, leads) from ScopeVisio. | read |
| `scopevisio_get_contact` | Get detailed information about a specific contact by ID. | read |
| `scopevisio_list_outgoing_invoices` | List outgoing invoices (Ausgangsrechnungen) from ScopeVisio. | read |
| `scopevisio_list_incoming_invoices` | List incoming invoices (Eingangsrechnungen) from ScopeVisio. | read |
| `scopevisio_list_projects` | List projects from ScopeVisio. | read |
| `scopevisio_list_tasks` | List tasks from ScopeVisio. | read |

#### AFAS Profit (6)

| Tool | What it does | Access |
|---|---|---|
| `afas_profit_list_connectors` | List the GetConnectors and UpdateConnectors published to this app connector. | read |
| `afas_profit_get_connector_metadata` | Read one GetConnector's field definitions: the field ids, their types and lengths. | read |
| `afas_profit_get_data` | Read rows from a GetConnector with AFAS's positional three-list filter. | read |
| `afas_profit_get_debtors` | Read the Profit_Debiteuren GetConnector — customers with their debtor number, name, address and credit data. | read |
| `afas_profit_get_invoices` | Read the Profit_Facturen GetConnector — invoices with their number, date, debtor and amounts. | read |
| `afas_profit_get_employees` | Read the Profit_Medewerkers GetConnector — employees with their number, name, department and employment data. | read |

#### Zucchetti (6)

| Tool | What it does | Access |
|---|---|---|
| `zucchetti_list_services` | Ask the installation which REST services it publishes. | read |
| `zucchetti_list_records` | List records of any published resource with paging and a search fragment. | read |
| `zucchetti_get_record` | Read one record of any published resource by its id, with every field the API user is allowed to see. | read |
| `zucchetti_list_anagrafiche` | List anagrafiche — Zucchetti's customers and suppliers — with their code, name, partita IVA and address. | read |
| `zucchetti_list_documenti` | List documents (documenti) — invoices, orders and delivery notes — with their type, number, date, counterparty and total. | read |
| `zucchetti_list_articoli` | List items (articoli) from the catalogue with their code, description, unit of measure and price. | read |

#### TeamSystem (6)

| Tool | What it does | Access |
|---|---|---|
| `teamsystem_list_customers` | List customers with their name, partita IVA, codice fiscale and address. | read |
| `teamsystem_get_customer` | Read one customer in full: registered and billing addresses, tax data, payment terms and the e-invoice routing code. | read |
| `teamsystem_list_suppliers` | List suppliers with their name, partita IVA and address, for the purchasing side of the ledger. | read |
| `teamsystem_list_invoices` | List invoices in a date range with their number, date, customer, total and e-invoice status in the Sistema di Interscambio. | read |
| `teamsystem_get_invoice` | Read one invoice in full: every line with its VAT rate, the totals, the payment schedule and the e-invoice transmission record. | read |
| `teamsystem_list_items` | List items and services from the catalogue with their code, description, unit, price and VAT rate. | read |

#### Axonaut (9)

| Tool | What it does | Access |
|---|---|---|
| `axonaut_list_companies` | List companies — Axonaut's clients and prospects — with their name, SIRET, address, category and assigned user. | read |
| `axonaut_get_company` | Read one company in full: its addresses, custom fields, the employees attached to it and its accounting identifiers. | read |
| `axonaut_list_employees` | List employees — the *people* attached to client companies, not your own staff — with their name, e-mail, phone and role. | read |
| `axonaut_list_invoices` | List invoices with their number, date, company, pre-tax and total amounts and payment state. | read |
| `axonaut_get_invoice` | Read one invoice in full: every product line with quantity, price and VAT, the totals, and the payments recorded against it. | read |
| `axonaut_list_quotations` | List quotations (devis) with their number, date, company, total and whether they have been accepted. | read |
| `axonaut_list_expenses` | List expenses and supplier invoices with their date, supplier, category, pre-tax amount and VAT — the cost side of the ledger. | read |
| `axonaut_list_products` | List catalogue products with their reference, name, pre-tax price, VAT rate and stock quantity. | read |
| `axonaut_list_projects` | List projects with their name, company, budget, status and dates — the anchor for time and profitability questions. | read |
<!-- tools:end -->

## FAQ

### How do I connect my ERP to Claude or ChatGPT?
Install your ERP's adapter in AnythingMCP, enter its API credentials, and add the MCP server URL to Claude as a custom connector or to ChatGPT as an app. If your ERP is not in the table, connect its REST API, SOAP services or database instead.

### Which ERPs are verified against a real system?
The "Verified live" column says so per system, with the date; each dedicated repository explains how. The others follow the vendor's API documentation and have not been confirmed yet.

### Can the AI change data in my ERP?
Only through tools that write, and only when a role allows them. Most ERP adapters only read; SAP Business One, Odoo, ERPNext and Dynamics NAV have write tools, marked in the tools table.

### Can I connect several ERPs, or an ERP and a shop, at once?
Yes. Every connector on the same MCP server is available in one conversation, so the AI can compare an order in the ERP with its shipment or its marketplace order.

### Does my ERP data leave my network?
Self-hosted, the credentials and the audit log stay on your server; only the fields a tool returns go to the AI model you use, and response mapping removes fields before they do.

## Related

- [sap-mcp-server](https://github.com/HelpCode-ai/sap-mcp-server): SAP MCP server: connect SAP Business One, S/4HANA Cloud and Concur to Claude & ChatGPT. Orders, partners, invoices as AI tools.
- [ecommerce-mcp-server](https://github.com/HelpCode-ai/ecommerce-mcp-server): E-commerce MCP server: connect Amazon, eBay, WooCommerce, Shopware, Kaufland, OTTO and 7 more to Claude & ChatGPT.
- [soap-to-mcp](https://github.com/HelpCode-ai/soap-to-mcp): Turn any SOAP/WSDL web service into MCP tools for Claude & ChatGPT. Legacy SOAP APIs as AI tools, no code, self-hosted.
- [sql-to-mcp](https://github.com/HelpCode-ai/sql-to-mcp): SQL to MCP: connect PostgreSQL, MySQL, SQL Server, Oracle or MongoDB to Claude & ChatGPT. Read-only, audited, no code.
- [openapi-to-mcp](https://github.com/HelpCode-ai/openapi-to-mcp): OpenAPI to MCP: turn any OpenAPI/Swagger or REST API into an MCP server for Claude & ChatGPT. Every endpoint a tool, no code.
- [AnythingMCP](https://github.com/HelpCode-ai/anythingmcp): the open-source MCP server and gateway this repository is built on.

## License

AGPL-3.0-only. The adapter definition in `adapter/` comes from AnythingMCP (AGPL-3.0).
