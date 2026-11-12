# Digital Menu & Stock Dashboard

## Version 1 Product Requirements Specification

**Document Version:** 1.1  
**Status:** Development Baseline  
**Product:** Digital Menu & Stock Dashboard  
**Organization:** Sucrée Bakery & Café

---

## 1. Product Overview

### 1.1 Purpose

The Digital Menu & Stock Dashboard is a mobile-responsive web application designed to provide customers with an accessible digital menu while allowing authorized café staff to monitor and update item availability.

Customers access the menu by scanning a QR code displayed at café tables. Staff use a separate authenticated dashboard to update availability and identify products that are running low.

The application centralizes menu visibility and stock-status communication, helping staff respond to availability changes without relying solely on verbal updates.

### 1.2 Objectives

The application aims to:

1. Provide customers with an accessible, mobile-friendly digital menu.
2. Display current menu items, categories, prices, and availability.
3. Allow authorized staff to update item availability and low-stock indicators.
4. Inform staff about unavailable and low-stock items through a shared dashboard and notifications.
5. Maintain an activity history of stock-status changes.
6. Keep the public menu synchronized with successfully saved availability updates.

### 1.3 Target Users

- **Customers:** Browse the public digital menu.
- **Authorized Staff:** View the staff dashboard, update stock indicators, receive notifications, and review activity history.
- **Developer / System Administrator:** Provision staff accounts, maintain menu data, configure product labels, and manage application deployment.

---

## 2. User Access and Permissions

### 2.1 Customer Access

- Customers can access the public menu through a QR code or direct URL.
- No account registration or login is required.
- Customers cannot modify menu information or stock statuses.

### 2.2 Staff Access

The following staff members are eligible for application access:

- Owner
- Cooks
- Baristas
- Cashiers / Front-of-House staff

Utilities and dishwashing personnel are excluded from the staff dashboard.

All authorized staff share the same application permission level. There are no separate owner, manager, or department-specific permissions within the application.

Each staff member must have an individual account.

### 2.3 Account Provisioning

- Staff accounts are created and maintained by the designated developer through a controlled provisioning process.
- Public staff registration is not available.
- The application does not include a staff account-management interface.
- Staff must use their own credentials.
- Passwords must be securely hashed and must never be stored in plaintext.
- Access must be restricted to active, provisioned accounts.

### 2.4 Developer Responsibilities

The developer maintains:

- Staff account eligibility and provisioning.
- Menu categories and item records.
- Product names, descriptions(optional), images(optional), prices.
- New and Bestseller identifiers.
- Application configuration and deployment.

These operations are managed through controlled backend, database, or administrative processes outside the staff dashboard.

---

## 3. Customer-Facing Digital Menu

### 3.1 Menu Access

- Each café table has a QR code that directs customers to the public digital menu.
- The menu must be responsive across mobile phones, tablets, and desktop browsers.
- No application installation is required.

### 3.2 Menu Categories

The menu is organized into the following categories.

#### Drinks

1. Coffee
2. Signature Drinks
3. Milk-Based
4. Tea
5. Matcha & Hōjicha

#### Food

1. Bakery
2. Starters
3. Salads
4. Sandwiches
5. Entrée & Pasta

#### Separate Menu Section

- Add-ons & Customizations

### 3.3 Menu Item Information

Each menu item may display:

- Item name
- Description, when available
- Product image, when available
- Individual price
- Availability
- New label, when applicable
- Bestseller label, when applicable

### 3.4 Pricing

Some products have multiple serving options, while others have only one.

Examples include:

- Hot
- Iced

Each serving variant must have its own price.

The system must support:

- One menu item with multiple serving variants.
- One menu item with a single serving option.
- Individual prices for each variant.
- Parent-level availability shared across all serving variants.

A stock-status update to a parent menu item applies to all of its serving variants.

### 3.5 Add-ons & Customizations

Add-ons must be displayed in a separate section, with their respective names and prices.

Initial add-on records include:

- Sub Oat
- Sub Non-fat
- Salted Crème
- Sub Breve
- Splash Breve
- Syrup
- Sauce
- Splenda
- Vanilla Whey Protein (10g)

Add-ons are independently stock-tracked. Each add-on has its own availability and low-stock indicators, separate from the main menu items.

### 3.6 Customer-Facing Availability Display Rules

The public menu must follow these rules:

