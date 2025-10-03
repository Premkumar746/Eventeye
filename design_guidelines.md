# Design Guidelines: EventEye Certificate Automation System

## Design Approach
**Design System-Based** using Material Design principles with Linear's data-density and Notion's clarity. This creates a professional, efficiency-focused dashboard where organizers can manage certificate workflows at scale with confidence.

## Core Design Elements

### A. Color Palette

**Light Mode:**
- Primary: 260 80% 55% (EventEye purple - CTAs, key actions)
- Success: 150 65% 45% (delivered status)
- Warning: 35 90% 55% (pending status)
- Error: 0 70% 50% (bounced/failed)
- Background: 220 15% 98%
- Surface: 0 0% 100% (cards, panels)
- Border: 220 10% 88%
- Text Primary: 220 25% 15%
- Text Secondary: 220 12% 50%

**Dark Mode:**
- Primary: 260 75% 65%
- Success: 150 60% 55%
- Warning: 35 85% 65%
- Error: 0 65% 60%
- Background: 220 18% 10%
- Surface: 220 15% 14%
- Border: 220 10% 22%
- Text Primary: 0 0% 96%
- Text Secondary: 220 8% 70%

### B. Typography
- **Primary**: Inter (Google Fonts)
- **Monospace**: JetBrains Mono (for codes, IDs, QR data)
- **Headers**: 600-700 weight, tight tracking
- **Data Tables**: 400-500 weight, 1.5 line-height
- **Scale**: text-xs to text-4xl, emphasize text-sm for dense data

### C. Layout System
**Spacing Units**: 2, 4, 6, 8, 12, 16 (p-2, gap-4, m-8, py-12)
- Dashboard grid: 12-column with 4-unit gaps
- Sidebar: 280px fixed width (desktop)
- Content area: max-w-7xl with responsive padding
- Card spacing: p-6 to p-8, consistent across surfaces

### D. Component Library

**Dashboard Sidebar:**
- Fixed left navigation (280px)
- Sections: Dashboard, Certificates, Templates, Participants, Analytics, Settings
- Active state: primary background with subtle glow
- Collapsed mobile view with overlay

**Stats Cards (Dashboard Overview):**
- 2x2 grid on desktop, stacked mobile
- Large number (text-3xl font-bold) + label + trend indicator
- Icons: certificate count, delivery rate, pending queue, verification scans
- Hover: subtle border glow transition

**Certificate Template Builder:**
- Split view: Live preview (right 60%) + Controls (left 40%)
- Drag-drop zones for logo, signature, QR placement
- WYSIWYG text editor with merge field chips ({{name}}, {{event}}, {{date}})
- Color picker, font selector, layout presets
- Save/Duplicate template buttons (top-right)

**Participant Management Table:**
- Sortable columns: Name, Email, Phone, Status, Sent Date, Actions
- Bulk actions toolbar: Select all, Send, Resend, Delete
- Status badges: Delivered (success green), Bounced (error red), Pending (warning amber), Not Sent (neutral gray)
- Inline edit for quick name corrections
- AI verification toggle: Shows confidence score (0-100%) with color coding
- Search + filter bar above table
- Pagination (20/50/100 per page selector)

**Bulk Send Modal:**
- Step wizard: 1) Review (show count) → 2) Channel Select (Email/WhatsApp checkboxes) → 3) Schedule (now/later) → 4) Confirm
- Progress bar during send with real-time count updates
- Estimated time remaining indicator
- Cancel/Pause controls

**Delivery Tracking Dashboard:**
- Metrics bar: Delivered %, Bounced %, Pending count, Open Rate
- Filterable timeline view (last 24h, 7d, 30d, all time)
- Status distribution donut chart
- Export to CSV button
- Refresh indicator with last updated timestamp

**QR Code Management:**
- Generated QR preview (large, scannable)
- Download formats: PNG, SVG, PDF
- Verification URL below QR
- Analytics: Total scans, unique scans, scan locations (map placeholder)
- Regenerate/Revoke options

**AI Name Verification Panel:**
- Confidence meter: 0-100% with color gradient (red → amber → green)
- Flagged names list with suggested corrections
- Side-by-side comparison (uploaded vs. suggested)
- Approve All / Review Individually actions
- Learn More tooltip explaining AI verification

**Upload/Import Interface:**
- Drag-drop zone (bordered dashed, primary accent on hover)
- Supported formats: CSV, Excel, Google Sheets link
- Sample template download link
- Column mapping interface (if headers mismatch)
- Validation preview: Show errors before import
- Progress bar during processing

**Navigation Header:**
- Minimal top bar: EventEye logo (left), Search (center), Notifications + Profile (right)
- Breadcrumbs below header on sub-pages
- Quick actions dropdown: New Certificate, Upload Participants, Send Batch

### E. Animations
- Table row updates: Fade-in status changes (400ms)
- Modal transitions: Scale + fade (250ms)
- Progress bars: Smooth width transitions
- Hover states: Border/shadow changes (200ms)
- NO: Excessive scroll effects, decorative animations

## Images

**Dashboard Hero:** No traditional hero - dashboard opens directly to stats overview
**Template Backgrounds:** Provide 6 certificate background patterns (geometric, elegant borders, minimal textures) as selectable template bases
**Empty States:** Illustration placeholders for: No certificates yet, No participants uploaded, No delivery history
**Icons:** Material Icons for dashboard navigation, Font Awesome for status indicators

## Layout Structure

**Main Dashboard View:**
1. Stats grid (4 cards: Total Certificates, Delivery Rate, Pending, Scans)
2. Quick Actions row (New Certificate, Upload List, Send Batch buttons)
3. Recent Activity feed (left 60%, list of last 10 actions)
4. Delivery Status summary (right 40%, mini chart + breakdown)

**Certificate Builder (Full Page):**
- Left Panel: Template selector, Text fields, Design controls, Save/Preview
- Right Panel: Live certificate preview (A4 aspect ratio), Zoom controls, Download test

**Participants List (Table View):**
- Filter bar (sticky top)
- Bulk action toolbar (appears when rows selected)
- Main data table (full width, 100vh - headers)
- Floating action button (+ Add Participant, bottom-right)

**Delivery Tracking:**
- Metrics dashboard (top third)
- Filterable table (bottom two-thirds)
- Export/Refresh controls (top-right)

## Multi-Column Strategy
- Dashboard: 2-column split (60/40 for activity feed + summary)
- Stats cards: 4-column grid (responsive: 1 → 2 → 4)
- Tables: Full-width single column for data integrity
- Certificate builder: 40/60 split (controls/preview)

## Accessibility & Trust Signals
- WCAG AAA contrast in tables (critical for data scanning)
- High-visibility status colors (accessible red/green for colorblind)
- Toast notifications for all actions (success/error)
- Loading states with clear messaging
- SSL badge in footer, Terms/Privacy links
- "AI-verified" badge with explanation tooltip
- Data export audit trail