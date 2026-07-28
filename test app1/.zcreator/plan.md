Add a new executive-dark Admin Dashboard built primarily with HTML snippets. It will summarize the existing order, fulfillment, inventory, payment, and customer data without changing the underlying forms.

## User Profiles

No new user profile names are needed. The dashboard will use the app’s existing internal profiles and exclude portal-facing users.

No files to write. Use existing internal profiles for intended dashboard access: Administrator, Developer, Read, Write, Sales Operations Manager, Customer Service Representative, and Inventory Control Specialist. Exclude Customer portal profile and Logistics Partner (Carrier) portal profile from the new Admin Dashboard access. Do not add roles.

**Implementation notes:** Do not create or edit profile files in this segment; permissions are handled after the page exists.

## Admin_Dashboard

Create a polished executive-dark dashboard page with modern cards, operational highlights, charts-style visual blocks, quick actions, and recent activity sections. The page should focus on management visibility across sales orders, fulfillment, payments, inventory, and customers.

Create a new page with linkname Admin_Dashboard and displayname "Admin Dashboard". The page must be built primarily using .dshtml snippets referenced through <dsp> blocks in the main page. Use an executive dark visual style: dark gradient background, glassmorphism cards, high-contrast typography, blue/purple/teal accent colors, rounded cards, status pills, and responsive CSS grids. Required snippet files under Pages/Admin_Dashboard/:
1. Admin_Hero.dshtml: header section with title "Admin Command Center", subtitle for order and fulfillment operations, current high-level KPIs calculated with Deluge from existing forms: total orders, total customers, total items, total inventory records. Include quick action chips linking conceptually to key actions where possible using Creator anchors or clearly labeled action tiles; no JavaScript.
2. KPI_Cards.dshtml: 6 KPI cards with Deluge-backed values: total order value from orders.total_amount, payment records count, completed payments count, pending payments count, low-stock inventory count where available_stock <= reorder_point, scheduled fulfillment count. Show trend-style labels as static/helper text when true historical trend data is not available.
3. Operations_Grid.dshtml: two-column dashboard body containing visual progress/status blocks. Include order status distribution from orders.status, fulfillment status distribution from fulfillment_schedules.status, payment method distribution from payment_records.payment_method, and inventory risk list showing up to 8 inventory records with product display, available_stock, reorder_point, and risk badge.
4. Activity_Table.dshtml: attractive dark table/cards for recent operational records: latest orders by order_date/order_id/customer/status/total_amount and latest payments by payment_date/order/status/amount/status. Use safe null checks and limit record display to a small number.
5. Quick_Links.dshtml: admin shortcut panel with prominent cards for Add Order, Add Inventory, Add Fulfillment Schedule, Orders Report, Inventory Report, Payment Records Report, and Customers Report. Use Creator-compatible links/actions if syntax is known; otherwise render readable non-JS anchor tiles with link names.
Main page Pages/Admin_Dashboard.ds: XML-style page tag <page linkname = "Admin_Dashboard" displayname = "Admin Dashboard"/> with <content><zml><layout> rows/columns and <dsp> components referencing each .dshtml file through CDATA htmlpage wrappers. Use full-width hero, KPI row, operations grid, activity table, quick links. No page parameters needed. Do not change existing DashBoard page.

**Implementation notes:** Use HTML snippets as the primary rendering method. Use inline Deluge inside snippets to compute counts and sums from existing forms. Avoid JavaScript. Create component/snippet files before the main page file.

## Permissions

Grant internal profiles access to the new Admin Dashboard while keeping portal-facing profiles out. This keeps the dashboard aligned with the requested internal-user audience.

Update profile permissions as needed so Admin_Dashboard is accessible to internal profiles: Administrator, Developer, Read, Write, Sales Operations Manager, Customer Service Representative, and Inventory Control Specialist. Do not grant Admin_Dashboard access to Customer or Logistics Partner (Carrier). Preserve all existing form, field, and report permissions. If predefined profile files do not support or need explicit page permissions, leave them unchanged and apply page permissions only to custom internal profiles that already use ModulePermissions/PagePermissions syntax.

**Implementation notes:** Read existing profile files before editing; add page permissions only if the app’s profile syntax requires explicit page access entries.

## UI Configuration

Add the new Admin Dashboard to the web navigation so internal users can open it easily. The existing Dashboard menu entry remains unchanged.

Edit UI/web/menu.ds to add page Admin_Dashboard to the Dashboard navigation area, near the existing DashBoard page. Use display context "Admin Dashboard" via the page displayname and an admin/dashboard icon such as ui-1-dashboard-half if valid in the existing menu. Do not remove the existing DashBoard page. Preserve SharedAnalytics_Section and all existing menu sections.

**Implementation notes:** Place the new page near the existing Dashboard section and use a valid dashboard/admin-style icon from the existing icon set if possible.