| Internal condition | Customer-facing display |
| --- | --- |
| Available | No availability label displayed |
| Available + Low on Stock | No availability label displayed |
| Out of Stock | Temporarily Out of Stock |

Additional requirements:

- Items marked Available must appear normally without an explicit "Available" label.
- Items marked Low on Stock must remain visible without displaying their low-stock indicator or remaining-order count.
- Items marked Out of Stock must display the exact label "Temporarily Out of Stock".
- Out-of-stock items must remain visible in the menu so customers can see that the item is temporarily unavailable.
- The customer-facing interface must not expose internal stock indicators, remaining-order counts, staff identities, or activity information.

### 3.7 New and Bestseller Labels

Menu items may be tagged as:

- New
- Bestseller

These labels are manually maintained through the controlled backend or database process.

The application must not automatically calculate these labels using sales data or analytics in Version 1.

An item may have either label, both labels, or neither.

---

## 4. Staff Dashboard

### 4.1 Dashboard Purpose

The staff dashboard provides a centralized view of items that require operational attention.

It must display:

1. Low on Stock items.
2. Out of Stock items.

The dashboard must organize these items by their respective menu categories and clearly identify their current status.

The dashboard must be usable on the company's shared phone and other supported devices.

### 4.2 Dashboard Item Information

Each displayed item should include:

- Item name
- Category
- Current stock indicator
- Remaining orders, when marked Low on Stock
- Last updated timestamp
- Staff member responsible for the latest update

Add-ons must also appear in the dashboard and be identifiable as add-ons rather than ordinary menu items.

### 4.3 Stock Indicators

The application uses two independent operational indicators:

#### A. Availability

- Available
- Out of Stock

#### B. Low on Stock

- Enabled
- Disabled

The availability indicator determines whether the item can still be offered to customers.

The Low on Stock indicator identifies items that are still available but have limited remaining order capacity.

These indicators must be handled independently while respecting the interface rules below.

---

## 5. Stock Management and Update Workflow

### 5.1 Availability Control

Every main menu item and add-on must have an availability control.

The staff member can set an item to:

- Available
- Out of Stock

When an item is marked Out of Stock:

- The item must be displayed as unavailable on the public menu.
- The Low on Stock control must be hidden.
- Any existing low-stock indicator and remaining-order value must be cleared.
- The item must appear in the Out of Stock section of the staff dashboard.

When an item is changed back to Available:

- The item becomes available on the public menu.
- The Low on Stock control becomes accessible again.
- The item is removed from the Out of Stock section if no other applicable condition requires it to appear.

### 5.2 Low on Stock Control

The Low on Stock control is available only when an item is marked Available.

The staff workflow is as follows:

1. The staff member opens an available item.
2. The staff member enables the Low on Stock indicator.
3. The indicator is replaced by a remaining-order counter.
4. The counter displays an initial value of 4.
5. Plus and minus buttons allow the staff member to adjust the value.
6. A button labeled **Update**, positioned beside the counter, submits the change.
7. Once the update succeeds, the item appears in the Low on Stock section of the staff dashboard.

The counter must follow these limits:

- Minimum: 1
- Maximum: 4
- Initial value: 4

The plus button must be disabled when the value is 4.

The minus button must be disabled when the value is 1.

The backend must enforce these limits, including for direct API requests.

### 5.3 Remaining Orders Definition

The counter represents the approximate number of additional customer orders that the café can fulfill before the item is expected to become unavailable.

It does not represent a standardized physical measurement such as pieces, grams, liters, or servings.

Examples:

- Chicken Pesto – 1 remaining order
- A beverage – 3 remaining orders
- An add-on – 2 remaining orders

The same remaining-order concept applies to both main menu items and add-ons.

The count is manually maintained by authorized staff. It is not automatically deducted when a customer places an order, because Version 1 does not support online ordering or automatic sales integration.

Staff must update the count as operational conditions change.

### 5.4 Low on Stock Update Behavior

- Enabling Low on Stock initializes the counter to 4.
- Adjusting the counter must not immediately modify the persisted value.
- The staff member must select **Update** to submit the adjusted value.
- A successful update persists the new remaining-order value and update timestamp.
- A successful update creates the corresponding activity record and staff notifications.
- Disabling Low on Stock clears its saved remaining-order value.
- Marking an item Out of Stock clears its Low on Stock indicator and remaining-order value.
- If the staff member leaves without updating, the previously saved state remains unchanged.
- The Update button must provide appropriate feedback while the request is processing and after success or failure.

### 5.5 Parent-Level Stock Tracking

Availability and low-stock indicators are tracked at the parent menu-item level.

For example, marking Latte as Out of Stock makes both its Hot and Iced variants unavailable.

The same principle applies to other items with multiple serving variants.

Each add-on, however, is an independently tracked item with its own availability and low-stock state.

### 5.6 Manual Stock Updates

Stock indicators are manually updated by authorized staff based on actual café operations.

The application does not:

- Automatically deduct remaining orders.
- Calculate stock from sales transactions.
- Perform live inventory accounting.
- Predict stock depletion.

The dashboard is an operational communication tool, not a full inventory-management or point-of-sale system.

---

## 6. Notifications and Activity History

### 6.1 Notifications

Every successful stock-status change must generate persistent notifications for all active staff accounts, including the staff member who performed the update.

Notifications must communicate:

- Item name
- Previous status
- New status
- Remaining orders, when applicable
- Staff member who made the change
- Date and time of the update

Notifications must be available through the staff dashboard and remain accessible after logout or when accessed from another device.

### 6.2 Notification Read Status

- Each staff member has an individual notification read/unread state.
- Reading a notification must not change its state for other staff members.
- Notifications must remain stored until removed through a controlled retention process outside ordinary staff interactions.

### 6.3 Real-Time Updates

When a staff member successfully saves a stock update:

- The public menu must reflect the committed state promptly.
- Connected staff dashboards must receive the corresponding update.
- Connected staff devices must receive real-time notification events.

Server-Sent Events (SSE) may be used for real-time delivery.

The system must support reconnection and retrieval of missed persistent notifications after a connection interruption.

A real-time delivery failure must not prevent a successfully committed stock update or its persistent notification from being saved.

### 6.4 Activity History

Every successful change to an item's availability or Low on Stock state must create an activity-history record.

The record must include:

- Item name or item reference
- Previous state
- New state
- Remaining-order value, when applicable
- Staff member responsible
- Timestamp

Activity records must be immutable through the staff application.

Staff cannot edit or delete activity-history entries.

If an incorrect update occurs, staff must submit a new correct update. The new action must be recorded as another activity.

Unchanged submissions must not create duplicate activity records or notifications.

---

## 7. Business Rules

The following rules govern Version 1 behavior.

| ID | Business Rule |
| --- | --- |
| BR-01 | Only provisioned, active staff accounts can access the staff dashboard. |
| BR-02 | All authorized staff have equal application permissions. |
| BR-03 | Customers can access the public menu without authentication. |
| BR-04 | Every main menu item has an independent availability and Low on Stock state. |
| BR-05 | Every add-on has its own independently tracked availability and Low on Stock state. |
| BR-06 | Low on Stock is available only when an item is Available. |
| BR-07 | Remaining Orders must be an integer from 1 to 4. |
| BR-08 | Enabling Low on Stock initializes Remaining Orders to 4. |
| BR-09 | Out of Stock clears the Low on Stock state and its remaining-order value. |
| BR-10 | Disabling Low on Stock clears its remaining-order value. |
| BR-11 | Remaining Orders are manually updated and are not automatically deducted. |
| BR-12 | Availability is tracked at the parent menu-item level and applies to all serving variants. |
| BR-13 | Each serving variant has its own price. |
| BR-14 | New and Bestseller labels are maintained through a controlled backend or database process. |
| BR-15 | Successful stock changes generate activity-history records and persistent staff notifications. |
| BR-16 | Staff cannot edit or delete activity-history records through the application. |
| BR-17 | Low-stock details are visible to staff but not to customers. |
| BR-18 | Menu catalog and staff account provisioning are maintained outside the staff dashboard. |

---

## 8. Scope

### 8.1 Included in Version 1

- Public QR-based digital menu.
- Responsive customer-facing interface.
- Menu categories and item listings.
- Individual serving-variant prices.
- Separate Add-ons & Customizations section.
- Main menu item stock tracking.
- Independent add-on stock tracking.
- Available / Out of Stock controls.
- Low on Stock controls.
- Remaining-order counter from 1 to 4.
- Plus, minus, and Update interactions.
- Staff authentication.
- Staff dashboard grouped by category.
- Dashboard visibility for low-stock and unavailable items.
- Persistent staff notifications.
- Real-time update delivery for connected staff.
- Activity history.
- New and Bestseller labels.
- Developer-managed menu data and staff account provisioning.

### 8.2 Excluded from Version 1

- Online ordering.
- Online payments.
- Customer accounts.
- Customer order tracking.
- Point-of-sale integration.
- Automatic stock deduction.
- Full inventory management and purchasing workflows.
- Automatic sales-based Bestseller calculations.
- Automatic New label assignment.
- Staff account registration or management screens.
- In-app role or permission management.
- Menu item, category, or price management screens.
- Editing or deleting activity-history records.
- Variant-level stock tracking.
- Automated demand forecasting.

---

## 9. Nonfunctional Requirements

### 9.1 Performance

- The public menu must load efficiently on typical mobile connections.
- Stock updates must be processed promptly.
- The dashboard must not require a full page reload for real-time updates.
- Database queries should use appropriate indexes and avoid unnecessary data retrieval.

### 9.2 Security

- Use HTTPS in production.
- Implement secure authentication and server-side authorization.
- Protect all staff endpoints.
- Use secure password hashing.
- Use secure, HTTP-only session cookies where server-managed sessions are used.
- Apply CSRF protection to state-changing requests.
- Validate all incoming requests on the backend.
- Prevent unauthorized access to staff-only data.
- Never expose staff identities, internal remaining-order counts, notifications, or activity records through public menu endpoints.
- Protect credentials, environment variables, and application secrets.
- Maintain security logging without exposing sensitive information.

### 9.3 Reliability and Data Integrity

- Successful stock updates must be persisted in the database.
- Stock changes, activity records, and persistent notifications must be saved consistently.
- The application must prevent invalid remaining-order values.
- Concurrent updates must not silently overwrite one another.
- Real-time delivery failure must not compromise persisted data.
- Regular database backups and restore testing must be maintained.

### 9.4 Maintainability

- Use modular, maintainable application architecture.
- Separate frontend presentation, backend business logic, and persistence concerns.
- Use dedicated request and response DTOs.
- Maintain database schema changes through versioned migrations.
- Document significant architectural decisions.
- Include automated tests for critical business rules and workflows.

### 9.5 Compatibility

- Support modern mobile and desktop browsers.
- Prioritize mobile usability for staff dashboard interactions.
- Support the company's shared phone as a primary staff notification and dashboard device.

---

## 10. Acceptance Criteria

### Customer Menu

#### AC-01 – QR Access

Given a customer scans a café QR code, when the destination opens, then the public digital menu must load without requiring authentication.

#### AC-02 – Menu Display

Given the public menu loads, then the customer must be able to browse the configured categories, items, and individual prices.

#### AC-03 – Customer Availability Display

Given an item is Available, when the customer views the menu, then no explicit "Available" label must be displayed.

Given an item is marked Low on Stock, when the customer views the menu, then it must remain visible without an availability label or low-stock details.

Given an item is Out of Stock, when the customer views the menu, then the exact label "Temporarily Out of Stock" must be displayed.

#### AC-04 – Low-Stock Privacy

Given an item is marked Low on Stock, when the customer views the menu, then the item must remain displayed as Available without revealing its remaining-order count.

### Staff Dashboard

#### AC-05 – Staff Authentication

Given an active provisioned staff member enters valid credentials, when authentication succeeds, then the staff dashboard must become accessible.

#### AC-06 – Dashboard Organization

Given there are low-stock or unavailable items, then the dashboard must display them in their respective sections, grouped by category.

#### AC-07 – Availability Update

Given a staff member changes an item to Out of Stock, when the update is successfully saved, then the item must appear in the Out of Stock section and become unavailable on the public menu.

#### AC-08 – Low-Stock Update

Given an item is Available, when a staff member enables Low on Stock, then the remaining-order counter must appear with an initial value of 4.

#### AC-09 – Counter Validation

Given the remaining-order counter is displayed, then the staff member must not be able to decrease it below 1 or increase it above 4.

### AC-10 – Low-Stock Update

Given a staff member adjusts the remaining-order counter, when the staff member selects the "Update" button and the backend accepts the request, then the new value must be persisted, reflected in the dashboard, and recorded in the activity history.

#### AC-11 – Independent Add-on Tracking

Given an add-on's availability or Low on Stock state changes, then only that add-on's stock state must be updated, independently of other add-ons and main menu items.

#### AC-12 – Notifications and Activity History

Given a successful stock-state change occurs, then the system must save an activity record and persistent notifications for active staff accounts.

#### AC-13 – Real-Time Synchronization

Given staff members are connected to the dashboard, when another staff member successfully updates an item's stock state, then connected dashboards must receive the update without requiring a manual page refresh.

#### AC-14 – Activity Integrity

Given an activity record exists, then staff must not be able to edit or delete it through the application.

---

## 11. Technical Design Considerations

The implementation should follow a pragmatic, maintainable architecture.

### 11.1 Proposed Technology Stack

- **Frontend:** Angular
- **Backend:** Java with Spring Boot
- **Database:** PostgreSQL
- **Real-Time Communication:** Server-Sent Events (SSE)
- **Database Migration:** Flyway
- **Containerization:** Docker
- **Version Control:** Git and GitHub
- **CI/CD:** GitHub Actions

Framework and dependency versions must be verified against official compatibility and support information when implementation begins.

### 11.2 Suggested Data Model

Core entities:

1. `users` – staff accounts and account status.
2. `categories` – public menu categories.
3. `menu_items` – main menu products and their stock states.
4. `menu_item_variants` – serving options and individual prices.
5. `menu_add_ons` – independently tracked add-ons and their prices.
6. `stock_activity_logs` – immutable stock-change history.
7. `notifications` – persistent, per-staff notifications.

### 11.3 Stock-State Representation

The application should model availability and low-stock status separately.

Suggested conceptual fields for both main menu items and add-ons:

- `availability_status`: `AVAILABLE` or `OUT_OF_STOCK`
- `low_stock_enabled`: Boolean
- `remaining_orders`: Nullable integer, constrained to 1–4 when Low on Stock is enabled

The backend must enforce these invariants:

- `OUT_OF_STOCK` requires `low_stock_enabled = false` and `remaining_orders = null`.
- `AVAILABLE` with Low on Stock disabled requires `remaining_orders = null`.
- `AVAILABLE` with Low on Stock enabled requires `remaining_orders` between 1 and 4.

This model avoids treating Low on Stock as a mutually exclusive availability status.

### 11.4 API Design Considerations

Example public endpoints:

- `GET /api/public/menu`
- `GET /api/public/menu/categories`

Example staff endpoints:

- `GET /api/staff/dashboard`
- `PATCH /api/staff/menu-items/{id}/availability`
- `PATCH /api/staff/menu-items/{id}/low-stock`
- `PATCH /api/staff/add-ons/{id}/availability`
- `PATCH /api/staff/add-ons/{id}/low-stock`
- `GET /api/staff/notifications`
- `PATCH /api/staff/notifications/{id}/read`
- `GET /api/staff/activity-history`
- `GET /api/staff/events`

These are proposed endpoint contracts and may be refined during API design.

### 11.5 Backend Validation

- All stock updates must be validated server-side.
- Staff identity must be derived from the authenticated session, not trusted from client-submitted data.
- The server must generate update timestamps.
- Invalid state combinations must be rejected.
- Concurrent updates must be handled through version checks or optimistic locking.
- Stock updates and their corresponding activity and notification records must be committed consistently.

---

## 12. Definition of Done

A feature is considered complete when:

- Its documented functional requirements are implemented.
- Frontend and backend validation are in place.
- Relevant automated tests pass.
- Access control and security requirements are satisfied.
- Error and edge cases are handled.
- The implementation has been reviewed.
- Relevant documentation is updated.
- The feature works in the intended deployment environment.

The Version 1 release is ready for café use only after critical workflows have been tested, security checks have passed, backups have been configured, and the staff dashboard has been validated on the company's shared phone.

---

## 13. Development Notes and Decisions

The following implementation principles apply throughout development:

1. Keep the application focused on its primary purpose: public menu visibility and internal stock-status communication.
2. Avoid introducing full inventory, ordering, or POS capabilities into Version 1.
3. Treat remaining orders as an approximate operational estimate, not an automatically calculated inventory quantity.
4. Keep main menu items and add-ons independently stock-tracked.
5. Keep serving variants under their parent menu item for stock purposes.
6. Protect internal staff information and stock indicators from public access.
7. Prefer simple, reliable architecture over unnecessary infrastructure.
8. Record important architectural and implementation decisions in the project documentation.

**End of Version 1 Product Requirements Specification.**
